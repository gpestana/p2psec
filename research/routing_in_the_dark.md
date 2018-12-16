## Routing in the Dark: Pitch Black
**Nathan S. Evans, et al.**

**what**: Freenet `darknet` implements a decentralized routing algorithm under a
restricted-routing topology (friend-2-friend). the routing algorithm relies on
location swapping for improving lookup performance of such topologies to 
`Olog(n)`, under the conditions that trusted node connections form a small-world
network. the paper studies how relatively low-resourced attackers can subvert
the network topology and content availability by lying about their links during 
the location swapping protocol.

**results**: the authors show how the Freenet's `darknet` routing algorithm is
unable to provide performance guarantees when adversaries abuse the location
swapping protocol. a possible solution is to add computation verification 
algorithm to the protocol so that nodes can verify the claims of
their neighbours and their view of the network during the location swapping
protocol.

**importance**: decentralized p2p networks are hard to keep private and
restricted-routing topologies may help to solve it by only allowing connections
between trusted peers. in such conditions, the lookup/routing performance is
much poorer than `clearnet` decentralized networks, but the Freenet `darknet` 
algorithm achieves `Olog(n)` performance.

**small-world networks**: a small-world network is defined by networks in which
the shortest path to any node in the network is "small" (at least
logarithmically smaller) compared to the size of the network. small-world
networks are characterized by large coefficient of clustering (as in structured
networks) and average shortest path length close to those of random networks (as
in random networks).

**Freenet darknet routing algorithm**: Freenet implements a `darknet` routing
algorithm in which nodes are connected only to peers they trust. the main reason
for this is to obscure the activity of the nodes in the network (assuming that
trusted nodes are not attackers). a link between any peer in the network exists
only if both peers agree on it and Freenet assumes that there will be enough
links between peers in the network so that every peer will be connected in a 
small-world topology.

**restricted network topologies and content routing**: when the lookup of
content is successful, the content routing has to traverse the same path back
from the node in which the content was found to the node which performed the
lookup. this property makes sure that only trusted nodes are connected with each
other (as expected in a` darknet`).

**location swapping**: the Freenet overlay topology is created so that peers
with closer keys are as close together (connected) as possible. this is achieved
by a location swapping algorithm which aims at swapping nodes deterministically
if after swapping their respective neighbours have keys closer to them then
before the swapping. the location swapping protocol builds the network topology
that requires only average of `Olog(n)` steps for routing, assuming that the 
legal links between nodes form a small-world network.

**attack 1 - active**: the goal of the attack is to affect the network topology by
attacking nodes to swap to an arbitrary location. the attacker can lie about its
distance to nodes in order to force swapping to an arbitrary position in the network. a
victim cannot verify the information provided by the attacker before swapping because 
their connections are limited to trusted network, so their visibility of the
network is different. the attacker node can continue swapping its location until
it reaches the intended location. once an attacker actor adds enough nodes to
the same location, it has control over the content indexed in that location and
may drop all `GET` requests, effectively damaging content availability in the
network.

**attack 2 - passive/churning**: the authors show that natural node churning may
aid the attacker and even damage the network without existence of malicious nodes.
the location swapping algorithm under heavy `join-leave` churn (when a node 
leaves the network for good) adds swapping bias of locations among long-lived
peers. high `join-leave` churning will have the same results as the active
attack in the network.

**experiment**: the performance metrics used were 1) avg path length for key
lookup; 2) % of original content in the network that is still available; the
experiments show that with relative few resources, the attackers can effectively
a) force network unbalance and clustering - resulting in longer avg path lengths
that expected in small-world networks and hitting lookup performance and b)
large amounts of original content is lost from the network. the experiment also
shows how natural `join-leave` churning leads to unbalanced clustering of nodes.

---

**Q1:** does the location swapping algorithm take into consideration that after
the swapping, all nodes are still connected to verified and trusted nodes? (I
expect so, otherwise the network is not a `darknet` anymore)

**Q2:** what are the benefits and drawbacks of restricted-route topologies and
routing schemes (e.g. small-world network) in decentralized networks? (focus on 
a metadata resistance perspective).

**Q3:** could a zero-knowledge proof solve the active attack vector by adding a
layer of secure multipart computation verification?

One way to verify if nodes are lying is, ass the authors put it in the paper:

```
If there were a way for a node which purported to have
a certain number of friends to prove that all those friends
existed, nodes could be more confident about swapping.
```

