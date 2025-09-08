# VIREX Auditor Guidelines – v0.1.0-alpha

**Author:** Syon Foppen  
**Status:** Alpha – for public feedback only  

---

## 1. Introduction  

Auditors in VIREX provide **independent oversight** of the network’s governance, transparency logs, and node behavior.  
They ensure that **no single operator or federation member** can act maliciously without detection.  

This document defines the **roles, responsibilities, processes, and technical guidelines** for VIREX auditors.

---

## 2. Auditor Goals  

1. **Verify Transparency Logs**  
   - Ensure logs are append-only and tamper-evident.  

2. **Detect Misbehavior**  
   - Identify nodes or federation members violating protocol rules.  

3. **Publish Evidence**  
   - Provide public, cryptographic proof of any detected misbehavior.  

4. **Cross-Check Federation Actions**  
   - Confirm M-of-N approvals for all governance decisions.  

5. **Enhance Public Trust**  
   - Make VIREX auditable and accountable to the community.  

---

## 3. Auditor Responsibilities  

| Responsibility                  | Description                                     |
|----------------------------------|-------------------------------------------------|
| Log Verification                 | Check inclusion & consistency proofs in logs.   |
| Node Behavior Monitoring         | Verify uptime, routing integrity, and performance. |
| Federation Action Verification   | Confirm M-of-N threshold signatures on proposals. |
| Public Reporting                  | Publish signed reports on log states and misbehavior. |
| Checkpoint Publication            | Issue periodic signed checkpoints for transparency. |

---

## 4. Log Verification Process  

Auditors verify logs using **Merkle Tree proofs**:  
- **Inclusion Proofs:** Verify that a specific action exists in the log.  
- **Consistency Proofs:** Verify that no rewriting or deletions occurred.  
- **Checkpoint Proofs:** Issue signed root hashes at fixed intervals for cross-verification.  

**Verification Interval:**  
- Minimum: Every 10 minutes (configurable)  
- Checkpoints published hourly for public consumption  

---

## 5. Node Behavior Auditing  

Auditors check:  
- **Uptime & Availability:** Ensure nodes meet minimum SLA requirements.  
- **Routing Integrity:** Detect if mixnodes drop, delay, or modify messages.  
- **Mailbox Privacy:** Verify constant-size responses and fixed polling intervals.  

---

## 6. Misbehavior Reporting  

### 6.1 Conditions for Reporting  
- Key tampering attempts  
- Censorship or message dropping  
- Forked transparency logs  
- Missing signatures on critical actions  

### 6.2 Evidence Requirements  
Reports must include:  
- Cryptographic proofs (Merkle branches, signatures)  
- Timestamps and log checkpoints  
- Node identifiers and public keys  

### 6.3 Publication Process  
- Reports signed by at least one independent auditor key  
- Published to public transparency channels  
- Federation notified for potential node suspension or removal  

---

## 7. Federation Cross-Checks  

Auditors verify that:  
- All governance actions meet **M-of-N signature thresholds**.  
- No single party bypasses federated approval rules.  
- Key rotations and node removals follow protocol procedures.  

---

## 8. Tooling & Automation  

Planned tools for auditors:  
- **CLI utilities** for log verification and checkpoint publication.  
- **Monitoring dashboards** for uptime and routing integrity.  
- **Zero-Knowledge Proof tools** (future) for privacy-preserving audits.  

---

## 9. Security Recommendations  

- Auditor keys stored on **HSMs** or secure enclaves.  
- Cross-signing between multiple auditors prevents single-point failures.  
- Audit results mirrored on **multiple public channels** for redundancy.  

---

## 10. Future Extensions  

- **Automated Auditing Agents:** Fully automated log verification and report generation.  
- **Distributed Auditor Networks:** Multiple independent organizations performing audits in parallel.  
- **Blockchain Anchoring:** Publishing checkpoints on public ledgers for immutability guarantees.  

---

## 11. License  

- **Specification:** Creative Commons Attribution 4.0 (CC BY 4.0)  
- **Code (future):** Apache License 2.0  

---
