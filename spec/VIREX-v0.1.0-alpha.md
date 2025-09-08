# VIREX Protocol Specification – v0.1.0-alpha  

**Version:** v0.1.0-alpha  
**Status:** Alpha – for public feedback only  
**Author:** Syon Foppen  

---

## 1. Introduction  

VIREX (**Verifiable Infrastructure for Routing with Encryption and eXtensibility**) is a **privacy-preserving communication protocol** designed as a **learning project** to explore modern cryptography, mixnet routing, metadata protection, and federated Governance.  

This specification defines the **core concepts, architecture, and security goals** of VIREX in its alpha version.  

**Disclaimer:**  
- This is an **alpha draft** for **educational purposes**.  
- **Not for production use**.  
- Subject to change based on **public review** and **security feedback**.  

---

## 2. Goals and Principles  

1. **End-to-End Encryption (E2EE):** All messages must be encrypted between sender and recipient.  
2. **Metadata Privacy:** Minimize leakage of who talks to whom, when, and how often.  
3. **Abuse Resistance:** Prevent spam, flooding, and malicious nodes from disrupting the system.  
4. **Federated Governance:** No single entity controls the network; trust is distributed.  
5. **Transparency:** Auditable logs to detect malicious behavior or misconfigurations.  
6. **Extensibility:** Future-proof design for post-quantum cryptography and advanced features.  

---

## 3. Threat Model (High-Level)  

VIREX assumes:  
- **Adversaries** may control parts of the network but **not all mixnodes** simultaneously.  
- **Global passive adversaries** can observe traffic but cannot decrypt message layers.  
- Attackers may attempt **traffic correlation**, **denial-of-service**, or **key spoofing**.  

Out of scope for alpha:  
- Post-quantum adversaries (planned for future versions).  
- Side-channel and endpoint compromises.  

---

## 4. Protocol Architecture  

VIREX consists of the following layers:  

1. **Mixnet Layer:**  
   - Multi-hop routing with layered encryption (onion-style).  
   - Poisson delays and dummy traffic prevent timing analysis.  
   - Each mixnode sees only the next hop, never the full route.  

2. **End-to-End Encryption Layer:**  
   - Sender encrypts the message for the recipient using ephemeral keys.  
   - Provides **Perfect Forward Secrecy (PFS)**.  

3. **Oblivious Directory Service (ODS):**  
   - Public, auditable key directory with Merkle Tree proofs.  
   - Supports anonymous lookups via the mixnet.  

4. **Mailbox Layer:**  
   - Recipients fetch messages at fixed intervals with constant-size responses.  
   - Prevents metadata leaks about when messages are read.  

5. **Governance & Auditing Layer:**  
   - Federated control via threshold signatures.  
   - Transparency logs detect key tampering or misbehavior.  

---

## 5. Cryptographic Primitives  

| Purpose                    | Algorithm (Alpha)         | Notes                                    |
|----------------------------|----------------------------|-------------------------------------------|
| Key Exchange                | X25519                     | Ephemeral per session                     |
| Encryption                  | ChaCha20-Poly1305          | AEAD for confidentiality + integrity      |
| Hashing                     | SHA-256, HMAC-SHA256       | For PoW and integrity checks               |
| Transparency Logs           | Merkle Trees               | Inclusion and consistency proofs           |
| Signatures                  | Ed25519                    | Governance and log signing                  |

**Future Versions:**  
- Post-quantum cryptography (Kyber, Dilithium) in v2.0 planned.  

---

## 6. Message Lifecycle  

1. **Sender Prepares Message:**  
   - Encrypts payload for recipient using E2EE.  
   - Wraps in multiple encryption layers for each mixnode.  

2. **Mixnet Processing:**  
   - Each node strips one layer and forwards after random delay.  
   - Dummy traffic ensures constant load.  

3. **Mailbox Storage:**  
   - Final node stores message in recipient’s mailbox.  
   - Fixed-size blocks prevent traffic analysis.  

4. **Recipient Retrieval:**  
   - Recipient fetches blocks at fixed intervals, real or dummy.  
   - Decrypts payload using E2EE keys.  

---

## 7. Abuse Prevention

- **Proof-of-Work (PoW):** Each message requires solving a small computational puzzle. See [Deep Dive §10.1](VIREX-DeepDive.md#101-proof-of-work-algorithm) for algorithm details.
- **Rate Limits:** Nodes enforce per-sender quotas to prevent flooding.
- **Auditing:** Independent auditors verify logs, routing behavior, and key directories.

---

## 8. Governance Model

- **Federated Nodes:** Multiple independent operators run mixnodes and directories.  
- **FROST Threshold Signatures:** Critical actions (e.g., key revocation) require M-of-N approval. See [governance/Governance.md](../governance/Governance.md).  
- **Transparency Logs:** Publicly auditable, append-only logs detect malicious changes.  

---

## 9. Community Peers & Federation  

### 9.1 Node Operators  
- Anyone can run a **mixnode** or **mailbox node**.  
- Registration requires:  
  - **Key pair** (Ed25519)  
  - **Proof-of-Work** or **staking** (in later versions)  
  - Approval via **threshold signatures** of federation members  

### 9.2 Federation Governance  
- No central authority; governance controlled by **M-of-N keys**.  
- Threshold approvals required for:  
  - Key rotations  
  - Transparency log root updates  
  - Node suspension or revocation  

### 9.3 Peer Discovery  
- Nodes use a **gossip protocol** or **signed directory snapshots** for discovery.  
- Clients receive a **signed list of nodes** with public keys and uptime metadata.  

### 9.4 Reputation and Auditing  
- Misbehaving nodes publicly flagged in transparency logs.  
- Federation can suspend or revoke nodes based on public audits.  

### 9.5 Community Participation  
- Open to anyone but with **auditor oversight** to prevent abuse.  
- Ensures a balance between **openness** and **security guarantees**.  

---

## 10. Privacy Levels  

| Level | Cover Traffic       | Latency Impact      | Use Case                              |
|-------|---------------------|---------------------|---------------------------------------|
| L1    | Minimal              | < 5 seconds         | Low-latency messaging                  |
| L2    | Moderate             | < 10 seconds        | Higher anonymity sets                  |
| L3    | Heavy (dummy fetches) | < 30 seconds        | Maximum metadata privacy               |

---

## 11. Security Considerations  

- Multi-hop encryption prevents any single node from linking sender and recipient.  
- Transparency logs prevent key tampering or silent revocations.  
- Dummy traffic and Poisson delays resist timing analysis attacks.  
- Governance federation prevents single-operator compromise.  

---

## 12. Limitations (Alpha)  

- No reference implementation yet (planned for v0.2.0-beta).  
- Not post-quantum secure in v0.1.0-alpha.  
- No public testnet until after security review.  

---

## 13. Future Roadmap  

- **v0.2.0-beta:** Reference implementations in Rust, Go, .NET.  
- **v0.3.0-beta:** Public testnet, conformance tests, security fuzzing.  
- **v1.0.0:** Stable specification, security audits, production readiness.  
- **v2.0.0:** Hybrid post-quantum cryptography support.  

---

## 14. License  

- **Specification:** Creative Commons Attribution 4.0 (CC BY 4.0)  
- **Code (future):** Apache License 2.0  

---
