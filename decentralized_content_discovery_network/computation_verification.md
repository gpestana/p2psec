## Protocol for computation verification in P2P networks

A protocol for computation verification in a p2p network in which peers request 
and perform computation of a well known algorithm. The protocol is an
implementation of a result verification scheme coupled with a reputation
system, which helps to reduce the computation overhead of result verification.

### Context

In a P2P network, each peer may compute an input `I` against a well known 
algorithm `F(x)` and distributes the output `O` to the network peers. A peer may
also request other nodes for computing the algorithm against a set of inputs and
expects that the output received are valid. A set of received outputs 
`[O1, ..., On]` is valid if the they are correct outputs of a given set of inputs 
`[I1, ..., In]`, which means that the following holds true for every pair 
`{In, On}`:

 - Given a function `F(x)`, the output `Ox` is valid for `Ix` iff `F(In) == On`

### Problem 

In a completely decentralized network in which different peers request and serve
computation without any mechanism of trust, how can a requester peer - who asks
for a other network peers for computation - trust that the output is valid
 without having to run `F([I0, ..., In]` itself?

There is no trivial way for the requester to confirm if the output is valid
without running it locally and compare the received output with its own result, 
which defeats the purpose of requesting external computation. The goal of this
protocol is to create a mechanism for peers in the network to collectively 
ensure that requesters are providing valid outputs, while minimizing local
computation.

### Literature review

**Voting/replication solution**

Voting or replication is a generic solution for the computation verification
problem in p2p networks [1], [3]. It consists of requesting multiple peers the
computation results of the same input and select the output which was returned
by the majority. This solution requires that at least 51% of the peers who
provide the results are not compromised and return 100% correct results.
Replication has high overhead too - the same computation needs to be processed
by multiple peers.

Another disadvantage of the replication approach is the need for multiple peers
be willing to process the request. Depending on the network architecture and
protocol, this might not be the case (e.g. only certain peers in the network
serve a subset of the inputs).

This approach has been used by SETI@home [1] grid computing network.

**Quiz solution**

As presented by [1], "The basic idea of Quiz is to insert indistinguishable quiz
tasks with verifiable results known to the client into a package of normal 
tasks. The client can then accept or reject the task results based on the 
correctness of quiz results." [1] also presents a quiz generation algorithm that
optimizes the accuracy and overhead of the quiz based on a reputation system.

**Reputation system**

Reputation systems may be coupled with the computation verification protocol in
order for peers in the network to require less verification steps, thus reducing
the computation overhead. The relation between trust and computation overhead is
inversely proportional: the highest the trust, the lowest the overhead required.

[3] Uses a reputation system based on multiple techniques - voting,
spot-checking and others - and builds up metrics which define the optimal use of
computational redundancy.

[1] proposes a *trust-based scheduling* which the verification scheme is coupled
with a reputation system and they show that it helps the accuracy to converge
to 100% over time while decrease computation overhead.

Although the reputation system decreases the need to computational redundancy
overhead, it is not trivial to create one in a completely decentralized p2p
network. Grid computing reputation systems, on the other hand, are easier to 
develop and maintain since there is no requirement to distribute the reputation
system - usually small amount of nodes need to know reputation metrics and
centralization is possible.

[4] Proposes a trust system that uses DHT and CAN to calculate and store the 
global trust level for each peer.

**Grid computing vs decentralized P2P network**

Grid computing applications have been using verification schemes [1] to ensure
that outputs sent by peers are correct.

Grid computing and decentralized P2P networks may differ in a way that in grid
computing networks, the computing requester is unique and centralized (e.g.
SETI@home data centers request for peers in the network to process input),
whereas in decentralized P2P networks, any peer in the network is entitles to
request and serve computation loads. Moreover, in grid computing the reputation
system can be centralized.

### Protocol for computation verification in P2P network

The protocol is based on sampling the validity of results received. A
requester runs `F(Ix) = Ox` for a subset of the requested input and verifies
if the output received is valid. If a result received in invalid, the requester
flags the source peer as untrustworthy to the network.

The frequency of sampling performed (`Sf`) locally differs depending on the
requester risk aversion. A requester samples a percentage of the outputs
received from a certain peer. This percentage defines how much is the requester
willing to trust the requester and how much computation power is the requester
willing to spend on verification. The bigger the `Sf` is, the more likely is the
requester to catch a non-valid output received from a provider peer, but the
highest computation power is spent. In the extremes, a `Sf = 0` means that the
sampling frequency is 0 and thus, no verification is done - the local node will
accept all the outputs from the provider without running `F(Ix) = Ox`. On the
other extreme, a node adopting a `Sf = 1` will verify all the outputs received.

