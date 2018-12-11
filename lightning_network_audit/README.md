## Lightening Network

Lightening network (LN) is a P2P network which allow peers to create and maintain
directional micro payment channels between each other. Channels are secure - it
is possible to exchange locked funds without need for network consensus 
(through, e.g. blockchain transactions) - and allow secure payment channels 
without trust.

When both parties are happy with the exchange of value in a payment channel, 
they can close the channel. Closing a channel commits the micropayment value 
exchange to the main blockchain.

LN also allows payments to be routed through many channels. If peer A maintains
a channel with peer B which in turn maintains a channel with peer 
`(A <--> B <--> C)`, it is possible for peers A and C to use an indirect payment
path to exchange payments without the need for setting up a direct channel
between A and C.

### Network layer

**source routing**: peers use [source routing](https://en.wikipedia.org/wiki/Source_routing) to
set up payments paths in the network; this gives nodes full control of how
their payments are routed through the network when using payment paths (max
hops, max tx fees, etc);

**privacy preserving properties** onion routing using adapted sphinx packet
format is used to provide the following privacy preserving properties:
	- hide payment source and destination in all hops of the network;
	- hide path location from relay peers;
	- hide path structure from relay peers;
	- payment paths are indistinguishable from each other;

These properties help to anonymize payment paths and channels. This privacy 
preserving property mitigate censorship in the network - peer relays do not know
which payments they are relaying and the fees incentives relays to participate in
payment routing. Moreover, it provides peer unlikeability of channel peers.

**HORNET routing**: there are plans to use HONET [1] onion routing protocol in 
the future.

### Investigate

- [ ] What is the mechanism for peers to discover paths and relay peers?

Path set up is a critical step in onion routing protocols. When setting up
the onion path, peers should not leak any information about what is the chosen
route (i.e. onion relays), since knowing first and last relay de anonymizes the 
onion circuit by allowing easy timing-attacks at the edges.

Tor solves this problem by providing all peers
the current view of the relay pool and providing metrics about each relay
(health, bandwidth, etc..). This information is stored in a central authority 
directory. By providing the same information about the relays for every peer 
prior to path relay definition and let peers to locally decide which relays to
use, it is hard for a passive attacker to know which onion path is going to be
used.

- [ ] Is minimum set of hops defined in the code? Does this even matter in this
  case?

- [ ] Is network secure against passive network adversaries?

- [ ] Entropy in LN network 

### References

[1] [HORNET](https://www.scion-architecture.net/pdf/2015-HORNET.pdf)
