## Information Leaks in Structured Peer-to-Peer Anonymous Communication Systems
**Prateek Mittal, Nikita Borisov** [2012]

**what**: security and privacy in p2p anonymous communication systems (AP3 and Salsa) are studied with emphasis on the tension between security and privacy: often, mechanisms that ensure security in p2p systems (e.g. redundancy) end up affecting privacy by leaking more information.

**results**: AP3 and Salsa are more vulnerable to passive and active attacks than previously thought. 

**importance**: p2p anonymous communication systems are hard to design and implement. this research also shows how putting together provable secure and anonymous primitives may result on weak systems: the sum of secure parts may end up being a not-as-secure result. abstracting away parts of the p2p network often results in insecure systems.

---

**metadata leaks**: information and metadata leaks can be used to de-anonymise users in P2P networks. thus, not only active attacks should be considered in the P2P context. metadata leaks about user behavior are an important part of the anonymity in p2p systems and must be properly researched and implemented.

**active/passive attacks tension**: mechanisms to protect p2p systems from active attacks will increase the passive attacks surface because of the information/metadata leaks such mechanisms have. due to this tension, when employing naive mechanisms to protect the network against active attack, may result on a relatively small fraction of malicious nodes that "can act as a near-global passive adversary and compromise the security of anonymous communication systems".

**threat model**: the authors consider adversaries capable of launching passive and active attacks, who controls a fraction f of the network but cannot create and position nodes in the network at will. based on Raymond (see below), the adversary is active, internal and static.

**dht lookups vulnerable**: DHT lookups are extremely vulnerable to attacks on the lookup mechanism (both active and passive). The four main attack vectors are: a) Sybil attacks; b) lookup request interception and forged responses in order for malicious nodes to be resolved as lookup target and c) malicious nodes biasing routing tables of peers in the network so that malicious nodes are requested as many times as possible, so that lookup target inference is made easier; d) listening and correlating network requests.

**Castro, et al. secure lookup mechanisms**: these mechanisms aim at ensuring that the lookup response returns the actual closest node to the target. the downsides of these mechanisms are relying on central authority (PKI) and large information leaked which makes it easier to de-anonymise lookup initiators.

- *secure node ID assignment*: (Castro et al.) each node is issued a certificate controlled by a PKI which limits the amount of issued certs.
- *secure routing table maintenance*
- *secure lookups/message forwarding*: redundancy so that at least one message path is forwarded by a chain of honest peers 


**Salsa**: node ID is hash of the IP address; a node maintains routing information of local contacts and some routing information to other groups and performs the routing recursively. Salsa uses adapted routing to hide the lookup initiator and the path during the lookup.

- *defense against lookup poisoning*: redundant routing and bounds checks to reduce the lookup bias, making it necessary for an adversary to intercept all the redundant requests and control a node within the bound interval.
	- bound check: nodes that lay outside an interval of the target are discarded
	- redundant queries using paths with reduced probability of overlapping 
	- increasing the number of redundant paths decrease the number of compromised lookup requests, making it more secure. however, more redundant paths increase the privacy attack surface (more information is leaked about the initiator). thus, decreasing the active attacks surface increases the privacy vulnerability surface.
 - *lookup path building*: Salsa uses the bound checks and redundant checks to build a path for anonymous lookups. it first selects a set of nodes which will act as proxy to find other set of nodes. these nodes are communicate through layered encryption, ensuring that a node only knows about the previous hop in the path (similar to onion routing). once the path is established, the initiator instructs the final layer of nodes to perform the lookup (through the path built).  
		- path building bias: active attacks can be performed in order to increase probability that compromised nodes are part of the path. path compromising attacks are possible if the first and last node are compromised - allowing for timing attacks. increasing the number of hops decreases the change of these attacks (why?).
		- passive attacks: 1) initiator performs redundant lookups for the nodes in the first stage. thus, if the attacker detects redundant lookup up requests, the anonymity of the systems is compromised; 2) when adversary nodes are part of the path with honest nodes in between.


**AP3**: p2p anonymous system built on Pastry, where a random walk over all walks in the system is used to forward requests, while the lookup initiator identity is hidden. it is hard for request routers in the path to know whether the previous node is an initiator or another relay (i.e whether the lookup initiator can be identified.)
 - *selecting relays and info leaks*: AP3 uses Castro, et al. secure lookup to pick random relays in the network. note that nodes have only a partial view of the network for scalability purposes (different for Tor approach). however, the secure lookup breaks anonymity.
 - *observing chain of requests*: in a chain of requests, adversaries are able to guess that the lookup initiator is `I` if they did not observe any request to `I` - this means that the request was initiated by `I`. the probability for this to happen depends on the current traffic of the network. the bigger amount of traffic, the higher the entropy is and thus harder to find `I` through this mechanism. 

**the perils of design abstraction**: anonymity design is not cumulative, i.e., if system A and B are secure and anonymous, putting both together may not be as secure and anonymous. thus, system design must take this property into consideration.

---

- redundant paths in p2p networks leaks same information to more peers. the more redundancy, the easiest it is for peers in the network to act as (near) passive global adversaries.

- metric idea: what is the percentage of colluding adversaries needed for de-anonymising an user? or, what is the computational power required for an attacker to de-anonimize a subset of users? 

- Threat modeling: J.-F. Raymond. Traffic analysis: Protocols, attacks, design issues, and open problems. In Federrath [20], pages 10–29.

- Active attack security M. Castro, P. Druschel, A. Ganesh, A. Rowstron, and
D. S. Wallach. Secure routing for structured peer-to-peer overlay networks. In D. Culler and P. Druschel, editors, Symposium on Operating Systems Design and Implementation, pages 299–314. USENIX, Dec. 2002

- entropy metric of anonymity: 
	- C. Diaz, S. Seys, J. Claessens, and B. Preneel. Towards measuring anonymity. In Dingledine and Syverson [17], pages 184–188.
	- A. Serjantov and G. Danezis. Towards an information theoretic metric for anonymity. In Dingledine and Syverson [17].

- N. Borisov. Anonymous Routing in Structured Peer-to-Peer Overlays. PhD thesis, UC Berkeley, May 2005.