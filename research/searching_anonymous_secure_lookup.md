## In Search of an Anonymous and Secure Lookup
**Qiyan Wang, et al.**

**what**: this work explores anonymity vulnerabilities in Torsk and NISAN P2P
anonymity systems.

**results**: attacks describes reduce significantly anonymity of NISAN and Torsk
with only 20% of compromised nodes. Techniques to overcome the vulnerabilities
are explained. 

**importance**: anonymous P2P networks are important in the era of pervasive
surveillance. This work explores the attack surface of state-of-art P2P
networks - Torsk and NISSAN - and suggests techniques to overcome the
vulnerabilities.

**design categories of low-latency anonymous P2P systems**: 1) Random walks on 
restricted topologies to find relays (e.g. Tarzan, Morphmix, ShadowWalker) and
2) DHT lookups to select tandom relays (Salsa, AP3, NISAN, Torsk).

**threat model**: passive and active attacks performed by a partial adversary
which controls a static percentage of the nodes. The nodes controlled by the
adversary may collude with each other and amount to 20% of the networks (P2P
networks are not designed to resist attackers which control more [why?])

**Torsk lookup**: based on Kademlia DHT and Myrmic, its main goal is to resist
active attacks. Lookup is split in parallel, independent lookup branches
(usually t=3). The lookup node maintains a list with the closest peers to the
destination and asks recursively to those in the list who were not asked yet.
The list is updated when new addresses are received, if the new received
addresses are closer that the ones existing. The lookup stops when there are no
new nodes added to the list and all nodes have provided their closest. To resist
active attacks (e.g. nodes modifying their finger tables or providing malicious
nodes as response), each node keeps a certificate issued by a trusted cert 
authority. The certs are used to ensure that the final node is the one
responsible for the lookup address.

**Torsk lookup leaks**: since the lookup key is revealed to each queried node, 
if an adversary node is part of the queried path, it will get information about
which address the lookup initiator is looking for.  

**NISAN lookup**: based on Chord DHT, its main gola is to preserve anonymity.
The querier node keeps a list (TopList) with the closest fingers to the final queried ID.
At each iteration, it asks for all the finger table to the peers in the TopList
(effectively hiding the final address from potential passive attackers). The
process stops when the TopList is not updated at the end of one iteration. To
limit the capacity of an adversary to provide wrong finger tables, the querier
calculates the distance between the nodes received in the finger table and the
optimal finger. If the distance is bigger than a certain threshold, the result
is discarded (making it hard for an attacker to meaningfully forge node IDs which
would be accepted).

**passive attacks NISAN lookup**:

**Further reading**

- A. Panchenko, S. Richter, and A. Rache. Nisan:
Network information service for anonymization
networks. ACM CCS, November 2009.
- J. McLachlan, A. Tran, N. Hopper, and Y. Kim.
Scalable onion routing with torsk. ACM CCS,
November 2009.
- P. Mittal and N. Borisov. Infomation leaks in
structured peer-to-peer anonymous communication
systems. ACM CCS, 2008.
- P. Wang, I. Osipkov, N. Hopper, and Y. Kim. Myrmic:
Secure and robust dht routing. Tech. Rep. Univerity of
Minnesota DTC Research Report, 2006.

