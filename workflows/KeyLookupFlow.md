
# VIREX Key Lookup Flow, v0.1.0-alpha

**Author:** Syon Foppen  
**Status:** Alpha, for public feedback only  

---

## 1. Purpose  

This document describes how a client retrieves a recipient's public key using the Oblivious Directory Service, ODS, without revealing who they are searching for. It also explains how transparency logs and federation approvals protect against key replacement attacks.  

---

## 2. Participants  

| Participant            | Role                                                   |
|-------------------------|-------------------------------------------------------|
| Client                  | The requester that needs the recipient's public key   |
| Mixnodes                | Provide anonymous transport for the lookup request    |
| ODS Server              | Serves key records and Merkle proofs                  |
| Transparency Logs       | Store append-only checkpoints of ODS roots            |
| Auditors and Federation | Publish checkpoints, verify consistency, approve rotations |

---

## 3. High level steps  

1. Client prepares an anonymous lookup request, optionally via the mixnet to hide network metadata.  
2. Client queries ODS for recipient handle or identifier and requests:  
   - Current public key record  
   - Inclusion proof in the current Merkle root  
   - Signed root checkpoint reference  
3. ODS returns the key record, inclusion proof, and the latest signed root or a pointer to it.  
4. Client verifies:  
   - Signature on the ODS root by the federation, M of N  
   - Inclusion proof binds the returned key record into that root  
   - Optional consistency proof from a previous known checkpoint, to ensure append-only growth  
5. If verification succeeds, the client caches the key with its associated root and validity window, then proceeds with end-to-end encryption.  

---

## 4. Sequence diagram  

### 1. ODS Lookup Flow, anonymous key discovery
```MERMAID
sequenceDiagram

    %% Anonymous request through mixnet
    Alice Client->>Mixnode A: 1. ODS lookup request
    Mixnode A->>Mixnode B: 2. Forward after Poisson delay
    Mixnode B->>Mixnode C: 3. Forward after Poisson delay
    Mixnode C->>ODS Server: 4. Lookup recipient key

    %% Response and verification
    ODS Server-->>Mixnode C: 5. Key record, inclusion proof, root id
    Mixnode C-->>Mixnode B: 6. Return response
    Mixnode B-->>Mixnode A: 7. Return response
    Mixnode A-->>Alice Client: 8. Return response
    Alice Client->>Transparency Logs: 9. Fetch signed root checkpoint
    Transparency Logs-->>Alice Client: 10. Signed root with M of N signatures
```
---

## 5. Returned data structures, conceptual format  
```JSON
{
  "key_record": {
    "subject": "bob@example",
    "algo": "ed25519",
    "public_key": "base64, or multibase",
    "valid_from": "2025-09-08T10:00:00Z",
    "valid_to": "2026-09-08T10:00:00Z",
    "revocations": [],
    "metadata": {
      "usage": ["messaging", "virex e2ee"],
      "policy": "rotate every 90 days"
    }
  },
  "proof": {
    "type": "merkle inclusion",
    "leaf_hash": "hex",
    "branch": ["hex", "hex"],
    "root_hash": "hex",
    "root_id": "ods root checkpoint id"
  },
  "checkpoint": {
    "root_hash": "hex",
    "tree_size": 123456,
    "timestamp": "2025-09-08T10:00:02Z",
    "signatures": [
      {"member": "orgA", "sig": "base64"},
      {"member": "orgB", "sig": "base64"},
      {"member": "orgC", "sig": "base64"}
    ],
    "threshold": {"m": 3, "n": 5}
  }
}
```
---

## 6. Verification rules, client side  

- The checkpoint must carry at least M signatures from distinct federation members, where M of N complies with the current governance policy.  
- The inclusion proof must validate that the key record leaf commits to the exact fields returned, including subject, algorithm, public key, validity window, and policy metadata.  
- If the client already trusts an older checkpoint, it should verify a consistency proof from old root to new root. If the proof fails, the client must treat the directory as untrusted until auditors clarify.  
- The client should pin, cache, and age out keys according to the validity window and rotation policy. On rotation, clients should fetch a fresh record and proofs.  

---

## 7. Privacy considerations  

- Use the mixnet for ODS lookups to avoid leaking the target of the lookup to network observers.  
- Batch and pad ODS responses so record sizes do not reveal algorithm or metadata differences.  
- Rate limit and require lightweight proof of work for ODS queries to prevent abuse and enumeration.  
- Support negative lookups with indistinguishable responses, for example a dummy record plus proof of non-inclusion pattern, planned for a future version.  

---

## 8. Failure cases and client behavior  

| Failure                                     | Client action                                                |
|---------------------------------------------|-------------------------------------------------------------|
| Missing or invalid federation signatures     | Reject response, retry with different ODS replica, alert user |
| Inclusion proof does not validate            | Reject, escalate to auditors if repeated                     |
| Consistency proof fails from prior checkpoint| Treat directory as forked, pin old root, fetch auditor checkpoints |
| Expired key record                            | Request latest record, or halt with warning                  |
| Algorithm mismatch with policy                | Refuse to use key, request compatible record                 |

---

## 9. Security notes  

- ODS servers must be stateless with respect to the requester identity. No per requester logs beyond aggregate counters.  
- All checkpoints and proofs should be reproducible from public data so auditors can verify independently.  
- Federation private keys should be stored in HSMs, and rotations should be regular, for example every 6 months.  
- Clients should implement back off and randomization on retries to avoid creating timing beacons.  

---

## 10. License  

Specification, CC BY 4.0  
Code in future implementations, Apache 2.0  
