## inference attacks on peer-assisted CDNs

### abstract
Content Distribution Networks consist of edge data centers that cache content in
different geographical locations in order to provide redundancy and better
content distribution performance. With the increase of real time data such as
video streaming and the increasing of users requesting content, CDNs which are
relying on dedicated servers do not scale well. Peer-assisted CDNs (pCDN) solve this
problem by leveraging peers that received content to behave as relay of content
to peers close geographically. pCDNs turn peers into caching nodes and make it
cheaper for CDNs to scale and achieve better performances. If the pCDN protocol
is developed naively and given the P2P nature
of pCDNs, peers delivering and requesting data in the pCDN P2P network may be 
able to gather information that correlates IP addresses with online accessed
content. This information can pose a critical threat to online privacy. The goal
of this work is to perform inference attacks on deployed peer-assisted CDNs.


### hypothesis
It is relatively easy and cheap to gather critical and private data of users 
using peer-assisted CDNs, which can be used to infer user behavior.

### reckon
In order to test the hypothesis, we need to know which services are using a
peer-assisted CDN network in order to perform the attack.

### peer-assisted CDNs:
- [viblast](https://viblast.com)
- [teleport](https://teleport.media/)
- [peer5](https://www.peer5.com/)

### deliverables
- database dump which correlate IPs with content and timestamps in different pCDN.
- scripts which automate gathering of metadata while serving/requesting content
- reach out: blog post, paper, talk 

### literature
-  Anonymity in Peer-assisted CDNs: Inference Attacks and Mitigation
