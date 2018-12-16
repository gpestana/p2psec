## Bifrost: A Novel Anonymous Communication System with DHT
**Nasaki Kondo, et al.**

**what** the paper proposes separating the separation of the node management 
layer from the anonymous communication layer in P2P networks. The management
layer yses Chord DHT.

**results**
**importance**

**goals**: anonymous communications is defined through 1) sender anonymity; 2)
receiver anonymity; 3) untraceability. To achieve this degree of anonymity, the
receiver's IP address and routing information is encrypted in the messages.

**onion routing**: bifrost uses onion routing to achieve anonymous message
routing.

**node management layer and anonymous routing layer**: bitfrost separates the
node management and routing layers. The node management layer is a Chord DHT to
construct and maintain routing node routing tables. The anonymous routing layer
responsibility is to build routing circuits and encrypt messages.
 
