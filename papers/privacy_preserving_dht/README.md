## Privacy Preserving Distributed Hash Tables - Reality and Future 

![Version](https://img.shields.io/badge/version-draft%20in%20progress%20%200.1-blue.svg?style=for-the-badge)

**note**: The current version of the paper is a draft and being review and
modified. This is an open research work: feel free to contribute with ideas,
corrections and content. This work is supported by [hashmatter](https://hashmatter.com).

**Abstract** Distributed Hash Tables (DHT) are overlay networks that enable peers to store
and request data in a peer-to-peer (P2P) network. Peers are responsible for
storing data and for participating in the lookup and routing protocol. A DHT
does not require peers to have a complete view of the network and does not rely
on central authorities, resulting on resilient, scalable a decentralized
networks. DHTs are an important building block for the decentralized web and
many P2P systems. However, the decentralized nature of DHTs introduces privacy
vulnerabilities to the services built on top of it: in naive implementations of
decentralized networks users potentially disclose private data and metadata to
many untrusted parties. In this paper we review the literature of mechanisms and
protocols to achieve privacy preserving DHTs and their vulnerabilities. Finally
we outline open problems and directions for future research.

---

The core of the paper is a literature review of research work on protocols and
mechanisms for enhancing privacy in DHTs and its vulnerabilities. Currently, the 
literature section is organized as follow: 

**Privacy preserving DHTs: protocols and mechanisms**

*A. Privacy preserving DHT lookups*
- Octopus: A Secure and Anonymous DHT Lookup
- Adding Query Privacy to Robust DHTs 
- Design of PriServ, a privacy service for DHTs

*B. DHTs in anonymous communication systems*
- Scalable Onion Routing with Torsk
- Bifrost : A Novel Anonymous Communication System with DHT

*C. Privacy mechanisms in P2P networks*
- HORNET: High-speed Onion Routing at the Network Layer
- NISAN: Network Information Service for Anonymization Networks
- ShadowWalker: Peer-to-peer Anonymous Communication Using Redundant Structured Topologies
- TAP: A Novel Tunneling Approach for Anonymity in Structured P2P Systems

**Privacy vulnerabilities of DHTs**

- Security Considerations for Peer-to-Peer Distributed Hash Tables
- Hashing it out in public: common failure modes of DHT-based anonymity schemes
- Routing in the Dark: Pitch Black
- Information Leaks in Structured Peer-to-peer Anonymous Communication Systems
- In Search of an Anonymous and Secure Lookup: Attacks on Structured Peer-to-peer Anonymous Communication Systems
- Information leak in the Chord lookup protocol

The paper wraps up outlining future work and research directions.

## Contribute

This is an open research work. Feel free to contribute with ideas, content,
corrections or to fork it.

**Edit and generate the PDF**: The paper is written in Markdown ([privacy_preserving_dht.md](./privacy_preserving_dht.md)) and the Latex PDF file is generated using `pandoc` and `bibtex` ([privacy_preserving_dht.bib](./privacy_preserving_dht.bib)). To generate the final PDF, use the Makefile steps.

<br><br>

MIT License

Copyright (c) [2018] [Goncalo Pestana - hashmatter]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
