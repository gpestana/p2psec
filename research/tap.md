## TAP: A Novel Tunneling Approach for Anonymity in Structured P2P Systems
**Yingwu Zhu, Yiming Hu**

**what**: TAP is a tunneling approach for anonymity in structured P2P networks, with secure, replicated and fault-tolerant channels relying on the P2P structure.  

**results**: 

**importance**: TAP decouples anonymous circuits from fixed nodes, which means that maintaining secure paths will not stop functioning when relays leave the network. TAP helps building secure circuits in P2P networks which are robust against churn.

---

**approach to P2P anonymity**: in P2P privacy preserving networks (e.g. Crowds, Tor, Tarzan), message-identity unlikeability is achieved by routing messages through anonymous paths involving a randomly chosen sequence of network nodes.

**a problem with privacy preserving P2P relaying systems**: is the instability of the paths created: when relays leave the network, the secure circuit created will not work anymore.

**security considerations**: 
- attack surface increase: the replication of the tunnel hop information increases the attack surface for adversaries which control large numbers of colluding nodes to compromise anonymity. The authors argue that TAP aims at creating a balance between anonymity and reliability and it does not aim at perfect anonymity.
- DoS attacks: attackers may perform a denial of service attack by flooding the network with THAs so that new THAs cannot be installed. This can be avoided by requiring computational expensive challenges before installing THAs in order to limit the capacity of Dos attacks.

**tunnel hop anchor**: (THA) is the data structure with the information necessary for a node to function as a tunnel relay. A THA as a form of `<hop_ID, K, Hash(password)>`. The `hop_ID` uniquely identifies the tunnel hop and functions as a DHT key; the K is a symmetric key for encryption/decryption and `Hash(password)` is the hash of the password to control the tunnel. 

**bootstrapping THAs**: in order to deploy the first TAP tunnel anonymously, the initiator may use onion routing where each relay stores the THA used later on for the message tunneling. The onion routing only needs to be used once, since if there is a TAP tunneling in place, it can be used to deploy other THAs (and TAP tunnels) if needed.

**deleting THAs**: nodes maintaining THAs keep an hashed password per THA. The only node who knows the password is the tunnel owner (e.g. the initiator). The tunnel initiator can ask relays to delete the THA upon providing the password that match the hash (note: THAs could probably have timestamps TTL to avoid lingering tunnels)

---

