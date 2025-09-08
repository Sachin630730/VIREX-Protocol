
# VIREX Network Join Flow – v0.1.0-alpha

**Author:** Syon Foppen  
**Status:** Alpha – for public feedback only  

---

## 1. Purpose  

This document describes the process for new nodes (mixnodes, mailbox servers, ODS servers) to join the VIREX network under federation governance rules with transparency and security guarantees.  

---

## 2. Participants  

| Participant            | Role                                                   |
|-------------------------|-------------------------------------------------------|
| Node Operator            | Requests to join the network                          |
| Federation Members       | Approve or reject join requests via M-of-N signatures |
| Transparency Logs        | Store all join decisions for public verification      |
| Auditors                 | Verify the integrity of join actions and logs         |
| Existing Nodes           | Update routing tables after new node onboarding       |

---

## 3. High level steps  

1. Node operator generates a key pair and submits a **join request** to federation members.  
2. Federation reviews the request, checking security, availability, and operator trustworthiness.  
3. If approved by **M-of-N signatures**, the join request is added to **transparency logs**.  
4. Existing nodes update their routing tables to include the new node.  
5. Auditors verify the process and publish checkpoints for public trust.  

---

## 4. Sequence diagram  

TODO: Sequence diagram will be added in a future revision.  

---

## 5. Requirements for New Nodes  

- Must meet minimum uptime and security requirements.  
- Must provide operational information (bandwidth, region, operator ID).  
- Must run approved VIREX software with regular updates applied.  

---

## 6. Federation Approval  

- Federation uses **M-of-N threshold signatures** to approve join requests.  
- Approval events logged in **transparency logs** for accountability.  
- Auditors monitor for suspicious or malicious onboarding patterns.  

---

## 7. Security Considerations  

- Prevent Sybil attacks by requiring federation approval for every node.  
- Monitor node behavior post-join to ensure compliance with rules.  
- Support fast removal if a node becomes malicious or compromised.  

---

## 8. Future Extensions  

- Automated node onboarding with zero-knowledge proofs.  
- Reputation-based scoring for faster approvals of known operators.  
- Smart contract integration for decentralized governance.  

---

## 9. License  

Specification, CC BY 4.0  
Code in future implementations, Apache 2.0  
