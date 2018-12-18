## ClaimChain: Improving the Security and Privacy of In-band Key Distribution for Messaging

**Bogdan Kulynych, Wouter Lueks, Marios Isaakidis, George Danezis, and Carmela Troncoso.**

**what**: ClaimChain is a cryptographic primitive for providing a privacy-preserving, authenticated and decentralized data store of claims. In this paper, the primitive is presented and the example of in-band email pubkey exchange is used.   

**results**: ClaimChain has set of properties that can be used in different use cases in decentralized systems. A ClaimChain is authenticated (e.g. readers can be convinced about who generate the chain), it includes fine-grained access control mechanism (e.g. each claim in the chain may have controlled access) and it is privacy-preserving, although every reader can prove that the claim is valid, even if she cannot access any of its information.

**importance**: interesting primitive for decentralized systems with privacy preserving characteristics and capabilities. It also improved email in-band key-exchange without relying on external entities and servers.

**properties**:

**format**: A ClaimChain is a structure of linked blocks. Each block is the state (her own information and her current view of the network) of the owner when the block was generated. Each block contains {payload, pointer_previous_block, signature}. Each payload contains {index, nonce, metadata (i.e. pub keys, etc), public_data, block_map}. 

**encoding scheme**:

**access capabilities**:

**content addressable store**: