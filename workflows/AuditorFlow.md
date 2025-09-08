
# VIREX Auditor Flow – v0.1.0-alpha

**Author:** Syon Foppen  
**Status:** Alpha – for public feedback only  

---

## 1. Purpose  

This document describes the responsibilities and workflow of auditors in the VIREX protocol. Auditors ensure public verifiability, detect misbehavior, and provide checkpoints for federation governance transparency.  

---

## 2. Participants  

| Participant            | Role                                                   |
|-------------------------|-------------------------------------------------------|
| Auditors                | Verify logs, publish misbehavior reports               |
| Transparency Logs        | Store append-only records of governance actions        |
| Federation Members       | Respond to misbehavior reports, rotate keys if needed |
| Node Operators           | Operate mixnodes, mailbox nodes, or ODS servers        |
| Clients                  | Rely on public checkpoints for trust decisions        |

---

## 3. High level steps  

1. Auditors regularly fetch and verify **transparency logs** for governance actions.  
2. They generate **checkpoints** signed with their own keys for public distribution.  
3. They detect and report **misbehavior** (e.g., censorship, forking, key tampering).  
4. Reports include **cryptographic proofs** like Merkle branches and signatures.  
5. Federation responds by suspending or removing malicious nodes if needed.  

---

## 4. Sequence diagram  

TODO: Sequence diagram will be added in a future revision.  

---

## 5. Auditor Responsibilities  

| Responsibility             | Description                                        |
|-----------------------------|----------------------------------------------------|
| Log Verification            | Check inclusion & consistency proofs in logs       |
| Node Monitoring             | Monitor uptime, routing integrity, availability    |
| Federation Action Validation| Confirm M-of-N signatures on all proposals         |
| Misbehavior Reporting        | Publish signed reports for public inspection      |
| Checkpoint Publication       | Publish signed log root checkpoints periodically  |

---

## 6. Misbehavior Detection Examples  

- **Key Tampering**: Detects unauthorized key replacements in ODS logs  
- **Censorship**: Detects removal or withholding of proposals in logs  
- **Forked Logs**: Detects divergence in transparency logs via checkpoints  
- **Malicious Nodes**: Reports nodes with uptime or routing integrity failures  

---

## 7. Security Recommendations  

- Auditors should store private keys in **HSMs** or secure enclaves.  
- Multiple auditors should cross-sign checkpoints to avoid single points of failure.  
- All reports should include cryptographic evidence for reproducibility.  
- Auditors should be independent and geographically distributed.  

---

## 8. Future Extensions  

- Automated auditing agents for real-time log verification.  
- Zero-knowledge proofs for privacy-preserving misbehavior reports.  
- Public dashboards showing real-time log consistency status.  

---

## 9. License  

Specification, CC BY 4.0  
Code in future implementations, Apache 2.0  
