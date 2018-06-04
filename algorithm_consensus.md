## Protocol for computation checking in P2P networks

A protocol for checking if peers in a p2p network are performing valid
computations of a well known algorithm.

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

## Protocol for computation checking in P2P network

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
about it due to the non-repudiation properties of private key signature.

### Applications

Any P2P network in which peers share computation work of a well known algorithm
and in which peers need to have a controllable degree of trust on the results
received by other - possibly unknown - peers.

**decentralized p2p search indexer**: each node crawls and rates webpages based
on a well known algorithm. The results can be shared across the network. This
protocol creates the mechanisms and incentives for nodes to use the correct
indexing algorithm and not spread poisonous indexed results to the network.

**distributed data processing**: applications like SETI@Home and others can
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

#### Acks

Thanks @mikhaelsantos and @sergioisidoro for the discussions and ideas
