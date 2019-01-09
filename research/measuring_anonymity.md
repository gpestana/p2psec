## Towards measuring anonymity
**Claudia Diaz, Stefaan Seys, Joris Claessens, and Bart Preneel**

**what**: information theoretical model to quantify anonymity of network communications, based on how much information adversaries get about users and the on the probability an adversary assigns to users of the system's anonymity set. the model is applied to existent systems. the focus of the paper is to consider anonymity in mixes.

**results**:

**importance**: measuring anonymity is important as a starting point to evaluate, measure and design privacy preserving networks and it has special importance in p2p and decentralized networks

**previous work on measuring anonymity**: 
- [1] defines `1-p` to quantify how much information an attacker has about the system. `p` is the probability assigned to a particular user by the attacker. not that useful to consider the anonymity of a user within a particular set, or sets of users.
- [2] is based on a similar metric as this work without normalization.

**anonymity set**: (as of this work) is defined as set of users that send messages. these are the entities in the system we want to protect.

**attack model**: the degree of anonymity is defined based on the information an attacker gets from the users of the network, thus the anonymity measure depends on the definition of an attack (i.e attack model). in this work, the attacker may be 1) internal-external (he may control part of the network and gain information from within); 2) passive-active (carries both passive and active attacks) and 3) local-global. in this work, the attacker can carry probabilistic attacks, i.e. resolve with `probability p, A is the sender of the message`. 

**how to define anonymity**: anonymity is defined as the state of not being identifiable withing a set of subjects (the anonymity set). this work considers only sender anonymity and the anonymity is measured based on probabilities: at a certain point in time, what is the probability that an attacker is certain that a particular user is the sender of a message.

**distribution of probabilities**: the security of a systems is based on the distribution of probabilities that an attacker assigns to the anonymity set. in an optimal anonymous system, all users would have the same probability associated `1/N` (N being number of users, independent of set size).

**entropy**: for a given set of probabilities, information entropy provides a measure of the information contained in those probabilities.

**degree of anonymity**: (d) is defined as the entropy of the system after an attack (Hx) divided by the maximum entropy of the system (Hm): `d = Hx/Hm`. this metric quantifies the amount of information a system is leaking. when Hx == Hm the system is completely anonymous. as the Hx decreases (more information leaked in the system), the anonymity degree of the system decreases as well.

**minimum acceptable degree**: is proposed to be `d = 0.8`, but it depends on the anonymity requirements for the system.

**use cases**: the metric was applied to anonymity systems as a proof of concept (mix networks, crowds and Tor). the paper shows by using the anonymity metric presented that Tor is more tolerant to compromised nodes than Crowds. it also shows how to calculate the minimum anonymity set size of Tor for certain number of Tor users.    

**future work**: 
- the model is based on the probability an attacker assigns to users in an anonymity set. finding this probability not trivial for some systems;
- measure effect of dummy traffic in metric;
- take into consideration the information an attacker has a priori;
- apply metric to different systems and test it.

---

- [1] Reiter and Rubin `1-p` degree of anonymity: 
- [2] Towards an Information Theoretic Metric for Anonymity

- (ppp/p3: privacy preserving primitives catalog/book/guide)
