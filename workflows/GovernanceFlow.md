
# VIREX Governance Flow – v0.1.0-alpha

**Author:** Syon Foppen  
**Status:** Alpha – for public feedback only  

---

## 1. Purpose  

This document describes how governance decisions are made in the VIREX protocol using a federated M-of-N model with transparency logs and auditor oversight.  

---

## 2. Participants  

| Participant            | Role                                                   |
|-------------------------|-------------------------------------------------------|
| Federation Members       | Vote on critical actions, hold signing keys           |
| Auditors                 | Verify logs, publish misbehavior reports              |
| Transparency Logs        | Store append-only records of all governance actions   |
| Node Operators           | Run mixnodes, mailbox nodes, or ODS servers           |
| Clients                  | Indirectly affected by governance decisions           |

---

## 3. High level steps  

1. A federation member creates a **governance proposal** (e.g., node onboarding, key rotation).  
2. Other federation members review the proposal and decide whether to sign it.  
3. A proposal becomes valid once **M-of-N threshold signatures** are collected.  
4. The approved proposal is appended to the **transparency logs** with Merkle proofs.  
5. Auditors verify the log entry and publish **checkpoints** for public validation.  

---

## 4. Sequence diagram  

TODO: Sequence diagram will be added in a future revision.  

---

## 5. Governance Actions  

| Action                   | Requires M-of-N | Logged in Transparency Logs | Auditor Verification |
|---------------------------|----------------|------------------------------|-----------------------|
| Node Onboarding           | Yes            | Yes                          | Yes                   |
| Node Removal              | Yes            | Yes                          | Yes                   |
| Key Rotations             | Yes            | Yes                          | Yes                   |
| ODS Root Updates          | Yes            | Yes                          | Yes                   |
| Parameter Changes         | Yes            | Yes                          | Yes                   |
| Auditor Checkpoints        | No             | Yes                          | Yes                   |

---

## 6. Security Considerations  

- All proposals require **threshold signatures** to prevent unilateral changes.  
- **Transparency logs** ensure append-only records and public accountability.  
- **Auditors** detect censorship or manipulation attempts.  
- **Key rotations** minimize long-term key compromise risk.  

---

## 7. Future Extensions  

- Automated governance with smart contracts or ZK proofs.  
- On-chain anchoring of transparency log roots.  
- Distributed key generation (DKG) for stronger key security.  

---

## 8. License  

Specification, CC BY 4.0  
Code in future implementations, Apache 2.0  
