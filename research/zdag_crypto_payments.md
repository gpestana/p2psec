---
title: Z-DAG - PoS solution for real-time crypto payments
description: notes on Z-DAG paper
tags: papers, done
---

## Z-DAG: An interactive DAG protocol for real-time crypto payments with Nakamoto consensus security parameters

*Jagdeep Sidhu, Msc., Eliot Scott , Alexander Gabriel* (Syscoin Core Developers, Blockchain Foundry Inc)

[zdag paper](https://syscoin.org/zdag_syscoin_whitepaper.pdf)

The main idea of Z-DAG is to enforce a delay between transaction broadcast to allow nodes to deterministically construct a DAG of transactions before minting the block. Z-DAG provides a way for sender and receiver to preemptively agree on the validity of a transaction (with some confidence) before the block containing the transaction has been minted.

The main use case for Z-DAG is for point-of-sale solutions, to allow a payer to walk out from shop with some degree of confidence that the payment succeeded, without having to wait for the transaction to be minted.

Interesting approach, but I'm not fully convinced that merchants can trust unconfirmed transactions before block confirmation with a higer degree of confidence, in an adversarial setup. Also, there is no discussion about threat model and how Z-DAG can be attacked, which only confirms by skepticism.

**Notes**:

- Zero Confirmation Directed Acyclical Graph -- a technology that allow for point of sale with high degree of statistical probability of settlement in real time.
- Instant settlement protocol that uses a PoW. It is used in the confirmation of Syscoin service transactions (Syscoin provides trustless interoperability with Ethereum ERC-20, token & asset microtransactions, and Bitcoin-core-compliant merge-mined security);
 
- **Goal**: Z-DAG is used to validate nodes across the network and to ensure there is consensus on the ordering of transactions and no double spending.

- DAG Settelement: participants in a transaction are able to anticipate what transactions will be in the next block (and order) with confidence, before the block has been minted. This is made possible since miners order queued transaction based on time (with negligible processinf requirements).
- Incetives for ordering the transactions locally (miners): If the miner fails to order transactions, there is a risk for the block to not be accepted by the network, since accounts may overflow.
- Validating nodes use "a list" (which?) contained in the blocks to confirm there was no double-spending.
- Two transactions must have an interval period between issuance and network propagation (10s), in order for validating nodes based on time. If transfers are made within this delay, a conflict state is set.
- PoW is a fallback and partition tolerance mechanism for the DAG operation, since a new DAG is constructed for every block. 
- [**] In Bitcoin, double-spend can be modeled as a race between valid and malicious transactions to propagate the most node across a network first, thus by creating and enforcing delays between transactions, one transfer as exponential advantage over another. This allows Z-DAG to be constructed deterministically (since the ordering problem as been solved), which is hard to achieve in decentralized distributed systems.
- The rules of the consensus are not enforeced by the network, but rather between sender and receiver;
- Although sender and receiver can realize the account updates before transaction has been confirmed, the transaction is not completed before the block constaining it is mined. The transaction is simply settled with confidence (i.e. there's a prior agreement between sender and payed that the transaction will happen, with some degree with confidence [how to quanitfy confidence?]);
- With Z-DAG, the broadcasting nodes do not check for the validity of the transaction before broadcasting it, so as to speed up the transaction broadcsating over the network --> Optimistical broadcasting.



**high level overview of Z-DAG**:

1) Initiating node broadcasts that it has sent Syscoin Asset to another address;
2) As nodes receive transaction, they broadcast is before verifying it;
3) Nodes proceed to verify transaction;
4) Once transaction reaches destination, the sale is completed with confidence (even before block has been mined);
5) Miners order by time unconfirmed transactions and compete to mine the block (a la BTC)
6) Transactions of mined blocks are considered confirmed;


#### Questions and comments: 

- How is the delay between transactions enforced when multiple parties broadcast new transactions? i.e. it is relatively easy to verify that party A issues N transactions spaced at least by interval A, but it becomes harder to do the same (without really bad QoS) with to ensure interval of transations between M parties.
- The optimistic transasction broadcasting seems fragile against attackers. What is the probability of rolling back unconfirmed transactions when the sender is adversarial?
- No thread model?
- In the conclusion: "By using Z-DAG, customers transactions can be settled quickly and with the absolute security proven by Bitcoin.", this seems an overstatement to me. I'm still not convinced that a merchant can trust unconfirmed transactions with a high degree of confidence. How about if the transaction is broadcasted by adversary nodes that don;t check for the 10s delay, until the transaction arrives to the merchant? How easy is it to perform this attack?