
# VIREX Abuse Prevention Flow – v0.1.0-alpha

**Author:** Syon Foppen  
**Status:** Alpha – for public feedback only  

---

## 1. Purpose  

This document describes how VIREX prevents abuse, such as spam, denial-of-service attacks, or Sybil attacks, using Proof-of-Work, rate limiting, and federation oversight.  

---

## 2. Participants  

| Participant            | Role                                                   |
|-------------------------|-------------------------------------------------------|
| Clients                  | Solve PoW challenges before sending messages          |
| Mixnodes                 | Enforce rate limiting, verify PoW                     |
| Federation Members       | Update PoW parameters, enforce abuse mitigation rules |
| Transparency Logs        | Store configuration changes for public accountability |
| Auditors                 | Verify that abuse prevention measures are enforced    |

---

## 3. High level steps  

1. A client requests to send a message through the VIREX network.  
2. The network requires the client to solve a **Proof-of-Work** challenge.  
3. Mixnodes verify the PoW solution before accepting the message.  
4. Rate limiting ensures clients cannot exceed allowed traffic volumes.  
5. Federation members can update difficulty or thresholds via M-of-N decisions logged publicly.  
6. Auditors verify enforcement by analyzing logs and message acceptance statistics.  

---

## 4. Sequence diagram  

```MERMAID
%% Abuse Prevention Flow, PoW and rate limiting
sequenceDiagram
    Client->>Mixnode A: 1. Submit message plus PoW
    Mixnode A->>Mixnode A: 2. Verify PoW and rate limit
    alt Invalid or over limit
        Mixnode A-->>Client: 3. Reject with backoff
    else Accepted
        Mixnode A-->>Client: 3. Accepted
    end
    Federation->>Transparency Logs: 4. Update PoW parameters, M of N
    Transparency Logs-->>Auditors: 5. New config checkpoint
    Auditors->>Auditors: 6. Verify and publish notice
```  

---

## 5. Abuse Prevention Mechanisms  

| Mechanism            | Purpose                                         |
|----------------------|-------------------------------------------------|
| Proof-of-Work (PoW)   | Makes large-scale spamming economically costly   |
| Rate Limiting         | Prevents flooding even with valid PoW tokens     |
| Federation Oversight  | Allows parameter changes under M-of-N approvals |
| Auditing              | Ensures fairness and transparency               |

---

## 6. PoW Parameters  

- Adjustable difficulty to balance security vs. usability  
- Federation can change difficulty via M-of-N approvals  
- Parameters logged for public verifiability  

---

## 7. Rate Limiting Details  

- Per-client message limits enforced at mixnodes  
- Exponential backoff for clients exceeding limits  
- Metrics published for auditors to verify enforcement  

---

## 8. Security Considerations  

- Prevent attackers from bypassing PoW with pre-computation attacks  
- Ensure rate limits do not leak metadata about client activity  
- Use cover traffic to mask real vs. dummy traffic patterns  

---

## 9. Future Extensions  

- Dynamic difficulty adjustment based on network load  
- Reputation systems for well-behaved clients  
- Integration with zero-knowledge proofs for anonymous abuse prevention  

---

## 10. License  

Specification, CC BY 4.0  
Code in future implementations, Apache 2.0  
