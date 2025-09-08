# VIREX Protocol – Deep Dive (v0.1.0-alpha)

**Author:** Syon Foppen  
**Status:** Alpha – technical deep dive for public feedback  

---

## 1. Introduction  

This document provides a **technical exploration** of the VIREX protocol design for developers, security engineers, and reviewers.  

It explains the **core components, cryptographic layers, routing mechanisms, peer federation, and security assumptions** in greater detail than the main specification or overview.

---

## 2. High-Level Architecture  

VIREX consists of five main layers:  

1. **Mixnet Layer:** Multi-hop message routing with layered encryption.  
2. **End-to-End Encryption Layer:** Protects message contents from all intermediaries.  
3. **Oblivious Directory Service (ODS):** Public, auditable key directory with anonymous queries.  
4. **Mailbox Layer:** Stores encrypted messages for recipients with metadata privacy.  
5. **Governance & Auditing Layer:** Ensures transparency, abuse prevention, and trust minimization.  

Community peers and federation provide the **infrastructure backbone**, ensuring decentralization, openness, and resilience.

---

## 3. Mixnet Layer  

### 3.1 Goals  
- Hide who communicates with whom.  
- Resist traffic analysis via dummy traffic and delays.  
- Ensure no single node learns sender, recipient, and message content together.  

### 3.2 Routing Mechanism  
- Each message is wrapped in multiple layers of encryption (“onion routing”).  
- Each hop removes one layer to reveal the next destination.  
- Randomized **Poisson delays** prevent timing correlation.  
- **Dummy messages** are inserted to ensure constant traffic levels.  

### 3.3 Packet Format (Alpha Version)
| Field            | Size       | Purpose                                |
|------------------|------------|-----------------------------------------|
| Header (Encrypted)| Variable   | Next hop address + routing metadata     |
| Payload           | Variable   | Encrypted inner packet or final message |
| MAC               | 32 bytes   | Integrity check (HMAC-SHA256)           |

---

## 4. End-to-End Encryption Layer  

### 4.1 Key Exchange  
- **X25519** used for ephemeral Diffie-Hellman key exchange.  
- Each message uses a **fresh session key** for forward secrecy.  

### 4.2 Encryption  
- **ChaCha20-Poly1305 AEAD** for authenticated encryption.  
- Message = `Encrypt( session_key, plaintext || padding )`  

### 4.3 Padding  
- Messages are padded to fixed sizes to resist size-based traffic analysis.  

---

## 5. Oblivious Directory Service (ODS)  

### 5.1 Purpose  
- Store recipients’ public keys.  
- Support anonymous lookups: No one learns which key is being queried.  
- Ensure key integrity: Prevent silent key replacement attacks.  

### 5.2 Design  
- **Merkle Tree** for inclusion proofs and consistency proofs.  
- Clients verify root hashes signed by **federated operators**.  
- Anonymous lookups done via the **mixnet layer** to hide the query target.  

### 5.3 Security Goals  
- **Unobservability:** No link between lookup request and recipient identity.  
- **Auditability:** Any malicious key changes are publicly detectable.  

---

## 6. Mailbox Layer  

### 6.1 Design Goals  
- Recipients fetch messages without revealing read patterns.  
- Prevent timing correlation between message arrival and retrieval.  

### 6.2 Mechanism  
- Recipients poll mailboxes at **fixed intervals**.  
- Responses are always **constant size** blocks, real or dummy.  
- Messages encrypted end-to-end; mailbox operator learns nothing.  

---

## 7. Community Peers & Federation  

### 7.1 Peer Roles  
- **Mixnodes:** Route traffic and provide anonymity sets.  
- **Mailbox Nodes:** Store encrypted messages for recipients.  
- **ODS Servers:** Maintain key directories with transparency logs.  
- **Auditors:** Verify logs, detect misbehavior, and provide public oversight.  

### 7.2 Node Registration  
- New nodes register with the federation via:  
  - A **public key** (Ed25519)  
  - **Proof-of-Work** or **staking** (future versions)  
  - Approval using **M-of-N threshold signatures**  

