
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

3. **GovernanceFlow.md**  
   - Details the M-of-N federated governance process for node onboarding, key rotations, and log updates.  

4. **AuditorFlow.md**  
   - Defines the responsibilities of auditors in verifying logs, detecting misbehavior, and publishing checkpoints.  

5. **AbusePreventionFlow.md**  
   - Shows how Proof-of-Work, rate limiting, and federation rules prevent spam and DoS attacks.  

6. **NetworkJoinFlow.md**  
   - Explains how new nodes join the network under federation approval and transparency requirements.  

---

## File Descriptions  

| File                     | Purpose                                                     |
|--------------------------|-------------------------------------------------------------|
| MessagingFlow.md          | End-to-end message flow with privacy guarantees             |
| KeyLookupFlow.md          | Anonymous public key lookups with ODS and transparency logs |
| GovernanceFlow.md         | Federated M-of-N decision making and log updates            |
| AuditorFlow.md            | Auditor responsibilities, checkpoints, and misbehavior logs |
| AbusePreventionFlow.md    | PoW, rate limiting, and abuse prevention mechanisms         |
| NetworkJoinFlow.md        | Node onboarding and approval process                        |

---

## Future Additions  

- **Sequence Diagrams:** Will be added for each workflow document.  
- **Advanced Scenarios:** Examples for journalists, whistleblowers, and NGOs.  
- **Automated Auditing:** Flows for future ZKP-based auditing systems.  

---

## License  

Specification: CC BY 4.0  
Code in future implementations: Apache 2.0  
