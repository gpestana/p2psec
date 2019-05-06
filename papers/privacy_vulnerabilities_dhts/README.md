## Privacy Vulnerabilities in Distributed Hash Tables 

![Version](https://img.shields.io/badge/version-draft%20in%20progress%20%200.1-blue.svg?style=for-the-badge)

**note**: The current version of the paper is a draft and being review and
modified. This is an open research work: feel free to contribute with ideas,
corrections and content. This work is supported by [hashmatter](https://hashmatter.com).

**Abstract** Distributed Hash Tables (DHT) are overlay networks that enable distributed nodes to store and request data in a peer-to-peer (P2P) network. Data storage and data lookups are resolved collectively through a collaborative routing protocol in a deterministic way. The collaborative nature of DHTs results on resilient, scalable and decentralized networks where nodes are not required to maintain a complete view of the network while, simultaneously, not relying on central authorities. These properties make DHTs an important building block for the decentralized web and P2P systems. However, the decentralized nature of DHTs introduces privacy vulnerabilities due to the metadata leaked during the routing and lookup protocols. In naïve DHT implementations, it is trivial for any adversary to gather information about which nodes are requesting what data and which nodes are providing what data, without being detected and with relative low resources. Nowadays, the decentralized web ecosystem is relying heavily on DHTs as networks such as IPFS and Dat are steadily reaching mainstream adoption. Thus, it is important to address privacy preserving vulnerabilities of DHTs. Failing to deliver on user privacy will render decentralized systems unattractive as a viable alternative to centralized systems.  In this paper we outline the privacy vulnerabilities of the most common DHT protocols and show how those vulnerabilities affect current implementations applications built on top of distributed hash tables.

---

The core idea of the paper is to outline the privacy vulnerabilities of DHTs and show how those vulnerabilities bubble up to current applications and protocols that rely on DHTs. We base this work on the following literature: 

**Privacy vulnerabilities of DHTs**

- Large-Scale Monitoring of DHT Traffic
- Security Considerations for Peer-to-Peer Distributed Hash Tables
- Hashing it out in public: common failure modes of DHT-based anonymity schemes
- Information Leaks in Structured Peer-to-peer Anonymous Communication Systems
- In Search of an Anonymous and Secure Lookup: Attacks on Structured Peer-to-peer Anonymous Communication Systems
- Information leak in the Chord lookup protocol

**Vulnerability in the wild**

- Routing in the Dark: Pitch Black

## Contribute

This is an open research work. Feel free to contribute with ideas, content,
corrections or to fork it.

**Edit and generate the PDF**: The paper is written in Markdown ([privacy_preserving_dht.md](./privacy_preserving_dht.md)) and the Latex PDF file is generated using `pandoc` and `bibtex` ([privacy_preserving_dht.bib](./privacy_preserving_dht.bib)). To generate the final PDF, use the Makefile steps.

<br>

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
