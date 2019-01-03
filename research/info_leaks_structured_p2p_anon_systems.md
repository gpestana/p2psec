## Information Leaks in Structured Peer-to-Peer Anonymous Communication Systems
**Prateek Mittal, Nikita Borisov** [2012]

**what**
**results**
**importance**

**metadata leaks**: information and metadata leaks can be used to de-anonymise users in P2P networks. thus, not only active attacks should be considered in the P2P context. metadata leaks about user behavior are an important part of the anonymity in p2p systems and must be properly researched and implemented.

**active/passive attacks tension**: mechanisms to protect p2p systems from active attacks will increase the passive attacks surface because of the information/metadata leaks such mechanisms have. due to this tension, when employing naive mechanisms to protect the network against active attack, may result on a relatively small fraction of malicious nodes that "can  act as a near-global passive adversary and compromise the security of anonymous communication systems".

**threat model**: the authors consider adversaries capable of launching passive and active attacks, who controls a fraction f of the network but cannot create and position nodes in the network at will. based on Raymond (see below), the adversary is active, internal and static.

**dht lookups vulnerable**: DHT lookups are extremely vulnerable to attacks on the lookup mechanism (both active and passive). The four main attack vectors are: a) Sybil attacks; b) lookup request interception and forged responses in order for malicious nodes to be resolved as lookup target and c) malicious nodes biasing routing tables of peers in the network so that malicious nodes are requested as many times as possible, so that lookup target inference is made easier; d) listening and correlating network requests.

**Castro, et al. secure lookup mechanisms**: these mechanisms aim at ensuring that the lookup response returns the actual closest node to the target. the downsides of these mechanisms are relying on central authority (PKI) and large information leaked which makes it easier to de-anonymise lookup initiators.

- *secure node ID assignment*: (Castro et al.) each node is issued a certificate controlled by a PKI which limits the amount of issued certs.
- *secure routing table maintenance*
- *secure lookups/message forwarding*: redundancy so that at least one message path is forwarded by a chain of honest peers 



---

- redundant paths in p2p networks leaks same information to more peers. the more redundancy, the easiest it is for peers in the network to act as (near) passive global adversaries.

- metric idea: what is the percentage of colluding adversaries needed for de-anonymising an user? or, what is the computational power required for an attacker to de-anonimize a subset of users? 

- Threat modeling: J.-F. Raymond. Traffic analysis: Protocols, attacks, design issues, and open problems. In Federrath [20], pages 10–29.

- Active attack security M. Castro, P. Druschel, A. Ganesh, A. Rowstron, and
D. S. Wallach. Secure routing for structured peer-to-peer overlay networks. In D. Culler and P. Druschel, editors, Symposium on Operating Systems Design and Implementation, pages 299–314. USENIX, Dec. 2002