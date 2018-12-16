## Systematizing Decentralization and Privacy: Lessons from 15 years of Research
and Deployments
**Carmela Troncoso, Matio Isaakidis, George Danezis, HArry Halpin**

**what**:
**results**
**importance**

**interesting question:**: "is being vulnerable to a (possibly random) subset of
decentralized authorities better than being vulnerable to a single centralized
authority?"

**interdisciplinarity**: working on decentralized technologies require a broad
perspective of different areas: expertise in distributed systems, advanced
cryptography and economical and social behavior (game theory, incentives, etc)

**design assumptions**: it is important that assumptions about the network and
	environment are credible and realistic while designing decentralized
protocols. Abstract and over-optimistic assumptions will lead to protocols which
will fail to provide the scalability, privacy, security and incentives for the
network to be successful.

**decentralization and privacy**:
- naive decentralized systems can harm privacy. Distributing trust and
  exchanging information between peers may leak a lot of information about
user's behavior and increase the attack surface, rather than decreasing it.
- decentralization must use advanced cryptography to ensure that privacy,
  availability and integrity are achieved.
- most of real-world decentralized networks do not implement any mechanism to
  protect user privacy.

**problems with decentralization**:
- attack surface is often larger than in centralized systems, with both external
  and internal adversaries;
- traffic analysis is easier in decentralized networks, since peers are
  responsible to route messages.
- nodes have a partial, non-consistent view of the network, making it harder to
  detect adversary nodes and attacks
- routing complexity
- reputation and accountability systems are hard to build and maintain in P2P
  networks
- poor incentives. Without reputation it becomes hard to punish and reward peers
  in the network based on their behavior.

**open research problems**:
- establishing (and managing) reputation without relying in centralized services
- Sybil attacks on open and dynamic decentralized networks (social network vs
  proof of work vs ..?)
- improving scalability: inefficient decentralized networks will make adoption 
  harder
- how to better incentive peers in decentralized networks?
- how to systematically evaluate decentralized protocols in terms of its security,
  privacy, scalability, integrity, decentralization degree, etc..

**open development problems**:
- over simplified models used as starting point to design and build
  decentralized systems
- user-facing infrastructure (e.g. authentication)
- cutting-edge protocols and mechanisms for protecting user's privacy and
  security in decentralized networks haven't been implemented yet and remain as
academical theoretical solutions.
