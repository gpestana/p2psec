## Eclipse and Re-Emergence of Anonymous P2P Storage Network Overlay Services
**Marios Isaakidis, George Danezis**

**what**
brief description of the key features of anonymous P2P storage networks and
showcase of overlay application currently in use (CENO). CENO is a distributed
censorship resistance service on top of Freenet.

**results**

**importance**

**possible properties for a p2p storage oerlay service**: 1) anonymity for
producers; 2) anonymity for consumers; 3) plausible deniability of the files
hosted in the network nodes; 4) high availability; 5) persistence.

**p2p storage services and censorship**: p2p storage overlay services are
resilient to censorship since there are no central/special nodes in which the
network depends on and data may be replicated to many nodes.

**signed subspaces**: by applying pubkey crypto techniques, signed spaces may be
created so that only owner of private key can insert and update information in
the p2p network.

**content indexing/discovery**: lack of centralized services makes it harder to
process keyword storages. indexing has to be performed locally with costs.

**spam in p2p networks**: many freenet overlay services leverage the web of
trust model in which peers share trust scores to their trusted peers. the trust
scores of a peer web of trust are used to avoid spammers and allow trusted peers
to communicate

**CENO and the freenet overlay**: CENO relied on freenet to cache and distribute
content anonymously and in many geographical locations, making it a good scheme
for circumventing censorship. when content is stored in freenet through
`bridges`, it will be automatically replicated and stored anonymously. content
consumers can access the content through freenet client anonymously and in case
of censorship, peers can circumvent it if the content is cached in hosts
geographically not blocked by the government.

