# Sybil Control: Practical Sybil Defense with Computational Puzzles

- Distributed systems are subject to Sybil attack, where adversary creates and
  maintains	multiple nodes to acquire disproportionate weight in the network;

- SybilControl: decentralized scheme for controlling the upper bounds of the
  Sybil attack by making it harder - expensive - for attacker to run many nodes;

- SybilControl prevents the attacker to gain too much network influence by
  requiring nodes joining the network to compute proof-of-work; Existent nodes
may also be asked to compute the proof-of-work randomly (recurring proof or
work)

- The proof-of-work is required to make sure it is expensive for attackers to
  maintain too many valid nodes in the network;

- It's shown that the SybilControl scheme has low overhead and latency;

--

SybilControl does not prevent adversaries from joining the network, but rather
place an upper bound on the number of adversarial nodes from the same entity.
SybilControl provides a distributed way for nodes to verify that each other node
is 'paying' their computational costs to be part of the network.

For scalability purposes, nodes only challenge neighbor nodes. The challenge
of a node receives as an input the 'cryptographic aggregation' of all the
challenge responses it received thus far (it can be time bound). This way, the
challenge responses are propagated over the network in a gossip manner, allowing
to multi-hop proof of work verification.

Honest nodes do not accept work performed by nodes that cannot provide the proof
of concept. These nodes are considered adversaries.

Ping messages between nodes are a convenient way to carry challenges - since
they are usually regularly by nodes in P2P networks to ensure neighbors are
running.

A challenge hash comprises all concatenated challenges received from neighbor 
nodes and their identifiers, as well as the old node challenge. This way it the
challenges are propagated throughout the network, even though the gossip is
1-hop only.

```
Challenge[new] = Hash(NodeA_challenge || .. || NodeM_challenge || Challenge[old])
```

Protection mechanisms for honest nodes presented are against 3 different cases:
protecting against consistently unverifiable Sybils; protecting against
initially verifiable Sybils; and protection against consistently verifiable
Sybils;

The protection against consistently unverifiable Sybils consists on only
accepting new nodes as valid neighbors when these have resolved at least one
challenge upon joining the network. To avoid issues with node join latency in
churn-handling sensitive networks, the nodes keep an log of untrusted nodes
which haven't resolved any challenge yet. This makes it faster for a new node
which to establish the communication with other nodes upon resolving its first
challenge, while still not allowing non-valid nodes to influence the network.

 


## Notes/comments
