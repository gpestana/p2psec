## Protocol for computation checking in P2P networks

A protocol for checking if peers in a p2p network are performing valid
computations of a well known algorithm.

### Context

In a P2P network, each peer compute an input `I` against a well known algorithm
`F(x)` and distributes the output `O` to the network peers. A peer may also
request other nodes for computing the algorithm against a set of inputs and
expects that the output received are valid. A set of received outputs 
`[O1, ..., On]` is valid if the they are correct outputs of a set of inputs 
`[I1, ..., In]`, which is the same as saying that the following holds true for
every pair `{In, On}`:

Given a function `F(x)`, the output `Ox` is valid for `Ix` iff:

```
F(In) = On
```

### Problem

In a completely decentralized network in which different peers request and serve
computation without any mechanism of trust, how can a requester peer - who asks
for a certain input to be ran against the algorithm - trust that the output is
correct without having to run it itself?

There is no trivial way for the requester to confirm if the output is valid
without running it locally and compare the received output with its own result, 
which defeats the purpose of request external computation.


## Protocol for computation checking in P2P networks
### Applications
