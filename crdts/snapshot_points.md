# State snapshot consensus on a distributed P2P network

### Main Problem

Consider a distributed data structure shared by n nodes in a P2P network. Each node maintains a replica of the distributed structure. Nodes may modify the data structure locally and gossip those changes in the form of operations to other nodes in the network, so that these can also apply locally the operations applied by remote nodes. The network will eventually agree on the data structure state when all nodes have same set of operations locally. Each operation can be uniquely identified in the network and can be casually ordered (i.e. all nodes agree on the same casual order of the operations, even without network or clock sync guarantees)

Since the network converges over time - as each local node receives and applies operations by other nodes - it is not possible to ensure that  all the operations have been applied locally in every node of the network at a given point in time. How can a node decide locally what is the minimum common set of continguos operations applied in every node in the network at a given time?

A state snapshot is the minimum common state that all replicas in the network have applied at a given time. The state snapshot must be decided locally, without any coordination entity.

Once a node decides on a snapshot point, it can only communicate safely with nodes in the network which have the same snapshot point.

### Solution

A node can decide about the state snapshot if it has visibility of the nodes in the network and their states (which operations have been applied). A network map is the local data structure which maintains the current view of the network. It consists of a map per known node in the network with data about which operations they’ve applied and which nodes they know from existing in the network.

Example of a network map on a node N1

```
{
 N2: {
  N2: [A,B,D],
  N3: [A,B]
 },
 N3: {
  N2: [A,B],
  N3: [A,B,C],
  N4: [A,B]
 }
}
```

Based on the above network map example, if N1 itself has applied [A,B] set of operations, he can locally guarantee that [A,B] is the current snapshot point, since all the nodes he's aware of in the network have applied that subset of operations. 

### Obstacle 1 - inconsistent snapshot point when new nodes join the network

When a new node joins the network, it will request the current data structure to one of the existing nodes - not necessarily the one with the most updated state.

In the above case, a new node N5 may have joined the network and received the state [A] from N2 which, at the time, had only operation A applied. This solution does not prevent N1 from deciding [A,B] as being the snapshot point, which is not correct, since N1 had no visibility that N5 existed and thus, N5 may consider different snapshot points locally.

Solution obstacle 1

N1 needs to know that N2 had shared the state with N5, and that state was only [A]. Thus, everytime a new node joins the network it should be added to the network map of the node which shared the initial state with it. If this is the case, then N1 network map would have been the following:

```
{
 N2: {
  N2: [A,B,D],
  N3: [A,B],
  N5: [A]
 },
 N3: {
  N2: [A,B],
  N3: [A,B,C],
  N4: [A,B]
 }
}
```

In this case, N1 would consider [A] as the snapshot point and could safely communicate with all nodes in the network.

The requirement that N2 needs add N5 when sharing its data structure when N5 is joining constraints the network communication model. For example, pure gossip cannot be used since there is no mechanism for N2 to ensure that N5 has received its state. Thus, potentially leading to the case described above. A possible solution is to keep gossip communication between nodes in the network but making sure that joining the network follows a different protocol in which both nodes - the new node and the node sharing the initial state - communicate directly, allowing the node already in the network to add it to its network map.

As a general rule, a node in the network must be at least in one network map of a remote node. When this is the case, nodes can safely decide the snapshot point based on its local network map.

### Obstacle 2 - snapshot point deadlock
