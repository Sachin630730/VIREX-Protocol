
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

### 1. Governance Flow, M of N approvals
```MERMAID
%% Governance Flow, M of N approvals
sequenceDiagram
    Member A->> Member A: 1. Draft proposal
    Member A->> Member B: 2. Request signature
    Member B-->> Member A: 3. Signature B
    Member A->> Member C: 4. Request signature
    Member C-->>Member A: 5. Signature C
    Member A->> Transparency Logs: 6. Submit proposal with signatures
    Transparency Logs -->>Auditors: 7. New checkpoint available
    Auditors->>Auditors: 8. Verify inclusion and consistency

```

### 2. Transparency Log Update, publishing new ODS root
```MERMAID
sequenceDiagram
    ODS Server->>Federation: 1. New ODS root, request co sign
    Federation-->>ODS Server: 2. M of N signatures
    ODS Server->>Transparency Logs: 3. Publish root with signatures
    Transparency Logs-->>Auditors: 4. Checkpoint ready
    Auditors->>Auditors: 5. Verify signatures and append only
```

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
