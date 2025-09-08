# Security Policy – VIREX Project  

## Supported Versions  

Currently, the **VIREX Protocol** is in **alpha** stage (**v0.1.0-alpha**).  
The focus is on **public feedback**, **design discussions**, and **specification review**.  
Security reporting procedures are already in place for when reference implementations are introduced in future versions.  

---

## Reporting a Vulnerability  

If you discover a security issue, please follow these steps:  

1. **Do NOT open a public GitHub Issue** for the vulnerability.  
2. Instead, report it privately using one of the following methods:  
   - **GitHub Security Advisories** (preferred)  
   - Email: [syon@syonfoppen.nl](mailto:syon@syonfoppen.nl)  

This helps prevent malicious actors from exploiting the vulnerability before it is addressed.  

---

## Encryption for Secure Communication  

For sensitive vulnerability reports, you can encrypt your communication using our PGP key:  

- **PGP Fingerprint**: `5982 EF3B 32E7 672D D299 CAB3 45EA A161 4436 9252`  
- **Public Key**: [Download PGP key](https://keys.openpgp.org/vks/v1/by-fingerprint/5982EF3B32E7672DD299CAB345EAA16144369252)  

We recommend using this key when sending security-related information via email to ensure end-to-end encryption.  

---

## What to Include in Your Report  

To help us understand and reproduce the issue quickly, please include:  
- A detailed description of the vulnerability  
- Steps to reproduce or proof-of-concept code, if possible  
- The potential impact of the issue  
- Suggested remediation steps (if known)  

---

## Response Process  

- The security team will acknowledge your report within **7 days**.  
- We will investigate and assess the severity of the issue.  
- For critical vulnerabilities, we will prepare a patch or mitigation plan as quickly as possible.  
- You will be kept informed about progress and publication timelines.  

---

## Disclosure  

We follow a **coordinated disclosure** approach:  
- You report the vulnerability privately.  
- We work on a fix or mitigation.  
- A security advisory is published with credit to the reporter once the issue is resolved.  

---

## Scope  

Currently in **v0.1.0-alpha**:  
- All documents under `spec/`, `governance/`, and `docs/` are in-scope for design-related vulnerabilities.  
- Future reference implementations (`reference-impl/`) will be in-scope starting from **v0.2.0-beta**.  

---

## Responsible Disclosure Commitment  

We are committed to:  
- Working **with security researchers** who report issues responsibly.  
- Ensuring vulnerabilities are **fixed before public disclosure**.  
- Giving **credit** to reporters who help improve the security of the project.  
