## Octopus: A Secure and Anonymous DHT Lookup
**Qiyan Wang, Nikita Borisov**

**what**: octopus is a DHT lookup technique which solves the security and
privacy vulnerabilities of DHTs by using attacker identification techniques
(less effective attacks), splitting lookups over separate anonymous paths
(better anonymity) and by using dummy queries (better anonymity).

**results**: a lookup protocol for DHTs which provides strong guarantees for
anonymity and security, where malicious nodes are quickly identified with high
accuracy. Octopus can also achieve near-optimal anonymity for both lookup
initiator and target (shown through probabilistic modeling and simulation). All
this with reasonable latency and communication overhead.

**importance**: many p2p applications rely on DHTs (IPFS, freenet, bittorrent,
etc..) because of their decentralized nature, a lot of information and metadata
is leaked by users of the DHT - both for users who lookup content in the DHT as
well as those who serve content. In such p2p networks, it is important to
identify attacker nodes and provide a strong layer of anonymity to its users. 

**threat model**: not consider a global adversity that is capable of controlling
the whole network and observing all communication traffic (unpractical in large
networks?). Assumes partial adversaries that can control up to 20% of the
network. Adversaries are able to intercept, log, modify and drop messages of the
network. Sybil attacks are not considered.

**security and anonymity in DHTs**: a certain degree of security is needed for
achieving anonymity in DHTs

**security and anonymity goals**: security: the most important goal for security
 is that lookup messages are not biased (dropped/modified/...) by adversaries;
anonymity: 1) not possible to determine who sent a specific DHT lookup message;
2) given a lookup initiator, it should not be possible to determine the target
of the lookup; 3) several queries cannot be correlated to find out information
about it.

**possible attacks**
- lookup misdirection attack: adversary returns a routing table filled with only
  adversary's controlled malicious nodes. This will allow the adversary to
learn by fine tuning which is the target node.
- finger pollution attack: when responding to routing table query updates, a
  malicious node may try to poison other node's routing table.

**trust model and malicious nodes punishment**: octopus rely on a centralized
certificate authority to issue and revoke certificates from nodes. Identified
malicious nodes have their certs revoked. The certificates are independent from
lookup queries. Merkle Hash Tree certificate revocation and other solution may
be used ny the CA.

**security mechanisms**: nodes (secretly) check other nodes' routing tables
(finger tables and predecessor/successor lists)  independently of the lookup 
process. 
- A trust/punishment system that issues
certificates is used to signal malicious nodes. Certificate management can be
done with e.g. Merkle Hash Tree based certificate revocation.
- anonymous lookup routing: nodeA can connect to nodeB through a series of
  relays, while protecting the contents of the message using onion encryption.

In summary:

- secret neighbor surveillance: to prevent lookup bias attacks, nodes check each
  other successor list anonymously. If a node is caught changing their successor
list, it is flagged as malicious (in the paper's example, through the
certification mechanism). Works as follows: each node contains a list of 
successor and
predecessor nodes. If nodeA successor list contains nodeB, then nodeB
predecessor list contains nodeA. nodeB can check if nodeA is performing a lookup
bias attack by anonymously asking nodeA for its routing table. If nodeB is not
there, it means the routing table as been manipulated.

- secret finger table surveillance: to prevent the lookup misdirection attack
	(*and attacks agains finger table updates),
the node keeps a buffer with received finger tables. Periodically, it will
select one finger node from a random finger table buffered (belonging to node 
F')  and request its predecessor list. If any node in the received finger table 
is closer that the original F', then the finger table has been manipulated,
since F' knows some node which is closer to ID but keeps other finger node
(potentially malicious). 

**metrics to evaluate security mechanisms**: octopus DHT maintains a reputation
system based on a centralized CA. The metrics to evaluate the security
mechanisms intend to understand how successful flagging malicious nodes in the
network is. Metrics are: 1) fraction of malicious nodes in the network 
(effectiveness) 2) false positive rate - e.g. honest node is flagged as malicious
(accuracy) ; 3) false alarm rate (efficiency)

**experimental results secure mechanisms**:
- secret neighbor surveillance mechanism can rapidly identify malicious nodes;
- secret finger surveillance mechanism is slower, but it identifies 80% of
  malicious nodes in 30m;
- false positive rate is close to 0 (almost no honest node will be flagged as 
malicious)
- over time, a malicious node will be identified with probability 

**anonymity mechanisms**: Octopus DHT considers only passive attackers - since
active attackers are removed from the system through the security mechanisms.
- construction of anonymity paths to send lookup queries while hiding the
  initiator
- splits individual queries over multiple (anonymous) paths
- dummy queries for adversaries to lean the lookup target

### Questions
- threat model considers partial adversaries that control up to 20% of the
  network. Why 20%? What is the percentage that breaks the assumptions? How to
guarantee that no adversary can overcome the 20% mark? 
- [ ] "Octopus can achieve near optimal privacy for requester and server" - define
  the attack surface and examples of attacks
- [ ] How to replace the central certificate authority but have a reputation
  mechanism to flag malicious nodes? 
