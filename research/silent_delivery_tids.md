## SilentDelivery: Practical Timed-delivery of Private Information using Smart Contracts

[arXiv](https://arxiv.org/pdf/1912.07824.pdf)

**Chao Li, Balaji Palanisamy**

**Summary/usefulness:** SilentDelivery is a very niche protocol (a decentralized
Timed-Information Delivery System [TIDS]). The main idea is that a set of smart
contracts provide a server for a sender to upload private information that is
revealed only after an interval, defined by the sender. Both “privacy” and “gas
cost savings” are in the context of TIDS, since by “private” they mean that the
trustees are not public (simply by encrypting the list of trustees) and “gas
costs savings” means that the protocol has a lightweight mode in which no heavy
verifications are done until some player challenges an adversary.

**what:** SilentDelivery is a decentralized approach for Timed-Information Delivery
System, which is secure, scalable and cost-efficient. It uses Threshold Secret
Sharing and Smart contracts for implementing a cost-efficient protocol for
timed-delivery of private information.

Times-Information Delivery System (TIDS) allows a sender to make an information
to arrive to a destination at a chosen future time.

The scalability is provided by implementing 2 different running modes: a
lightweight, where the heavy verifications do not take place; and a heavyweight
mode, which can be triggered for conflict resolution, in which all verification
happen.

Sender needs a private channel with all trustees (for sharing the TSS key
shares). This can be done using asymmetric encryption.

Since adversarial trustees may be able to disclose the keys before the time
defined by the Sender, it is possible for other trustees to report this to the
service provider. If the report is correct, then the trustee gets the Eth that
was kept for the adversary.

**potential vulnerability 1 (incentive design):** What if disclosing the timed-secret before
time is more valuable than the incentives for the trustees to only disclose
their shares once the time is up? If that’s the case, the trustees may as well
just decrypt the information before time. 
Fix: The identity of the trustees must not be revealed.

**potential culnerability 2 (availability):** What if there are not enough trustees online
when the message should be reported? If that happens, then the info is not
decrypted and the service does not work.

**scalability and costs:** The receiver needs to “recruit” n  trustees using a smart
contract, which is expensive. More trustees means better availability (t-n), but
more costs incurred on the sender.

**tackling the challenges:**
 - **strategy 1**: The relation between sender and trustee is kept private, by
encrypting the entries in the list of trustees for a protocol run. This strategy
makes it harder for other trustees to find whom to collude, in order to perform
the attack described in vulnerability 1. 

 - **strategy 2:** Implement 2 modes of the protocol: a lightweight where trustees are
trutes, and a heavy mode when a trustee reports an adversary. Trustees are
incentivized to report malicious players.


