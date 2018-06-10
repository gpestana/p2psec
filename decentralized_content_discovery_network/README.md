## Decentralized content discovery network

This repo keeps a set of technical docs trying to answer the question "What does it
take to build a decentralized, P2P content discovery network?". A content
discovery network is a generalization of a search engine, in which peers in the
network index, process, subscribe, publish and request web content metadata.

--- 

### The problem

> TL;DR: new protocols will inevitably scatter online content
> across different networks with different communication protocols. current
> search index engines are not the answer for content discovery in multiple
> networks.

With the upcoming avalanche of new protocols, p2p and decentralized networks 
coming to life, data will be more scattered than ever. Networks of users 
communicating and collaborating using protocols other than HTTP are destined to
become the norm. Although HTTP and the current centralized web will not be
replaced, many different networks communicating using different protocols will 
live and strive alongside, each of them supporting and solving specific use cases for
different communities. Over the years, the data storage and computation in the
web developed to become centralized at its core. The HTTP protocol enables users
and servers to communicate and for users to request storage and computation
power from (ever more) centralized systems. 

Data is already being stored and replicated across many decentralized and centralized
systems which are accessible through their own protocols and network primitives.
Networks and protocols such as [IPFS](ipfs.io), [DAT](https://datproject.org/) 
and [Scuttlebutt](https://www.scuttlebutt.nz) are just examples of self 
contained and dynamic communities that are already generating and storing 
considerable volumes of data.

Although limitative in its features and 
architecture, the simplicity and widely adoption of the HTTP protocol allowed 
web content to be relatively easy to index and discover. Search engines are 
sitting on top of huge amounts of indexed web data dues to the huge amounts of
computation power companies like google have put into crawling and indexing HTTP
based websites and because the web content is often served and accessible using 
a common protocol - HTTP.. But with the new ecosystem boom where multiple 
protocols - not necessarily compatible - are the basis for active and dynamic 
networks, are the traditional search engines the right answer for content and
peer discovery online?

We argue it is not, and we need a protocol and network which solves content
and connectivity discovery for the upcoming web and public networks.

### The solution

We propose a p2p decentralized protocol which enables peers to discover content
metadata online. The content itself is not stored nor shared in the network. The
protocol only offers a mechanism for peers to request, subscribe and publish
metadata of content stored in different networks.

## Protocol anti-principles

What the protocol is not:

- **Blockchain**: at least for now. This is not a project aiming at leveraging
  the ICO frenzy. We aim at building an easy and cross network protocol for
discovering content. However, if in the future there is a good reason to use 
blockchain to achieve our goals, we'll use it.

- **google**: we are not replacing google or any other current search engine.
  However, search engines would benefit from participating in the network as 
peers to serve users.

- **Content delivery P2P network**: the protocol aims at content discovery
  stored in multiple centralized or decentralized netoworks. The protocol allows
peers to communicate with each other to query, subscribe and publish metadata
about online content.

### Protocol principles

- **Metadada discovery oriented**: the protocol facilitates peers to query,
  subscribe and publish online content metadata from several networks.

- **Decentralized and P2P**: all peers in the network are feature-full and may
  query and reply to queries from other peers.

- **Embeeded trust mechanisms**

- **Easy and robust anonymity**: strong anonymity should be either embedded in
  the protocol or relatively easy to setup.


### Research and specs

[Computation verification](./computation_verification.md)

[Reputation](./reputation.md)

[Transport](./transport.md)

[Client layer](./client_layer.md)

[Pubsub](./pubsub.md)

[Data mode](./data_model.md)

[Privacy](./privacy.md)

[Identity](./identity.md)

[Peer discovery](./peer_discovery.md)
