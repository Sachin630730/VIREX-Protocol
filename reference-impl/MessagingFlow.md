
# VIREX Messaging Flow – v0.1.0-alpha

**Author:** Syon Foppen  
**Status:** Alpha – for public feedback only  

---

## 1. Introduction  

This document describes the **end-to-end messaging flow** in the VIREX protocol:  
- How a message travels from **Alice (sender)** to **Bob (recipient)**  
- Which protocol layers are involved  
- How **privacy**, **anonymity**, and **abuse prevention** are ensured  

---

## 2. Participants  

| Participant         | Role in the Flow                                        |
|---------------------|---------------------------------------------------------|
| Alice's Client       | Prepares message, encryption layers, PoW, sends to mixnet |
| Mixnodes (M1–M3)     | Apply onion routing, Poisson delays, dummy traffic       |
| ODS Servers          | Store public keys for anonymous lookup if needed        |
| Mailbox Nodes        | Store final encrypted message for Bob                   |
| Bob's Client         | Retrieves messages anonymously, decrypts final content  |
| Auditors & Federation| Oversee key integrity, node behavior, transparency logs |

---

## 3. Step-by-Step Message Flow  

1. Alice prepares message and requests Bob’s key from ODS anonymously.  
2. Encrypts the message using E2EE, wraps it in onion layers, solves PoW.  
3. Mixnodes forward the message through hops with Poisson delays and dummy traffic.  
4. Mailbox nodes store the encrypted message in fixed-size blocks.  
5. Bob polls mailbox nodes at fixed intervals, retrieves messages anonymously.  
6. Auditors verify transparency logs and federation actions.  

---

## 4. Sequence Diagram  

### 1. ODS Lookup Flow, anonymous key discovery
```MERMAID
sequenceDiagram

    %% Anonymous request through mixnet
    Alice->>M1: 1. ODS lookup request
    M1->>M2: 2. Forward after Poisson delay
    M2->>M3: 3. Forward after Poisson delay
    M3->>ODS: 4. Lookup recipient key

    %% Response and verification
    ODS-->>M3: 5. Key record, inclusion proof, root id
    M3-->>M2: 6. Return response
    M2-->>M1: 7. Return response
    M1-->>Alice: 8. Return response
    Alice->>Logs: 9. Fetch signed root checkpoint
    Logs-->>Alice: 10. Signed root with M of N signatures
```

### 2. Messaging Flow, end to end delivery
```MERMAID
%% Messaging Flow, end to end delivery
sequenceDiagram

    %% Send path
    Alice->>M1: 1. Send onion packet, includes PoW
    M1->>M2: 2. Forward after Poisson delay
    M2->>M3: 3. Forward after Poisson delay
    M3->>Mailbox: 4. Store encrypted message block

    %% Retrieve path
    Bob->>Mailbox: 5. Poll at fixed interval
    Mailbox-->>Bob: 6. Return constant size block
    Bob->>Bob: 7. Decrypt end to end payload

```

---

## 5. Privacy Guarantees  

| Threat                 | Mitigation in VIREX                  |
|------------------------|---------------------------------------|
| Sender-Recipient Linking | Multi-hop mixnet + dummy traffic      |
| Timing Correlation      | Poisson delays + fixed polling        |
| Key Replacement Attacks | ODS + Transparency Logs               |
| Spam / DoS              | Proof-of-Work + rate limiting         |
| Malicious Node Control  | Federation governance + auditing      |

---

## 6. Future Extensions  

- Adaptive cover traffic  
- Post-quantum cryptography  
- ZKP auditing  

---

## 7. License

Specification: CC BY 4.0  
Code in future implementations: Apache 2.0
