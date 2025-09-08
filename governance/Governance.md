# VIREX Governance Model – v0.1.0-alpha

**Author:** Syon Foppen  
**Status:** Alpha – for public feedback only  

---

## 1. Introduction  

VIREX is designed as a **federated system**:  
- No single entity controls the entire network.  
- Critical actions require **multi-party approvals (M-of-N)**.  
- **Transparency logs** provide public verifiability for all governance actions.  

This document describes the **roles**, **processes**, and **cryptographic mechanisms** for governance in VIREX.  

---

## 2. Governance Goals  

1. **Distributed Trust:** No central authority can compromise the network.  
2. **Accountability:** All decisions are publicly auditable.  
3. **Resilience:** Governance continues even if some operators fail or act maliciously.  
4. **Security:** Strong cryptography prevents unilateral or unauthorized actions.  
5. **Openness:** New node operators can join under clear, transparent rules.  

---

## 3. Governance Roles  

| Role                  | Responsibilities                                                       |
|-----------------------|-------------------------------------------------------------------------|
| **Federation Members** | Operate mixnodes, mailbox nodes, and ODS servers under governance rules. |
| **Auditors**           | Verify transparency logs, publish misbehavior reports.                  |
| **Key Holders**        | Hold shares of threshold signing keys for approvals.                    |
| **Community Peers**    | Independent node operators participating in the VIREX network.          |

---

## 4. Federated Decision-Making  

### 4.1 Threshold Signatures
- **M-of-N model:** At least M independent signatures required for critical actions.
- Example:
  - 5 federation members total.
  - M = 3 required for valid approval.
- Uses **FROST** over **Ed25519** for threshold signatures ([IETF draft](https://www.ietf.org/archive/id/draft-irtf-cfrg-frost-16.html), [Zcash reference implementation](https://github.com/ZcashFoundation/frost)).
- **Aggregation example:** Members A, C, and E produce partial signatures. An aggregator combines them into a single Ed25519 signature, which any peer verifies against the group public key like a normal Ed25519 signature.

### 4.2 Key Lifecycle

#### Key Generation
- Federation members run a distributed key generation (DKG) protocol for FROST, deriving a shared public key and private key shares without ever constructing the full secret key.

#### Share Distribution
- Each member receives its share over authenticated secure channels and stores it in hardened hardware (e.g., HSM). Commitments to the generated shares are recorded in transparency logs for later auditing.

#### Rotation
- Keys are rotated periodically or when membership changes by rerunning the DKG. Old shares are securely destroyed and a new group public key is logged for auditors.

### 4.3 Actions Requiring Threshold Approval
- Adding or removing federation members.  
- Updating ODS root hashes in transparency logs.  
- Rotating signing keys for nodes or directories.  
- Revoking misbehaving or compromised nodes.  

### 4.4 Governance Workflow

1. **Proposal:** Federation member creates a governance action request.  
2. **Review:** Other members verify request validity.  
3. **Signatures:** Members co-sign the action until M-of-N threshold is met.  
4. **Execution:** Signed action is appended to **transparency logs**.  

---

## 5. Transparency Logs  

- **Append-only Merkle Trees** store all governance actions.  
- Each action includes:  
  - Type of action (e.g., key rotation, node removal)  
  - Timestamp  
  - Signatures from federation members  
  - Cryptographic hash linking to previous state  

Auditors verify:  
- **Consistency proofs**: No rewriting of log history.  
- **Inclusion proofs**: Actions are publicly visible and verifiable.  

---

## 6. Federation Membership  

### 6.1 Requirements  
- Operate at least one core VIREX service: mixnode, mailbox, or ODS.  
- Generate an **Ed25519 key pair** for signing and authentication.  
- Pass initial vetting by existing federation members.  

### 6.2 Onboarding Process  
1. New node operator requests federation membership.  
2. Existing members review operational and security capabilities.  
3. M-of-N approval required for admission.  
4. Admission event added to **transparency logs**.  

### 6.3 Removal or Suspension  
- Federation can remove members for:  
  - Proven misbehavior  
  - Key compromise  
  - Operational failure  
- Removal also requires M-of-N approval and is **publicly logged**.  

---

## 7. Auditor Role  

Auditors are independent entities monitoring:  
- Node uptime and performance  
- Log consistency and key rotations  
- Potential censorship or malicious behavior  

Auditors publish:  
- **Misbehavior reports** with cryptographic evidence  
- **Transparency log checkpoints** for public verification  

---

## 8. Security Considerations  

- Federation keys stored securely with **hardware security modules (HSMs)** recommended.  
- Regular **key rotations** prevent long-term compromise.  
- **Multi-party approvals** mitigate insider threats and single-point failures.  

---

## 9. Future Roadmap  

- **Automated Governance Tools:** Smart contract or zero-knowledge based approvals (v1.0.0).  
- **Advanced Auditing:** Zero-knowledge proofs for censorship resistance (v2.0.0).  
- **Economic Incentives:** Optional staking or reputation systems for node operators (future research).  

---

## 10. License  

- **Specification:** Creative Commons Attribution 4.0 (CC BY 4.0)  
- **Code (future):** Apache License 2.0  

---
