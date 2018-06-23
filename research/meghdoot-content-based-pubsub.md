#Meghdoot: Content-Based Publish/Subscribe over P2P Networks

Meghdoot implements a content-based publish-subscribe system over a DHT based on
Content Addressable Network (CAN) by defining algorithms for subscription
installation and event delivery which improve load distribution and replication
in P2P content-based pubsub systems. It defines peer management algorithms -
peer joining the network, peer departure/failure, event delivery and
subscription installment - to better balance load among peers and scaling up
well as number of peers, subscriptions and events increase. 

Problem: in a P2P network where peers subscribe to events happening in the
network, how to make sure that the load is balanced between peers (e.g. not
a few set of peers are responsible for routing and storing events or
subscriptions)?

Solution: when storing subscriptions, Meghdoot splits CAN euclidean zones so that
subscriptions are better spread among peers (subscription load balance). It also
defines how to add more peers to same zones so that subscriptions are replicated
in the network to avoid losses of subscriptions when nodes are down. When 
delivering events, Meghdoot creates alternative propagation event paths in order
to balance the event delivery load.

### P2P pubsub network using CAN

### Subscription load

### Event load

### Peer join

### Peer departure or failure

### Experimental evaluation

### Questions:

Q: Can Meghdoot algorithm support an infinite set of subscription parameters? 
(since it uses CAN as the structure p2p overlay, can CAN support it?)

Yes. Meghdoot algorithms for subscription/event delivery are compatible with an
infinite set of subscription parameters. In CAN, a key is mapped onto a point in
the logical space. The mapping is calculated by a deterministic hashing
function. Thus, the hashing function must support deterministic mapping of 
infinite key values onto the logical space with N dimensions. The more
dimensions the logical space has, the more subscription storing and routing can 
load be optimized.

Q: Is there any production P2P network using the Meghdoot protocol? If so, how
  does it compare with the simulation results?

To my current knowledge, there is no pubsub p2p network using Meghdoot in
production.


### Further reading

[1] [A Scalable Content-Addressable
Network](https://dl.acm.org/citation.cfm?id=383072)
---

## notes

> these notes where taken while reading the paper

content based pubsub systems to DHTs over P2P networks with load balancing among
peers and scalability with increasing number of peers, subscriptions and events


Q-1: what does "scalability" and "load balancing" mean in practice in this
context?

pubsub allow publishers to deliver targeted content to subscribers in a
  decoupled manner;

pubsub system is responsible for managing the subscriptions and deliver the
events to the matching subscriptions.

in p2p systems, peers are used to store and to route events to other peers in
the network which have subscribed to the events.

content based p2p systems the events are distributed based on the event's
content. this leads to poorly balanced networks, in which few of the peers
forward disproportional load.

Q-2: are there any mechanisms for flow control in p2p pubsub networks?

older p2p networks used centralized subscriptions or flooding algorithms to
implement pubsub systems; more sophisticated p2p networks rely on logical
overlay network formed by peers, such as DHTs (e.g. CAN, Chord, Pastry,
Tapestry).

### pubsub model in Meghdoot

content-based pubsub system with multiple attributes for fine granularity when
subscribing to content; each attribute has a name, type and domain.

a subscription is a set of equalities or range over one or more attribute.

an event `e` matches the subscription S if its values match with the
subscription definition

e.g.:

```
attributes {T temperature; C country}
subscription S = {temperature > 10; country = Finland} 
event E = {T: 23, C: Finland}
```
the pubsub system is responsible for:

a) store subscriptions defined by the users; and 
b) find subscriptions matching the event

### logical space construction

how to construct the logical address space in the overlay network. the logical
space is used for maintaining the distributed hash table

the logical space is partitioned among the peers in the network. each peer owns
a zone in the network.

**CAN - content address network**
CAN is a distributed system that maps keys onto values; keys hashed into `n` 
dimensional space

the peers maintain a DHT as described in CAN; CAN builds and maintains an
overlay network in which every peer has a point assigned within the cartesian
space (independent of the physical node location). each peer owns its own zone
within the cartesian space. the routing in CAN is done by a routing table
maintained by each peer which maintains a map between peer address and their
coordinates.

Q-3: does Megdhoot supports infinite `n` attributes in the schema? this would 
mean a `2n` logical cartesian space which would be infinite.

### subscription installation

first, a peer creating a subscription must calculate in which zone is the
subscription being installed. after, it should route the subscription request by
forwarding the subscription request to the neighbor which is closest in the CAN
euclidean space of the target peer. this process is repeated until the
subscription reaches the destination zone.

a `subscription point` is a point in the euclidean space in which the
subscription was installed


Q-4: still not sure how to calculate in which logical zone the subscription
should be installed

### event delivery

an `event point` is a point in the euclidean space in which the event was
installed

Q-5: still not sure how to calculate in which logical zone the event should be
redirected to

### load characteristics

a peer may be loaded with subscriptions and/or events -- this means that a peer
in the network may store a set of subscriptions or a set of events. 

a peer which stores subscriptions is responsible for delivering the events to
the subscribers. thus a load from subscriptions is proportional to the number of
subscriptions the peer keeps.

load from event delivering/routing comes from the fact that peers need to route
the event to the correct zone. in this case, splitting the zone into smaller
zones does not help, since the routing will most likely pass through the same
peers.

in order to achieve better load balance for event delivery, loaded zones must be
replicated and the events should be routed randomly through the multiple paths
available to reach the event point.
   
        
```
          _Z1.   
_ _ _ _ /     \ _ _ _ _ >> 
        \ _Z2. /

```
Z1 and Z2 can now split the load for the routing

the zone replication can be achieved by copying all the subscriptions of an
overloaded node, N1, to a new node, N4, which is joining the network. the 
neighbors of N1 need to store the address of N4 alongside with N1 and select
randomly where to route the event (either N1 or N4). this will probabilistically
split the load on N1 in 50%, since the neighbors have 2 paths where to route the
event to.

### peer join

when a new peer joins the network, the contacted peer in the network which is 
responsible suggest a coordinate to the new peer will check if there are
overloaded zones. for this, each peer maintains information about its load as
well as it's neighbors and calculate which peers are most likely loaded the
most.

when a loaded peer is found, it will decide whether to partition itself when a
new node joins the network based on local conditions (see paper notes on how to
find out a loaded node)

if the peer is loaded because of too many subscriptions, then the zone is split
into two, in order to split the subscription load between the two zones.


### experimental setup

based on

---

load:
 - read and notes: |||
