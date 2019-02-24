## Route Fingerprinting in Anonymous Communications
**George Danezis, Richard Clayton**

**what**: partial view of the network can be used to uniquely fingerprint nodes in a P2P network, based on the information the nodes have learned. The paper discusses an example of route fingerprinting of Tarzan, an anonymous communication system  

**results**: 2 attacks on Tarzan initial design against the route reconstruction protocol and the circuit relay protocol

**importance**: it is important to consider an holistic view of anonymous networks and consider all the potential leak and attack surfaces, specially when creating and managing secure onion and mix circuits with partial view of the network.

---

**partial view of P2P anonymous networks**: partial network view gives room to potential privacy attack surface due to the peer discovery and route (re)construction. (this is a similar problem that Shadowwalker tries to solve).

**Tarzan**: an anonymous p2p network in which every node is a mix. This work focus on fingerprinting of traffic based on nodes' partial view of the network. Tarzan provides a route reconstruction protocol

**route reconstruction attack**: when a circuit relay churns or is unreliable, the circuit "owner" can trigger a route reconstruction protocol to replace the unresponsive node. The protocol opens up a vulnerability in which an adversary will eventually control all the nodes in the circuit. The attack works as follow: the attacker controls one node in the circuit and performs a DoS attack against the next node in the circuit (the one he's aware of). Once the circuit owner realizes about the unresponsive node, it will trigger the routing reconstruction protocol. If the new node selected is part of the adversary nodes, it will proceed with the same attack against the next honest relay. This can be extrapolated until the adversary controls the whole circuit without being detected. [this attack has been discarded in favor of reconstructing the whole circuit].

**selecting nodes for secure circuits**: important for P2P anonymous communications based on onion routing and mix routing. However, there isn't a scalable, decentralized and secure protocol for partial view decentralized networks (maybe Shadowwalker?). Attackers may often poison the bootstrap/finger table of nodes trying to pick random nodes from the network and perform network analysis to limit the set of possible relays chosen. These attacks easily provide an attacker knowledge about the circuit path and subsequent de-anonymization. 

**for system designers**: 1) unwise select a small amount of nodes as seed for constructing secure circuits (small relatively to size of the network); 2) important problem is how to maintain circuits under churn without having to reconstruct the whole circuit in a secure manner. 

---

- When there is node churn/unreliability of a relay in a circuit, how much of a problem is it to construct a new circuit for DHT lookups instead of reconstructing (i.e. replacing) the failing node? In DHTs I'd expect to use "ephemeral" circuits instead of keeping an open stream of data.  

