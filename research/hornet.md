## HORNET: High-speed Onion Routing at the Network Layer
**Chen Chen, et al.**

**what**: system for high-speed, e2e anonymous channels at the network (router) layer. it proposes a onion routing scheme in which relays do not need to keep state of the channels - the state is carried in the payload - and studies the trade-offs between those approaches.

**results**: design and implementation of HORNET, which provides stronger anonymity that existing network-level schemes; performance of the scheme is comparable with high-end commodity routers;

**importance**: anonymous communication protocol with good performance and scalability at a network level is a great improvement to nowadays state of art and it would provide developers and users better anonymity and privacy out of the box.

---

**goals**: scalable and efficient network-level routing scheme that is secure against mass surveillance (relationship anonymity), supporting both sender anonymity or sender-receiver anonymity. the adversary should not be able to gain information from bulk traffic analysis.

**targeted de-anonymization attacks**: since HORNET aims at being low-latency communication protocol, it does not offer any protection against targeted de-anonymization, where the adversary invests resources on attacking a single or small set of victims.

**properties**: HORNET aims at the following properties:
	- *path information integrity and secrecy*: packet header cannot be changed without detection and the router cannot learn any information besides what is the next hop;
	- *no packet correlation*: adversary is not able to correlate traffic by performing bulk traffic analysis;
	- *no session linkage*: packets cannot be linked across sessions;
	- *payload secrecy and e2e integrity*: adversaries and routers cannot learn any information from packet payload (except length and timing).

**anonymous header**: (AHRD) is the packet header that is created at the session setup by the sender with information for each of the path routers to know what is the next hop the package should be forwarded to, without revealing any other info. each router has setup a symmetric key with the sender to access its segment of the header. the AHRD keeps it length at every step of the circuit.

**forward segment**: (FS) is the information segment that keep the state of the routers but it is offloaded to the edge nodes (e.g. sender). the FS is not kept in the nodes to avoid over load the routers with state information as the number of paths increase (more scalability).

**session setup**: a sender sets up a session by using SPHINX [1] to setup symmetric keys with each of the routers in the path and to obtain the FS from each router. this info will be used to construct the AHRD.

**packet structure**: there are 2 types of packets: session setup packets and data packets. session setup packets contain sphinx header and payload and FS payload. this information is used by each router in the path to setup the session keys and FS between the routers and the sender, which are included by the anonymous header. the data packets include the AHDR and data payload.

**security**:
	- *session linkage*: each session is established independently with fresh keys;
	- *forward/backward correlation*: only destination is able to correlate forward and backward traffic.
	- *packet correlation*: packet is obfuscated at each hop in the path and header and packet are padded to a fixed length.
	- *path length and node position*: neither session setup or data package leak information about path length and position of the router in the path. this is achieved with padding and obfuscation;
	- *timing attacks*: HORNET can use asymmetric paths against timing attacks.
	- *state modification*: integrity of setup and data packets is protected with HMACs.
	- *path modification*: chained per-hop MACs are used to protect path integrity;
	- *replay attacks*: to avoid replay attacks, packets have an expiration and end users/routers can use counters to detect replayed packets;
	- *payload secrecy*: payload is encrypted using shared keys;
	- *DoS*: since the routers do not need to maintain state for each communication, that DoS vector is covered, however, setting up multiple paths by attackers may be used as DoS. to mitigate this, HORNET nodes can require users to solve a puzzle before setting up the session to defend against attackers with limited resources.


**performance**: HORNET has been measured to process anonymous traffic in FIAs at over 93 GB/s without per-flow state maintenance. the most expensive (and slow) part of the protocol is the session setup, which needs to be done only once at every session.

---

- what are the modifications/improvements for using HORNET over DHTs?

1. Sphinx paper
