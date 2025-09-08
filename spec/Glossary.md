# VIREX Protocol – Glossary (v0.1.0-alpha)

**Author:** Syon Foppen  
**Status:** Alpha – for public feedback only  

---

## A  

**AEAD (Authenticated Encryption with Associated Data)**  
An encryption scheme that provides both **confidentiality** (data is hidden) and **integrity** (data cannot be modified undetected). VIREX uses **ChaCha20-Poly1305** as its AEAD primitive.  

**Auditors**  
Independent parties verifying the integrity of **transparency logs**, **node behavior**, and **governance decisions** in VIREX.  

---

## C  

**ChaCha20-Poly1305**  
The chosen AEAD cipher in VIREX, offering high performance and strong security guarantees.  

**Client**  
The software or user interacting with the VIREX network to send or receive messages.  

**Community Peers**  
Independent node operators running **mixnodes**, **mailbox servers**, or **directory services** under federated governance.  

**Cover Traffic**  
Dummy traffic injected into the network to prevent adversaries from learning real traffic patterns.  

**Cryptographic Primitives**  
The core algorithms (e.g., X25519, Ed25519, SHA-256) providing security guarantees in VIREX.  

---

## D  

**Dummy Messages**  
Fake messages inserted into the network to obscure real message patterns and resist traffic analysis.  

**Directory Service (ODS)**  
Oblivious Directory Service storing recipients' public keys in a transparent, auditable, and anonymous manner.  

---

## E  

**End-to-End Encryption (E2EE)**  
Encryption where only the **sender** and **recipient** can read the message content, even if intermediaries see the data.  

**Ephemeral Keys**  
Short-lived keys used for **Perfect Forward Secrecy (PFS)**; compromise of one key does not compromise past sessions.  

---

## F  

**Federation**  
The distributed governance model in VIREX where multiple independent entities control network infrastructure and critical decisions.  

**Forward Secrecy**  
A property ensuring past messages remain confidential even if long-term keys are later compromised.  

---

## G  

**Governance Layer**  
The part of VIREX responsible for **node admission**, **key rotations**, and **auditor oversight**, secured by **threshold cryptography**.  

**Gossip Protocol**  
A peer discovery mechanism where nodes exchange signed information about other nodes in a decentralized way.  

---

## H  

**HMAC (Hash-Based Message Authentication Code)**  
Used in VIREX for integrity checks and **Proof-of-Work puzzles**.  

**Hybrid Post-Quantum Cryptography**  
Planned for future versions, combining classical cryptography with post-quantum algorithms for long-term security.  

---

## K  

**Key Transparency**  
Mechanism ensuring **public keys** cannot be maliciously replaced without detection, using **Merkle Trees** and **auditable logs**.  

---

## M  

**Mailbox Nodes**  
Servers storing encrypted messages until recipients fetch them at fixed intervals to prevent timing attacks.  

**Merkle Tree**  
Data structure allowing efficient proofs of **data inclusion** and **log consistency**. Used for **transparency logs** and **ODS proofs**.  

**Mixnet**  
A network where messages are **mixed**, encrypted in multiple layers, and delayed randomly to resist traffic analysis.  

---

## N  

**Node Operator**  
Any participant running a VIREX node (mixnode, mailbox, or directory).  

**Nonce**  
A unique value used in encryption to prevent replay attacks and ensure message uniqueness.  

---

## O  

**Oblivious Directory Service (ODS)**  
VIREX’s system for secure, anonymous, and auditable public key lookups.  

**Onion Routing**  
Layered encryption where each intermediate node decrypts one layer, learning only the next hop, not the full path or message.  

---

## P  

**Peer Discovery**  
Process through which nodes and clients learn about available network participants via signed directories or gossip protocols.  

**Perfect Forward Secrecy (PFS)**  
Property ensuring session keys are not reused, protecting past communications if keys are compromised.  

**Proof-of-Work (PoW)**  
Computational puzzles clients must solve before sending messages to prevent **spam** and **DoS attacks**.  

---

## R  

**Rate Limiting**  
Restricts the number of messages or requests a client can make in a given time period, preventing abuse.  

**Replay Attack**  
An attack where valid messages are maliciously resent. Prevented by nonces and sequence numbers in VIREX.  

---

## S  

**Sybil Attack**  
An adversary creates many fake identities (nodes) to gain disproportionate influence. Mitigated via **PoW**, **auditing**, and **federated approval**.  

**Snapshot**  
Signed directory state used by clients to bootstrap trusted information about network nodes and keys.  

---

## T  

**Threshold Signatures**  
M-of-N approval model where critical actions (e.g., key rotations) require multiple independent signatures to be valid.  

**Transparency Logs**  
Append-only logs providing public verifiability for key updates, node changes, and governance actions.  

**Traffic Analysis**  
Adversary attempts to learn who communicates with whom by observing network traffic patterns.  

---

## U  

**Uptime Metrics**  
Data on node reliability, used in peer discovery snapshots for client trust decisions.  

---

## V  

**VIREX**  
Verifiable Infrastructure for Routing with Encryption and eXtensibility – the protocol itself.  

---

## W  

**Watchdog Auditors**  
Independent auditors verifying transparency logs and publishing misbehavior reports for public inspection.  

---
