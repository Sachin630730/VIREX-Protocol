# VIREX Transparency Logs – v0.1.0-alpha

**Author:** Syon Foppen  
**Status:** Alpha – for public feedback only  

---

## 1. Introduction  

Transparency logs in VIREX ensure that **all critical governance actions** are **publicly verifiable** and **tamper-evident**.  

They provide:  
- **Cryptographic integrity**: No rewriting of history.  
- **Public accountability**: Auditors and the public can verify all actions.  
- **Trust minimization**: Federation members cannot secretly change system state.  

---

## 2. Design Goals  

1. **Append-only:** Once written, actions cannot be removed or modified.  
2. **Public Verifiability:** Anyone can check correctness using cryptographic proofs.  
3. **Federated Trust:** M-of-N approvals prevent unilateral modifications.  
4. **Efficiency:** Proofs are compact and easy to verify.  
5. **Auditability:** Independent auditors can cross-check logs for misbehavior detection.  

---

## 3. Data Structure  

- Logs are implemented as **Merkle Trees**:  
  - Each leaf = hash of a governance action.  
  - Each internal node = hash of its child nodes.  
  - **Merkle root** = cryptographic fingerprint of the entire log state.  

- Every new action creates a **new root hash**.  
- Old states remain verifiable via **consistency proofs**.  

---

## 4. Logged Actions  

| Action Type           | Description                                       | Requires M-of-N Approval |
|-----------------------|---------------------------------------------------|---------------------------|
| Federation Onboarding | Adding new node operators or auditors              | Yes                       |
| Node Removal           | Removing misbehaving or compromised nodes         | Yes                       |
| Key Rotations          | Rotating keys for nodes or federation members     | Yes                       |
| ODS Root Updates       | Publishing new ODS Merkle Tree root hashes        | Yes                       |
| Governance Proposals   | Adding proposals for voting or future extensions  | Yes                       |
| Transparency Checkpoints | Auditors publishing log consistency checkpoints | No                        |

---

## 5. Proof Types  

1. **Inclusion Proofs**  
   - Verify that a specific action exists in the log.  
   - Uses **Merkle branch** from leaf to root for efficient verification.  

2. **Consistency Proofs**  
   - Verify that the log grew append-only between two checkpoints.  
   - Prevents deletion or rewriting of history.  

3. **Checkpoint Proofs**  
   - Auditors periodically publish **signed root hashes** for cross-verification.  

---

## 6. Federation Integration  

- **M-of-N threshold signatures** required for each logged action.  
- Log entries include:  
  - Timestamp  
  - Action type  
  - Signatures from federation members  
  - Cryptographic hash chain linking to previous state  

Example structure for each entry:  
```JSON
{
    "timestamp": "2025-09-08T12:00:00Z",
    "action_type": "KeyRotation",
    "details": { "node_id": "mixnode-12", "new_key": "ed25519:..." },
    "signatures": [sig1, sig2, sig3],
    "prev_root": "hash_of_previous_root",
    "new_root": "hash_of_current_root"
}
```
---

## 7. Auditor Responsibilities  

Auditors must:  
- Verify **inclusion proofs** for new actions.  
- Publish **consistency checkpoints** at regular intervals.  
- Detect and report any **forked or inconsistent logs**.  
- Sign and publish **audit reports** for public verification.  

---

## 8. Security Considerations  

- Logs are **append-only**: Merkle root changes require M-of-N approval.  
- **Cross-signing** by auditors prevents hidden log forks.  
- Public proofs make malicious modifications **detectable** even if some federation members collude.  

---

## 9. Future Extensions  

- **Distributed Log Shards:** For scalability and regional redundancy.  
- **Zero-Knowledge Proofs:** Privacy-preserving audit proofs for sensitive actions.  
- **Cross-Chain Anchoring:** Optional publication of root hashes on public blockchains for stronger immutability guarantees.  

---

## 10. License  

- **Specification:** Creative Commons Attribution 4.0 (CC BY 4.0)  
- **Code (future):** Apache License 2.0  

---