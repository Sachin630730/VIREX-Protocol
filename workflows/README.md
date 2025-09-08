# VIREX Workflows – v0.1.0-alpha

**Author:** Syon Foppen  
**Status:** Alpha – for public feedback only  

---

## Overview  

The `workflows/` folder contains step-by-step process documentation for all major workflows in the VIREX protocol.  
Each document explains **how protocol components interact**, including clients, mixnodes, mailbox servers, ODS, federation governance, auditors, and abuse prevention mechanisms.  

---

## Recommended Reading Order  

1. **MessagingFlow.md**  
   - Describes how messages travel from sender to recipient via the mixnet, mailboxes, and auditors.  

2. **KeyLookupFlow.md**  
   - Explains anonymous key lookups via the Oblivious Directory Service (ODS).  

3. **KeyRotationFlow.md**  
   - Details how clients rotate public keys with federation approval and transparency logs.  

4. **GovernanceFlow.md**  
   - Details the M-of-N federated governance process for node onboarding, key rotations, and log updates.  

5. **AuditorFlow.md**  
   - Defines the responsibilities of auditors in verifying logs, detecting misbehavior, and publishing checkpoints.  

6. **AbusePreventionFlow.md**  
   - Shows how Proof-of-Work, rate limiting, and federation rules prevent spam and DoS attacks.  

7. **NetworkJoinFlow.md**  
   - Explains how new nodes join the network under federation approval and transparency requirements.  

8. **FailureRetryFlow.md**  
   - Describes fallback strategies if nodes fail or drop packets, including randomized retries and alternate routes.  

---

## File Descriptions  

| File                     | Purpose                                                     |
|--------------------------|-------------------------------------------------------------|
| MessagingFlow.md          | End-to-end message flow with privacy guarantees             |
| KeyLookupFlow.md          | Anonymous public key lookups with ODS and transparency logs |
| KeyRotationFlow.md        | Key rotation with federation approval and log transparency  |
| GovernanceFlow.md         | Federated M-of-N decision making and log updates            |
| AuditorFlow.md            | Auditor responsibilities, checkpoints, and misbehavior logs |
| AbusePreventionFlow.md    | PoW, rate limiting, and abuse prevention mechanisms         |
| NetworkJoinFlow.md        | Node onboarding and approval process                        |
| FailureRetryFlow.md       | Retries, alternate routes, and fault tolerance strategies    |

---

## Future Additions  
- **Advanced Scenarios:** Examples for journalists, whistleblowers, and NGOs.  
- **Automated Auditing:** Flows for future ZKP-based auditing systems.  

---

## License  

Specification: CC BY 4.0  
Code in future implementations: Apache 2.0  
