This paper discusses the problems narrowing down anonymous systems as entropy systems. It claims that entropy is not a good measure for anonymity and systems designed to maximize entropy also obfuscate how anonymous the system really is, while not protecting some attack vectors in protocols such as onion routing and mixnets. It also says that, although secure against relatively strong adversaries, mixnets are not user friendly (due to high latency) enough to so that the adoption makes it secure. Thus, onion routing ends up being more secure against expected and real-case scenario adversaries. It wraps up by suggesting that trust can be used to improve onion routing protocols.

## notes/questions

- I believe the most popular classes of anonymous communication systems are entropist (Tor, mixnets) If these are not appropriate, what are the other options? 

- entropism: entropy does not always mean anonymity. when entropy is the top priority, it drives design to maximize entropy instead of anonymity. anonymity is a multi-faceted property and it does not good to focus on a property alone (e.g. entropy)

"Tor [...] gets its protection from creating cryptographic circuits along routes that an adversary is unlikely to observe or control."

Tor passes traffic bidirectionally with reduced latency, which makes is a good fit for anonymous DHTs communications.

- an entropy approach to Tor anonymity: Tor anonymity relies on the size of the anonymity set.

- timing attacks - controlling both entry and exit nodes or controlling website and entry node - can be trivially used to de-anonymise traffic regardless of the size of the anonymity set (entropy). in this case, entropy fails to deliver anonymity. anonymity is not causal of entropy in certain cases.

- entropy as the main focus for designing and evaluate anonymity systems obscures the level of anonymity a system provides.

- for those who see entropy as the solution for network anonymity, the question that is tried to answer is "how can entropy make a set of users less distinguishable".

**adversaries and vulnerabilities in entropy-based anon systems:**

- the attacker: "The Man": he owns big chunks of the anonymity infrastructure. He also controls ISPs, backbones and websites and have physical surveillance access to its victims.

- global passive adversary: controls no nodes, but can observe all traffic in all the network links. this adversary is unlikely to exist and it is both too powerful (can passively sniff all network traffic) and too weak (cannot actively interfere with any network packet)

- low latency anonymous network are (usually) vulnerable against The Man

- onion routing without entry guards are broken against small number of well placed adversaries for longterm, repeated connections (do not allow long term, repeated connections)

-  

## in-DHT onion routing

- onion routing requires a certain level of entropy for providing sender anonymity. how much entropy is needed in a purely P2P network - e.g. DHT -  for onion routing to work? 

- (for the paper) onion routing is as secure as the inability to an adversary to observe the cryptographic circuits used by a sender. thus we we must not consider global adversaries.

- (for the paper) onion routing security breaks against an adversary that can observe the whole network - and thus correlate traffic from both entry and exit nodes of a particular circuit. Onion routing is designed to be secure against adversaries with only partial view of the network. 

	- Can we assume that an adversary will not be able to passively get all traffic in the network? 
 	- Giving its P2P routing protocol, could it be that DHTs are more vulnerable to adversaries to link relays in the same circuit than other P2P networks?  

- anonymity vulnerabilities and low latency are correlated.

- low latency anonymity networks are fundamentally broken against The Man, but do offer some protection against weaker adversaries and may offer an interesting trade-off between latency, overhead and anonymity for DHTs.


## check later

- Shannon entropy

