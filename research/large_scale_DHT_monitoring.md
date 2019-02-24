## Large-Scale Monitoring of DHT Traffic
**Ghulam Memon, et al.**

**what**: technique called Montra for effectively perform passive monitoring of DHTs without biasing results and with relatively few peers. The key idea of Montra is to make monitors minimally visible and lightweight.

**results**: Montra can capture around 90% of the query traffic and accurately identify its source and destination for 90% in a Kademlia DHT. 32K kad peers with Intel Core 2 Duo 1GB

**importance**: DHT monitoring is important for many reasons: 1) metrics of the network and for further improvement 2) assessing the security/privacy properties of the network. It is, thus, important to monitor the traffic of DHTs without biasing the results, while being able to gather enough traffic with few resources 

--- 

**naïve DHT traffic capture**: problems with naive DHT traffic capture are: 1) small number of passive monitor peers will result in biased and non-representative results; 2) too many peers will result in too much resource consumption and 3) actively disrupt the network behavior.

**kad DHT traffic classification**: the traffic can be classified into two categories: 1) destination traffic (lookup request received by the destination after - potentially - routing the network) and 2) routing traffic (request which is being routed towards final destination). Montra focuses on measuring destination traffic since it represents user behavior and it is comparably less than routing traffic.

**Minimal Visible Monitors**: (MVMs) are peers which monitor the traffic requests for a certain content ID by placing itself in the vacinity of the content ID, based on kad's XOR'ed metric. By doing this, MVM will receive the same requests as the peers responsible by the peer ID. This happens due to redundancy mechanisms in DHTs ("Montra leverages the need to “lookup multiple nodes” to capture each lookup message"). 
 
**Monitored DHT zones**:

---

- "most of early studies on DHTs focused on extensive simulations, analysis and small scale deployments" -- not so much the case anymore with networks such as bittorrent, IPFS, Dat, etc.