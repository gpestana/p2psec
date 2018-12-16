## Scalable Anonymous Communication with Provable Securitys
**Prateek Mittal, Nikita Borisov, Carmela Troncoso, Alfredo Rial**

**what**: the study proposes two new primitives for scalable, anonymous communication with (theoretically) provable security. 1) P2P based system based on neighbor policies for achieving anonymity; 2) client-server PIR (private information retrieval) system;

**results**: reciprocal neighbor policy nullifies adversarial advantage for short random walks;

**importance**: in particular, Tor users need to maintain a global view of the system to chose the relays from the available nodes. This is not scalable as the size of the system grows;

**Tor and the relay directory**: McLachlan et al. [1] predict that in the future, Tor network may be spending an order of magnitude more bandwidth maintaining the global view of the system than in the anonymous communication itself;

**heuristic anonymity vs provable anonymity**: heuristic anonymity is not enough for designing anonymous systems. Q: How to show provable anonymity in the communication context? 

**scalability and P2P**: scalability may not necessarily mean P2P networks. PIR systems are not P2P but may offer good privacy and reasonable scaling.

### reciprocal neighbor policy

**goal**: route capture attacks - when malicious node lies about its finger tables in order for the honest node to build circuit with malicious, colliding nodes - will eventually isolate malicious nodes in the network topology, thus reducing the probability malicious nodes are selected in the circuit building.

**how**: honest node A notices that malicious node M is not broadcasting its own address as it should. node A removes malicious node M from its own finger table. This strategy isolates the malicious nodes in the network topology; 

**provable security**: a random walk is used to select nodes for building the onion circuit. At a certain point in time, a random walk is done either at a malicious or honest surface. The transitions from malicious to honest area is modeled as a Markov chain, with its given probabilities (related to Q1). It is shown that given this system, the reciprocal neighbor policy nullifies adversarial advantage for short random walks;

**securing reciprocal neighbor policy**:
// 1. why isn't it secure?
// 2. how to secure (in p2p fashion)

--- 

[1] MCLACHLAN, J., TRAN, A., HOPPER, N., AND KIM, Y. Scalable onion
routing with torsk. ACM CCS (November 2009).


**Q1**: how did they come up with the probability functions user for the Markov chain state transitions?