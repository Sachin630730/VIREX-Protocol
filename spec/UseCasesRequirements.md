# VIREX Protocol – Use Cases & Requirements (v0.1.0-alpha)

**Author:** Syon Foppen  
**Status:** Alpha – for public feedback only  

---

## 1. Introduction  

This document defines the **use cases** and **requirements** for the VIREX protocol.  

It explains:  
- What the system is designed to achieve  
- Typical scenarios for real-world usage  
- Functional and non-functional requirements for the protocol  

The goal is to provide a **clear roadmap** for both specification authors and future implementers.

---

## 2. Use Cases  

### 2.1 Private Messaging  
**Actors:**  
- Alice (Sender)  
- Bob (Recipient)  
- Mixnodes, Mailbox Nodes, ODS Servers  

**Description:**  
Alice sends a message to Bob without revealing:  
- Who she is sending to  
- When she is sending it  
- How often they communicate  

**Requirements Met:**  
- End-to-end encryption  
- Metadata privacy  
- Mailbox anonymity  
- Proof-of-Work against spam  

---

### 2.2 Federated Governance  
**Actors:**  
- Node Operators  
- Auditors  
- Federation Key Holders  

**Description:**  
Critical actions like key rotations, node onboarding, and revocations require **M-of-N approvals** using threshold cryptography.  

**Requirements Met:**  
- Distributed trust  
- Transparency logs  
- Auditor oversight  

---

### 2.3 Key Lookup with Privacy (ODS)  
**Actors:**  
- Alice (Client)  
- ODS Servers  
- Auditors  

**Description:**  
Alice fetches Bob’s public key via the **Oblivious Directory Service** without revealing to anyone which key she is looking up.  

**Requirements Met:**  
- Anonymous key lookups  
- Publicly auditable directory logs  
- Signed directory snapshots  

---

### 2.4 Abuse Prevention  
**Actors:**  
- Spammers  
- Honest Clients  
- Federation Operators  

**Description:**  
Malicious actors attempting to flood the network are mitigated by:  
- Proof-of-Work puzzles  
- Rate limiting per sender  
- Auditable logs for reporting abuse  

**Requirements Met:**  
- Spam resistance  
- DoS mitigation  
- Transparency and accountability  

---

### 2.5 Public Auditing & Misbehavior Detection  
**Actors:**  
- Auditors  
- Federation Key Holders  
- General Public  

**Description:**  
Independent auditors verify logs and node behavior to detect censorship, misrouting, or malicious key changes.  

**Requirements Met:**  
- Transparency logs  
- Verifiable proofs (Merkle trees)  
- Public misbehavior reports  

---

### 2.6 Privacy for Journalists, Whistleblowers & Activists  
**Actors:**  
- Journalists  
- Whistleblowers  
- Activists & NGOs  

**Description:**  
Sensitive communication often involves high-risk scenarios where metadata privacy is as critical as content confidentiality:  

- A journalist communicates with a whistleblower under strict secrecy.  
- A human rights activist shares information in a censored environment.  
- NGOs exchange sensitive data in authoritarian regions.  

**Requirements Met:**  
- **Metadata Privacy:** Prevent linking sender and recipient.  
- **Cover Traffic & Fixed Polling:** Hide real communication patterns.  
- **Anonymous Key Lookups:** Prevent key request correlation attacks.  
- **Federated Governance:** Avoid single-operator compromise or censorship.  
- **Transparency Logs:** Detect any silent key replacement or manipulation.  

---

## 3. Functional Requirements  

| ID    | Requirement                                          | Alpha Version (v0.1.0) | Future Version         |
|-------|------------------------------------------------------|-------------------------|-------------------------|
| F1    | End-to-end encryption (ChaCha20-Poly1305)            | ✓                       | PQC hybrid (v2.0.0)      |
| F2    | Multi-hop mixnet routing with layered encryption      | ✓                       | Optimization planned     |
| F3    | Proof-of-Work puzzles for spam resistance             | ✓                       | Adaptive difficulty      |
| F4    | Anonymous key lookups via ODS                         | ✓                       | Privacy-preserving ZKPs   |
| F5    | Threshold cryptography for governance decisions       | ✓                       | Advanced cryptographic voting |
| F6    | Transparency logs with Merkle Tree proofs             | ✓                       | Distributed log shards    |
| F7    | Fixed-interval mailbox polling for metadata privacy   | ✓                       | Adaptive polling patterns |
| F8    | Gossip protocol for peer discovery                    | Planned                 | v0.2.0-beta               |
| F9    | Auditors verifying log consistency and node behavior  | ✓                       | Automated auditing tools  |
| F10   | Public misbehavior reports                            | ✓                       | Zero-knowledge proofs     |

---

## 4. Non-Functional Requirements  

| ID    | Requirement                                  | Target for v1.0.0               |
|-------|----------------------------------------------|----------------------------------|
| N1    | Latency below 5 seconds for Level 1 privacy  | < 5s average per message          |
| N2    | Horizontal scalability for mixnodes          | Support 1000+ concurrent nodes    |
| N3    | Robustness under node churn                   | No single point of failure        |
| N4    | Open federation with independent operators    | No centralized trust              |
| N5    | Public verifiability of logs                  | Consistency proofs for all changes |
| N6    | Extensibility for post-quantum cryptography   | Hybrid crypto support planned      |
| N7    | Minimal metadata leakage                      | Cover traffic + Poisson delays     |
| N8    | High availability (> 99%) for core services    | Redundant node infrastructure      |

---

## 5. Future Extensions  

- **Post-Quantum Cryptography (v2.0.0):** Hybrid PQC for key exchange and signatures.  
- **Automated Auditing:** Zero-knowledge proofs for misbehavior detection.  
- **Advanced Anti-Sybil Mechanisms:** Reputation systems, staking models.  
- **Public Testnet:** Large-scale testing before v1.0.0 stable release.  

---

## 6. Out of Scope for Alpha  

- Formal verification of cryptographic primitives.  
- Integration with external identity systems.  
- Mobile and lightweight client implementations.  

---

## 7. License  

- **Specification:** Creative Commons Attribution 4.0 (CC BY 4.0)  
- **Code (future):** Apache License 2.0  

---
