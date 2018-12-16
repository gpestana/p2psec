## Crawling the dht for fun and profit
**Scott Wolchok and J. Alex Halderman**

**What**: 2 attacks crawling the Vuze BitTorrent DHT: crawling for creating a new
index and passively crawling over time for getting information about what data
is being searched and when.

**Result**: possible to create a new index with millions of entries in a question of
hours; tracked 8M ips downloading over 1.5M files in 16 days

**Importance**: vuze BitTorrent DHT is not private and it is easy for law
enforcement to track who's downloading and providing copyrighted material. The
upside of it is that it is easy to replicate the tracking index if needed.
Monitoring user activity is very easy and cheap.

**Vuze DHT in the context of BitTorrent**: Generally, a DHT provides a data model
abstraction in which the user store and retrieve values based on keys in a
decentralized, p2p network.

BitTorrent uses two different DHTs [why/differences]. The DHTs are used for
keeping a logbook of which peer in the network keeps which files and provides
the primitives for storing and lookup trackers. The DHT is basically a
decentralized log book. The p2p architecture gives resilience to the network:
it's not easy to shut down BitTorrent if the log of who has which files is
stored in millions of computers. The DHT prevents single point of failure
[counter examples of Napster].

**The sniffing attack**: uses the Sybil attack to get visibility of who is part of
the network (IPs) and what each peer is storing and requesting. The attack
consists of inserting many clients in the network and waiting for the data to be
replicated to them. As the attack nodes keep receiving and storing replicated
data and DHT requests, they keep a log of IP addresses and content
requested/stored. Once the data has been replicated, the nodes jump to other
position in the DHT and restart the process again. This makes it fast and
relatively cheap to gain a lot of information about the DHT and its nodes.

**Identifying peers**: identifying the most active peers in the bittorrent network
can be challenging because BitTorrent users may use proxies to maintain
anonymity. This and the fact that many peers may use the same proxy, resulted on
a small number of pairs IP:port pair to be associated with relatively large
amounts of files and connections, when compared with individual users. In the
context on BitTorrent, this relation is enough to enable attackers to identify
individual peers and trace them down.

**Conclusion**: DHT makes the BitTorrent tracking more resilient since there is no
single point of failure which would shutdown the network if down. The P2P nature
of the DHT makes it easy to 1) replicate the tracker indexing and 2) get an
accurate picture of who is participating in the network and how. These two
points are easily achieved by creating many nodes which sniff the network and
change positions in the DHT often.


**To read further**:

- ZHANG, C., DHUNGEL, P., WU, D., AND ROSS, K. W. Unraveling the BitTorrent
ecosystem. http://cis.poly.edu/~ross/papers/PublicEcosystem.pdf, 2009

**Open questions**:
 
- Why aren't right holders using these techniques to target individuals which are
illegally downloading copyrighted material?

- It's easy to lower incentives for actively participating in BitTorrent by
prosecute users who relay and download copyrighted files. How to achieve
anonymity/privacy in the DHT context, without decreased performance and decrease
user experience.

