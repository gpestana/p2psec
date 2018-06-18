##Meghdoot: Content-Based Publish/Subscribe over P2P Networks

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

the peers maintain a DHT as described in CAN; CAN builds and maintains an
overlay network in which every peer has a point assigned within the cartesian
space (independent of the physical node location). each peer owns its own zone
within the cartesian space. the routing in CAN is done by a routing table
maintained by each peer which maintains a map between peer address and their
coordinates.

Q-3: does Megdhoot supports infinite `n` attributes in the schema? this would 
mean a `2n` logical cartesian space which would be infinite.

### Subscription installation

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