### 7.3 Governance Model  
- **No central authority**: Federation manages node onboarding, revocations, and key rotations.  
- **Threshold cryptography** prevents unilateral control or malicious reconfigurations.  

### 7.4 Peer Discovery  
- Nodes share signed metadata via:  
  - **Gossip protocols** for dynamic updates  
  - **Signed snapshots** for clients bootstrapping into the network  

Metadata includes:  
- Node type and public key  
- Uptime and performance metrics  
- Federation approval status  

### 7.5 Reputation and Misbehavior Handling  
- Misbehaving nodes are **publicly flagged** in transparency logs.  
- Federation can **suspend or revoke** malicious nodes with public proofs.  
- Auditors continuously verify **routing integrity** and **log consistency**.  

### 7.6 Community Participation  
- Anyone can join, but **quality and security requirements** must be met.  
- Ensures both **openness** and **robustness** against Sybil attacks.  

---

## 8. Governance & Auditing Layer  

### 8.1 Transparency Logs  
- **Append-only Merkle Trees** for:  
  - ODS root hashes  
  - Node onboarding/removal events  
  - Key rotations and revocations  

### 8.2 Auditor Responsibilities  
- Verify log **consistency** across time.  
- Publish **misbehavior reports** if nodes act maliciously.  
- Participate in **M-of-N approval** workflows for critical changes.  

---

## 9. Cryptographic Primitives  

| Function                 | Algorithm (Alpha)        | Purpose                            |
|---------------------------|--------------------------|-------------------------------------|
| Key Exchange               | X25519                   | Ephemeral Diffie-Hellman             |
| Encryption                 | ChaCha20-Poly1305        | AEAD, confidentiality + integrity   |
| Hashing                    | SHA-256, HMAC-SHA256     | Integrity, PoW puzzles               |
| Digital Signatures          | Ed25519                  | Federation governance + logs         |
| Transparency Proofs         | Merkle Trees             | Inclusion, consistency verification  |

**Future Upgrade:** Post-quantum crypto planned for v2.0.  

---

## 10. Abuse Prevention

### 10.1 Proof-of-Work Algorithm

VIREX employs a Hashcash-style **SHA-256 proof-of-work puzzle** to make large-scale spam economically costly while remaining inexpensive for legitimate users.

1. **Challenge:** The first-hop mixnode issues a 128-bit random challenge `C` that is included with the message payload.
2. **Puzzle:** The sender searches for a nonce `N` such that `SHA-256(C || payload || N)` has at least **22 leading zero bits**. This corresponds to a difficulty parameter `d = 22`.
3. **Expected Solve Time:** At this difficulty, a commodity CPU performs about \(2^{22}\) hash evaluations, yielding an average solve time of ~200 ms per message.
4. **Verification:** Upon receipt, nodes recompute the hash once and check that the output meets the difficulty target. Messages with invalid or missing PoW are discarded.
5. **Adaptive Difficulty:** Federation governance can raise or lower `d` to match network conditions.

### 10.2 Rate Limits

Nodes enforce per-sender quotas to prevent flooding attacks.

### 10.3 Auditing

Logs allow public detection of misbehavior or censorship.

---

## 11. Privacy Levels

| Level | Cover Traffic       | Latency Impact      | Use Case                              |
|-------|---------------------|---------------------|---------------------------------------|
| L1    | Minimal              | < 5 seconds         | Low-latency messaging                  |
| L2    | Moderate             | < 10 seconds        | Higher anonymity sets                  |
| L3    | Heavy (dummy fetches) | < 30 seconds        | Maximum metadata privacy               |

---

## 12. Limitations (Alpha)  

- No public testnet yet.  
- No production-ready implementation.  
- Post-quantum security not yet included.  

---

## 13. Roadmap  

- **v0.2.0-beta:** Minimal reference implementation in Rust, Go, .NET.  
- **v0.3.0-beta:** Public testnet with auditing tools and security tests.  
- **v1.0.0:** Stable specification and security audit.  
- **v2.0.0:** Post-quantum secure version with hybrid cryptography.  

---

## 14. License  

- **Specification:** Creative Commons Attribution 4.0 (CC BY 4.0)  
- **Code (future):** Apache License 2.0  

---
