## TARANETL Traffic-Analysis Resistant Anonymity at the Network layer
**Chen Chen, et al.**

**what**: TARANET is an anonymous system that implements protection against 
traffic analysis at a network layer with low overhead and high performance. the
main goal is to create a system in which aims at optimizing anonymity and
performance. TARANET achieves better performance and anonymity by leveraging
network-level end-to-end traffic shaping assisted by packet splitting techniques

**results**: efficient end-to-end traffic shaping technique which defeats
traffic analysis; onion routing protocol that enables integrity protection,
replay protection and splittable paclets; design, implement and evaluate TARANET

**importance**

**network layer anonymity (NLA)**: network-layer anonymity relies on Autonomous
Systems (AS) to collaboratively hide the package forwarding paths. NLA is not
secure against compromised first-hops and last-hops and as such, the systems
offers relationship anonymity. besides anonymity, the NLA systems focus on
performance and scalability by limiting the state kept on network routers.

**end-tp-end traffic shaping**: 

**overlay networks vs network layer anonymity**: overlay networks that provide
anonymity are often not performant to real-time use cases (e.g. Tor). p2p
anonymous networks and mix-networks have high latencies and are not reliable.
network layer anonymity systems attempt at solving those problems.


