## Latency and Routing Efficiency Based Metric for Performance Comparison of DHT Overlay Networks
**Nitin Varyani, et al.**

**what**
mathematical model for measuring performance of structured DHT taking into
consideration both latency per successful lookup and routing efficiency. the
metric considers scenarios where failed lookups are retried by the protocol.
the paper also shows the model results applied to four different DHT protocols.

**importance**
important to establish a performance metric that can be applied to all DHT
protocols, so protocols can be uniformly compared. 

**previous DHT performance metrics and results**
structured DHT overlay networks have been evaluated based on 1) mean latency per
successful lookup and 2) percentage of successful lookups.

[8] routing efficiency as ratio of successfully routed messages/total numbers of
messages sent. Kademlia > Pastry > Chord.

[9] routing efficiency as average node live bandwidth per failed lookup. Kademlia
performs better under this metric. however, when considering node live bandwidth
per median of successful lookup latency, kademlia performs the worst. this work
considers a performance vs cost framework, which reveals how much network 
bandwidth is needed in order to achieve a certain lookup latency.

[10] routing efficiency as churn rate effect on the mean successful lookup
latency.

**why new metric**
DHT application with lookup retries must consider the `mean successful latency` 
and `routing efficiency` (% successful lookups) when evaluating performance.