A `Sf = 1` can be seen as a waste of computation there is redundance of
computation - if the requester is willing to spend the computation power for
running the algorithm against all inputs, there is no reason to request it to
external peers. However, this strategy can be used to completely verify a 
certain unknown provider peer.

If the network is big enough and there is enough entropy - requests and
computation being preformed by several peers - the request peers collectively 
benefit from other peers validations and may decrease their `Sf` locally, since 
there are many other peers performing computation to verify the input from the 
requesters. 

The incentives for the provider peers to respond with invalid outputs is as low
as the collective sampling frequency of the network. The more peers there are 
verifying the results - even if locally the `Sf` is relatively low - the highest
 is a high probability that the network will sample an invalid output if it 
occurs and flag the provider as untrustworthy to the whole network.

One technique to flag a provider as untrustworthy may be by gossiping to the
whole network the invalid result. If the results are signed with the 
provider's private key, it is possible for all peers in the network to learn
about it due to the non-repudiation properties of private key signature. There
are many other reputation systems in P2P networks that can be explored (e.g. DHT
and CAN based).

### Applications

Any P2P network in which peers share computation work of a well known algorithm
and in which peers need to have a controllable degree of trust on the results
received by other - possibly unknown - peers.

**decentralized p2p search indexer**: each node crawls and rates webpages based
on a well known algorithm. The results can be shared across the network. This
protocol creates the mechanisms and incentives for nodes to use the correct
indexing algorithm and not spread poisonous indexed results to the network.

**distributed grid data processing**: applications like SETI@Home and others can
leverage this protocol to make sure the data received from other nodes are
according to the expected algorithm.

### Caveats

- Determinism

The algorithm must be deterministic in order for the peers to be able to verify
the output. For example, if the algorithm to be ran needs to use a current
timestamp or randomized number, the output will inevitably differ from peer to
peer. To avoid this, the algorithm should take all the variables as input so
that the execution can be replicated in different execution environments.

- Algorithm agreement and distribution

The algorithm must be well known by every peer in the network. Every peer must
be able to run it in a deterministic way. This poses challenges to identifying,
discovering and distribution of the algorithm.

### Protocol details and API

#### A computation request format:

```javascript
request = {
	id: "5b990d9a68348633aeffacf8eb7ac714",
	fn_sig: "4d18db80e353e526ad6d42a62aaa29be",
	input: [{},{},{},...{}]
}
```

Where: 

- `id` is a locally unique identifier for the request;
- `fn_sig` is the signature (md5/sha,...) of the function to run;
- `input` is a list of objects. Each object represents the input of one 
computation;

The request must be signed by the requester.

#### A computation response format:

```javascript
	reponse = {
		id: "c6646510dcdc4d2fc990af4b88ce3de9",
		req: { ...request },
		output: [{}, {},... {}]
	}
```

Where:

- `id` is a locally unique identifier for the response;
- `req` is a copy of the signed request
- `output` is a list of objects. Each object represents an output relative to
the requested input. 

The response must be signed by the peer provider.

#### API

```javascript
result = verify(Fn(), response, provider_pubkey, Sf)
```

Where:

- `Fn` is the function or pointer to the binary that is supposed to be verified
- `response` is the response object received from the provider peer. It contains
  the outputs to be verified against `Fn()`
- `provider_pubkey` is the provider peer public
- `Sf` is the sampling frequency. The `Sf` value can be between 0 and 1, in
  which 0 means no sampling and 1 means sampling all the outputs.
- `result` is an object describing the verification result. The result object is
as follows:

```javascript
result = {
	Sn: 0.3,
	Fn: Fn(),
	ok: [true, ..., false],
	results: [{}, ..., {}]
}
``` 

---

1. [Result Verification and Trust-based Scheduling in Peer-to-Peer Grids](https://ieeexplore.ieee.org/document/1551018/)

2. [Uncheatable Grid Computing](https://ieeexplore.ieee.org/document/1281562/)

3. [Sabotage-tolerance mechanisms for volunteer
computing systems](https://www.sciencedirect.com/science/article/pii/S0167739X01000772)

4. [The eigentrust algorithm for reputation management in p2p networks](http://ilpubs.stanford.edu:8090/562/1/2002-56.pdf)


Thanks @mikhaelsantos and @sergioisidoro for the discussions and ideas
