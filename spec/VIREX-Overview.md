# VIREX Protocol – Overview (v0.1.0-alpha)

**Author:** Syon Foppen  
**Status:** Alpha – for public feedback only  

---

## 1. What is VIREX?  

VIREX stands for **Verifiable Infrastructure for Routing with Encryption and eXtensibility**.  

It is a **learning project** to explore how **private, secure, and abuse-resistant communication systems** can be designed.  

Many messaging tools today **encrypt your messages**, but they **still leak metadata**:  
- Who is talking to whom  
- When messages are sent  
- How often people communicate  

VIREX tries to **hide this metadata** while still keeping the system **auditable** and **abuse-resistant**.  

---

## 2. What VIREX Tries to Achieve  

- **End-to-End Encryption:** Only the sender and receiver can read messages.  
- **Metadata Privacy:** Nobody should learn who talks to whom, or when.  
- **Abuse Resistance:** Spammers and attackers should be stopped.  
- **Federated Governance:** No single company or server controls everything.  
- **Transparency:** Public logs help detect cheating or tampering.  
- **Extensibility:** Future upgrades like post-quantum cryptography can be added later.  

---

## 3. How VIREX Works (Simplified)  

Imagine sending a **sealed letter** through several mail carriers:  
1. Each carrier only knows the **next** person to deliver to, not the full route.  
2. Some carriers carry **fake letters** to confuse eavesdroppers.  
3. The real recipient checks their mailbox at **regular times**, so nobody knows when they read messages.  

This is what VIREX does using:  
- **Mixnets:** Messages go through multiple servers with encryption layers.  
- **Dummy Traffic:** Fake messages hide real traffic patterns.  
- **Mailboxes:** Recipients fetch messages in fixed patterns to hide activity.  

---

## 4. The Role of the Directory (ODS)  

To send a message, you need the **public key** of the recipient.  
VIREX uses the **Oblivious Directory Service (ODS)**:  
- Stores public keys in a **public, auditable log**  
- Lets you look up keys **without revealing** whose key you are looking for  
- Detects if someone tries to **secretly replace keys**  

---

## 5. Community Peers & Federation  

VIREX is designed to be **open and federated**.  

- **Anyone can run a node**: mixnodes, mailbox nodes, and even ODS servers can be operated by independent peers.  
- Nodes must register with a **federated governance system** using:
  - A public key (Ed25519)  
  - Proof-of-Work or staking (future versions)  
  - Approval via **multi-party signatures**  

- **No central authority**: critical actions like key rotations, node suspensions, or log root updates require **M-of-N approvals** from federated members.  

- **Peer discovery**:  
  - Nodes learn about each other via a signed directory or gossip protocol.  
  - Clients receive **signed snapshots** of available nodes with public keys and metadata like uptime and reputation.  

- **Auditors**:  
  - Independent parties monitor node behavior via **transparency logs**.  
  - Misbehaving nodes can be flagged and suspended via federated consensus.  

This ensures a **balance between openness and security** while avoiding single points of failure.  

---

## 6. Preventing Abuse  

Without protections, attackers could flood the network. VIREX includes:  
- **Proof-of-Work:** Small puzzles make mass spamming expensive  
- **Rate Limits:** Limit how many messages one user can send  
- **Auditors:** Independent parties check logs and server behavior  

---

## 7. Governance  

VIREX is **federated**:  
- Multiple independent organizations run the infrastructure  
- Important changes require **multi-party approval**  
- Public logs make misbehavior detectable  

This avoids having a **single point of failure** or one company in control.  

---

## 8. Privacy Levels  

VIREX can be configured for different levels of privacy:  

| Level | Dummy Traffic      | Latency          | Use Case                  |
|-------|--------------------|------------------|---------------------------|
| L1    | Minimal             | < 5 seconds      | Low-latency messaging      |
| L2    | Moderate            | < 10 seconds     | Higher anonymity sets      |
| L3    | Heavy               | < 30 seconds     | Maximum metadata privacy   |  

More privacy usually means **slightly more delay** because of dummy traffic and random waiting times.  

---

## 9. Current Limitations  

- This is the **alpha version** – design only, no real implementation yet.  
- Not ready for **real-world use** or sensitive data.  
- Post-quantum encryption will come in **later versions**.  

---

## 10. Roadmap  

- **v0.2.0-beta:** First reference implementation in Rust, Go, .NET  
- **v0.3.0-beta:** Public test network for experiments  
- **v1.0.0:** Stable version after security review and audits  
- **v2.0.0:** Post-quantum secure version  

---

## 11. License  

- **Specification:** Creative Commons Attribution 4.0 (CC BY 4.0)  
- **Code (future):** Apache License 2.0  

---
