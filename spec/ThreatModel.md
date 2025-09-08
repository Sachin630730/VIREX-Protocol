# VIREX Protocol – Threat Model (v0.1.0-alpha)

**Author:** Syon Foppen  
**Status:** Alpha – public feedback welcome  

---

## 1. Introduction  

This document defines the **threat model** for the VIREX protocol.  

It clarifies:  
- The **assumptions** we make about the system and its environment  
- The **adversary capabilities** we aim to defend against  
- The **attacks** considered in scope for this version  
- The **security goals and mitigations** designed into VIREX  

---

## 2. Security Goals  

1. **End-to-End Confidentiality:**  
   Only sender and recipient can read message contents.  

2. **Metadata Privacy:**  
   Adversaries cannot easily link sender and recipient or learn timing/frequency patterns.  

3. **Integrity & Authenticity:**  
   Messages and system metadata cannot be altered undetected.  

4. **Abuse Resistance:**  
   Prevent spam, flooding, and malicious node takeovers.  

5. **Transparency & Accountability:**  
   Misbehavior by nodes or operators can be detected via public logs and audits.  

6. **Federated Governance:**  
   No single entity controls the network; trust is distributed across independent parties.  

---

## 3. System Assumptions  

- **Federation of Independent Nodes:** Multiple operators run mixnodes, mailbox nodes, and ODS servers.  
- **Cryptographic Primitives Secure:** X25519, ChaCha20-Poly1305, Ed25519, SHA-256 assumed secure for alpha.  
- **Adversary Resources Finite:** Attackers have limited bandwidth, compute, and cannot break standard crypto primitives.  
- **Auditors are Honest:** At least some auditors act honestly and publish accurate transparency logs.  

---

## 4. Adversary Model  

### 4.1 Capabilities  

Adversaries may:  
- Control parts of the network (mixnodes, mailbox servers, ODS replicas).  
- Observe traffic on links between clients and nodes.  
- Attempt message correlation through timing and volume analysis.  
- Submit arbitrary messages, possibly in large volumes (DoS).  
- Attempt key directory manipulation or node impersonation attacks.  
- Collude with other malicious operators.  

### 4.2 Goals of the Adversary  

- **Deanonymization:** Link sender and recipient through traffic analysis.  
- **Message Disclosure:** Break confidentiality of message contents.  
- **Service Disruption:** Cause denial-of-service or message loss.  
- **Infrastructure Compromise:** Control or impersonate nodes, ODS, or governance keys.  
- **Reputation Attacks:** Frame honest nodes as malicious through fake reports.  

---

## 5. Threat Scenarios & Mitigations  

| Threat                        | Description                                  | Mitigation in VIREX                           |
|-------------------------------|----------------------------------------------|-----------------------------------------------|
| Traffic Analysis               | Correlating send/receive times & volumes      | Poisson delays, dummy traffic, fixed-size blocks |
| Compromised Mixnode             | Attacker controls one or more mixnodes        | Multi-hop routing, no single point sees full path |
| Global Passive Adversary        | Observes all traffic globally                 | Cover traffic, metadata-hiding fetch patterns   |
| Key Replacement Attacks         | Malicious ODS gives fake keys                 | Merkle-tree transparency logs, signed roots     |
| DoS / Spam                      | Flooding nodes with junk traffic              | Proof-of-Work, rate limits, auditing            |
| Node Collusion                  | Multiple malicious nodes cooperate            | Federation approval, distributed trust          |
| Malicious Governance Keys       | Single operator abuses power                  | Threshold signatures (M-of-N approvals)         |
| Replay Attacks                  | Resending old messages                        | Nonces + sequence numbers in encryption layer   |
| Timing Attacks on Mailbox        | Observing when recipients fetch messages      | Fixed-interval polling, dummy fetches           |
| Message Tampering                | Modifying messages in transit                 | AEAD encryption (ChaCha20-Poly1305)             |
| Log Tampering                    | Hiding misbehavior in audit logs              | Append-only transparency logs, auditor proofs   |

---

## 6. Out of Scope (Alpha Version)  

- **Post-Quantum Attacks:** Future version (v2.0.0) will add PQC algorithms.  
- **Side-Channel Attacks:** Timing leaks on client devices not addressed in alpha.  
- **Physical Attacks:** Hardware compromise, coercion, or endpoint malware.  
- **Global Active Adversary:** Controlling majority of infrastructure simultaneously.  

---

## 7. Residual Risks  

- A **global passive adversary** observing *all* network links over a long time could still do statistical correlation, especially with low traffic volumes.  
- Federated governance assumes at least some fraction of nodes and auditors remain honest.  
- Extreme DoS attacks could delay message delivery despite PoW and rate limiting.  

---

## 8. Future Improvements  

- **Post-Quantum Cryptography:** Hybrid schemes to resist future quantum adversaries.  
- **Stronger Sybil Resistance:** Staking or reputation-based node admission.  
- **Adaptive Cover Traffic:** Smarter dummy traffic strategies under changing network loads.  
- **Automated Misbehavior Detection:** Auditors using zero-knowledge proofs for censorship resistance.  

---

## 9. Conclusion  

The VIREX threat model aims to balance **privacy**, **security**, and **abuse resistance** in a federated, open system.  
Residual risks remain for powerful adversaries, especially **global traffic analysis** and **colluding malicious nodes**.  
Mitigations in later versions will focus on stronger anonymity sets, post-quantum security, and advanced anti-Sybil mechanisms.  

---
