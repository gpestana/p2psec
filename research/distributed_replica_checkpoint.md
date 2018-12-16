## Uncoordinated distributed checkpoints

[1] [Discarding Obsolete Information in a Replicated Database System](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.470.8648)

Algorithm for distributed nodes to locally identify the set of timestamps that 
were received by all nodes. The highest timestamp of that set is called the
`Global-Cutoff` timestamp and it ensures that all older timestamps have been
received by all nodes in the network. This decision can be made locally and
different nodes may determine it at different times.

To ensure a safe checkpoint for snapshot, it is necessary to take into 
consideration the updates in transit - timestaps sent by nodes in the network 
but which were not yet received locally. The smallest timestamp from the set
which is the union between the timestamps in transit and highest local timestamp
is a `Global-Cutoff`. It is proved that this timestamp cannot decrease in the
network, which means that no future update can have smaller timestamp. This is 
the checkpoint in which every older timestamp can be safely assumed to have 
reached all nodes.

The algorithm is basically the following:

- A node computes its `Local-Cutoff` (LC) - the highest timestamp received locally;
- A node keeps a timestamp matrix (clock matrix) in which it records all the 
	`LC`s of its network peers;
- At every local update, the node computes a new `LC` based on the timestamp
  matrix and gossips it to the network.


