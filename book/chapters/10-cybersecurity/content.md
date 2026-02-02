# Chapter 10: Cybersecurity & Information Security

## Overview

Cybersecurity and Information Security form the backbone of protecting organizational digital assets, data, and systems from unauthorized access, attacks, and damage. This chapter covers security fundamentals, cryptographic principles, authentication mechanisms, threat landscapes, and security frameworks essential for government IT positions. Understanding these concepts is critical for designing secure systems, responding to incidents, and ensuring compliance with regulatory requirements.

## Learning Objectives

After completing this chapter, you will be able to:

1. **Explain** the CIA Triad and foundational security principles (B)
2. **Compare** authentication methods and authorization models (I)
3. **Analyze** cryptographic algorithms for different security requirements (A)
4. **Identify** various malware types and attack vectors (I)
5. **Apply** security frameworks in organizational contexts (A)
6. **Design** incident response procedures following best practices (E)
7. **Evaluate** compliance requirements for different regulatory standards (E)

---

## Section 1: Security Fundamentals [B]

### The CIA Triad

The CIA Triad represents the three fundamental objectives of information security:

```
                    ┌─────────────────┐
                    │ CONFIDENTIALITY │
                    │   (Secrecy)     │
                    └────────┬────────┘
                             │
              ┌──────────────┴──────────────┐
              │                             │
              ▼                             ▼
    ┌─────────────────┐          ┌─────────────────┐
    │   INTEGRITY     │◄────────►│  AVAILABILITY   │
    │  (Accuracy)     │          │   (Access)      │
    └─────────────────┘          └─────────────────┘
```

| Principle | Definition | Threats | Controls |
|-----------|------------|---------|----------|
| **Confidentiality** | Ensuring data is accessible only to authorized parties | Eavesdropping, data theft | Encryption, access controls |
| **Integrity** | Ensuring data accuracy and completeness | Tampering, corruption | Hashing, digital signatures |
| **Availability** | Ensuring systems and data are accessible when needed | DDoS, hardware failure | Redundancy, backups |

### Extended Security Principles

Beyond the CIA Triad, modern security incorporates additional principles:

| Principle | Description | Implementation |
|-----------|-------------|----------------|
| **Non-repudiation** | Ensuring actions cannot be denied | Digital signatures, audit logs |
| **Authenticity** | Verifying claimed identity | Certificates, authentication |
| **Accountability** | Tracking actions to entities | Logging, monitoring |

### Defense in Depth

Defense in Depth is a layered security strategy:

```
┌─────────────────────────────────────────────────────────────────┐
│                      PHYSICAL SECURITY                          │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │                   PERIMETER SECURITY                      │  │
│  │  ┌─────────────────────────────────────────────────────┐  │  │
│  │  │                 NETWORK SECURITY                    │  │  │
│  │  │  ┌───────────────────────────────────────────────┐  │  │  │
│  │  │  │              HOST SECURITY                    │  │  │  │
│  │  │  │  ┌─────────────────────────────────────────┐  │  │  │  │
│  │  │  │  │         APPLICATION SECURITY            │  │  │  │  │
│  │  │  │  │  ┌───────────────────────────────────┐  │  │  │  │  │
│  │  │  │  │  │          DATA SECURITY            │  │  │  │  │  │
│  │  │  │  │  └───────────────────────────────────┘  │  │  │  │  │
│  │  │  │  └─────────────────────────────────────────┘  │  │  │  │
│  │  │  └───────────────────────────────────────────────┘  │  │  │
│  │  └─────────────────────────────────────────────────────┘  │  │
│  └───────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
```

### Principle of Least Privilege

Users and processes should have only the minimum permissions necessary to perform their tasks:

```
┌──────────────────────────────────────────────────────────┐
│                    USER ROLES                            │
├──────────────┬───────────────┬───────────────────────────┤
│   Standard   │   Power User  │      Administrator        │
│    User      │               │                           │
├──────────────┼───────────────┼───────────────────────────┤
│ • Read own   │ • Read/write  │ • Full system access      │
│   files      │   shared      │ • User management         │
│ • Run apps   │   resources   │ • Configuration changes   │
│ • Limited    │ • Install     │ • Security settings       │
│   config     │   software    │ • Audit logs              │
└──────────────┴───────────────┴───────────────────────────┘
```

### Security by Design

Security should be integrated from the start, not added later:

| Phase | Security Activities |
|-------|---------------------|
| Requirements | Define security requirements, threat modeling |
| Design | Secure architecture, security patterns |
| Implementation | Secure coding practices, code review |
| Testing | Security testing, penetration testing |
| Deployment | Secure configuration, hardening |
| Maintenance | Patch management, monitoring |

---

## Section 2: Authentication & Authorization [I]

### Authentication Methods

Authentication verifies identity through three factor types:

| Factor Type | Description | Examples |
|-------------|-------------|----------|
| **Something You Know** | Knowledge-based | Passwords, PINs, security questions |
| **Something You Have** | Possession-based | Smart cards, tokens, phones |
| **Something You Are** | Biometric | Fingerprint, iris, facial recognition |

### Multi-Factor Authentication (MFA)

```
┌─────────────────────────────────────────────────────────────┐
│                    MFA AUTHENTICATION FLOW                  │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  User ──► [Password] ──► [OTP Token] ──► [Biometric] ──► Access
│              │               │              │                │
│         1st Factor      2nd Factor     3rd Factor            │
│         (Know)          (Have)         (Are)                 │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Single Sign-On (SSO)

SSO allows users to authenticate once and access multiple applications:

```
┌───────────┐     ┌─────────────┐     ┌────────────────┐
│   User    │────►│  Identity   │────►│  Application 1 │
└───────────┘     │  Provider   │     └────────────────┘
                  │   (IdP)     │     ┌────────────────┐
                  │             │────►│  Application 2 │
                  └─────────────┘     └────────────────┘
                                      ┌────────────────┐
                                 ────►│  Application 3 │
                                      └────────────────┘
```

### OAuth 2.0 Flow

```
┌──────────┐                                   ┌─────────────┐
│  User    │                                   │  Resource   │
│ (Owner)  │                                   │   Server    │
└────┬─────┘                                   └──────┬──────┘
     │                                                │
     │ 1. Authorization Request                       │
     │ ◄─────────────────────────────────────────────►│
     │                                                │
     │ 2. Authorization Grant                         │
     ├────────────────────────────────────────────────┤
     │                                                │
     │      ┌────────────────┐                        │
     │      │  Authorization │                        │
     │      │    Server      │                        │
     │      └───────┬────────┘                        │
     │              │                                 │
     │  3. Access Token                               │
     │ ◄────────────┤                                 │
     │              │                                 │
     │  4. API Request with Token                     │
     │ ─────────────────────────────────────────────► │
     │                                                │
     │  5. Protected Resource                         │
     │ ◄───────────────────────────────────────────── │
     │                                                │
```

### SAML (Security Assertion Markup Language)

SAML is used for enterprise SSO between identity providers and service providers:

| Component | Role |
|-----------|------|
| Identity Provider (IdP) | Authenticates users, issues SAML assertions |
| Service Provider (SP) | Relies on IdP for authentication |
| SAML Assertion | XML document with authentication/authorization data |

### Authorization Models

| Model | Description | Use Case |
|-------|-------------|----------|
| **RBAC** (Role-Based) | Permissions assigned to roles, roles assigned to users | Enterprise applications |
| **ABAC** (Attribute-Based) | Permissions based on attributes (user, resource, environment) | Complex, dynamic access control |
| **MAC** (Mandatory) | System-enforced access based on security labels | Military, government classified |
| **DAC** (Discretionary) | Owner controls access to their resources | File systems |

### RBAC Implementation

```
┌─────────────────────────────────────────────────────────────┐
│                       RBAC MODEL                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  USERS          ROLES              PERMISSIONS              │
│  ┌─────┐       ┌──────────┐       ┌──────────────────┐      │
│  │User1├──────►│ Admin    ├──────►│ Create/Read/     │      │
│  └─────┘       └──────────┘       │ Update/Delete    │      │
│  ┌─────┐       ┌──────────┐       └──────────────────┘      │
│  │User2├──────►│ Manager  ├──────►│ Create/Read/Update│     │
│  └─────┘       └──────────┘       └──────────────────┘      │
│  ┌─────┐       ┌──────────┐       ┌──────────────────┐      │
│  │User3├──────►│ Viewer   ├──────►│ Read Only        │      │
│  └─────┘       └──────────┘       └──────────────────┘      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## Section 3: Cryptography [A]

### Symmetric Encryption

Same key used for encryption and decryption:

```
┌───────────┐     ┌──────────┐     ┌────────────┐
│ Plaintext │────►│ Encrypt  │────►│ Ciphertext │
└───────────┘     │   (K)    │     └────────────┘
                  └──────────┘
                       │
                       │ Same Key (K)
                       │
                  ┌──────────┐
┌───────────┐     │ Decrypt  │     ┌────────────┐
│ Plaintext │◄────│   (K)    │◄────│ Ciphertext │
└───────────┘     └──────────┘     └────────────┘
```

| Algorithm | Key Size | Block Size | Status |
|-----------|----------|------------|--------|
| **AES** | 128/192/256 bits | 128 bits | Current standard |
| **3DES** | 168 bits | 64 bits | Legacy, being phased out |
| **DES** | 56 bits | 64 bits | Deprecated, insecure |
| **Blowfish** | 32-448 bits | 64 bits | Legacy |
| **ChaCha20** | 256 bits | Stream | Modern alternative to AES |

### Asymmetric Encryption

Different keys for encryption (public) and decryption (private):

```
┌─────────────┐                         ┌─────────────┐
│   SENDER    │                         │  RECEIVER   │
├─────────────┤                         ├─────────────┤
│             │     ┌─────────────┐     │             │
│  Plaintext  │────►│   Encrypt   │     │             │
│             │     │ (Public Key)│     │             │
│             │     └──────┬──────┘     │             │
│             │            │            │             │
│             │     ┌──────▼──────┐     │             │
│             │     │ Ciphertext  │────►│   Decrypt   │
│             │     └─────────────┘     │(Private Key)│
│             │                         │             │
│             │                         │  Plaintext  │
└─────────────┘                         └─────────────┘
```

| Algorithm | Key Size | Use Case |
|-----------|----------|----------|
| **RSA** | 2048-4096 bits | Encryption, signatures |
| **ECC** | 256-521 bits | Mobile, IoT (smaller keys) |
| **Diffie-Hellman** | 2048+ bits | Key exchange |
| **DSA** | 2048-3072 bits | Digital signatures |

### Encryption Modes

| Mode | Description | Properties |
|------|-------------|------------|
| **ECB** (Electronic Codebook) | Each block encrypted independently | Insecure for most uses (patterns visible) |
| **CBC** (Cipher Block Chaining) | Each block XORed with previous ciphertext | Requires IV, sequential |
| **CTR** (Counter) | Encrypts counter values, XORed with plaintext | Parallelizable, random access |
| **GCM** (Galois/Counter Mode) | CTR mode + authentication | Authenticated encryption, recommended |

### Hash Functions

Hash functions produce fixed-size output from variable input:

```
┌─────────────────────┐     ┌──────────────┐     ┌─────────────────┐
│   Input (any size)  │────►│ Hash Function│────►│ Hash (fixed)    │
│                     │     └──────────────┘     │                 │
│ "Hello World"       │                         │ a591a6d40bf420...│
│ (11 bytes)          │                         │ (256 bits/32 B)  │
└─────────────────────┘                         └─────────────────┘
```

| Algorithm | Output Size | Status |
|-----------|-------------|--------|
| **MD5** | 128 bits | Broken, not for security |
| **SHA-1** | 160 bits | Deprecated, collision found |
| **SHA-256** | 256 bits | Current standard |
| **SHA-512** | 512 bits | High security requirements |
| **SHA-3** | 224-512 bits | Latest standard |

### Digital Signatures

Digital signatures provide authentication, integrity, and non-repudiation:

```
SIGNING PROCESS:
┌──────────┐     ┌───────┐     ┌──────────────┐     ┌───────────┐
│ Document │────►│ Hash  │────►│ Encrypt with │────►│ Signature │
└──────────┘     └───────┘     │ Private Key  │     └───────────┘
                               └──────────────┘

VERIFICATION PROCESS:
┌───────────┐     ┌──────────────┐     ┌────────┐
│ Signature │────►│ Decrypt with │────►│ Hash 1 │──┐
└───────────┘     │ Public Key   │     └────────┘  │   ┌─────────┐
                  └──────────────┘                 ├──►│ Compare │
┌──────────┐     ┌───────┐                         │   └─────────┘
│ Document │────►│ Hash  │─────────────────────────┘
└──────────┘     └───────┘
                           Hash 2
```

### Public Key Infrastructure (PKI)

```
┌─────────────────────────────────────────────────────────────────┐
│                    PKI HIERARCHY                                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│                    ┌─────────────────┐                          │
│                    │   Root CA       │                          │
│                    │ (Self-signed)   │                          │
│                    └────────┬────────┘                          │
│                             │                                   │
│           ┌─────────────────┼─────────────────┐                 │
│           │                 │                 │                 │
│    ┌──────▼──────┐   ┌──────▼──────┐   ┌──────▼──────┐          │
│    │Intermediate │   │Intermediate │   │Intermediate │          │
│    │   CA 1      │   │   CA 2      │   │   CA 3      │          │
│    └──────┬──────┘   └──────┬──────┘   └──────┬──────┘          │
│           │                 │                 │                 │
│    ┌──────▼──────┐   ┌──────▼──────┐   ┌──────▼──────┐          │
│    │ End Entity  │   │ End Entity  │   │ End Entity  │          │
│    │ Certificate │   │ Certificate │   │ Certificate │          │
│    └─────────────┘   └─────────────┘   └─────────────┘          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### X.509 Certificate Structure

| Field | Description |
|-------|-------------|
| Version | Certificate format version (typically v3) |
| Serial Number | Unique identifier from CA |
| Signature Algorithm | Algorithm used to sign certificate |
| Issuer | CA that issued the certificate |
| Validity Period | Not Before, Not After dates |
| Subject | Entity the certificate represents |
| Public Key | Subject's public key and algorithm |
| Extensions | Additional attributes (Key Usage, SAN, etc.) |
| Signature | CA's digital signature |

---

## Section 4: Malware & Threats [I]

### Malware Types

| Type | Behavior | Propagation |
|------|----------|-------------|
| **Virus** | Attaches to programs, activates on execution | User action required |
| **Worm** | Self-replicating, spreads automatically | Network exploitation |
| **Trojan** | Disguised as legitimate software | Social engineering |
| **Ransomware** | Encrypts files, demands payment | Phishing, vulnerabilities |
| **Spyware** | Monitors user activity covertly | Bundled software, drive-by |
| **Rootkit** | Hides deep in system, maintains access | Privilege escalation |
| **Botnet** | Network of compromised computers | Various methods |
| **Adware** | Displays unwanted advertisements | Bundled installers |

### Malware Lifecycle

```
┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│   Delivery   │───►│ Exploitation │───►│ Installation │
│ (Email, Web) │    │(Vulnerability)│    │  (Payload)   │
└──────────────┘    └──────────────┘    └──────┬───────┘
                                               │
┌──────────────┐    ┌──────────────┐    ┌──────▼───────┐
│   Actions    │◄───│   Command &  │◄───│  Persistence │
│  on Target   │    │   Control    │    │(Survive reboot)│
└──────────────┘    └──────────────┘    └──────────────┘
```

### Social Engineering Attacks

| Attack Type | Description | Target |
|-------------|-------------|--------|
| **Phishing** | Fraudulent emails mimicking legitimate sources | Mass targeting |
| **Spear Phishing** | Targeted phishing at specific individuals | High-value targets |
| **Whaling** | Phishing targeting executives | C-level executives |
| **Vishing** | Voice-based phishing (phone calls) | Employees, customers |
| **Smishing** | SMS-based phishing | Mobile users |
| **Pretexting** | Creating false scenario to gain trust | Support staff |
| **Baiting** | Offering something enticing (infected USB) | Curious employees |
| **Tailgating** | Following authorized person through door | Physical access |

### Common Attack Vectors

```
┌─────────────────────────────────────────────────────────────────┐
│                    ATTACK SURFACE                               │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐              │
│  │   Email     │  │    Web      │  │   Network   │              │
│  │ • Phishing  │  │ • XSS       │  │ • DDoS      │              │
│  │ • Malware   │  │ • SQLi      │  │ • MITM      │              │
│  │ • BEC       │  │ • CSRF      │  │ • Sniffing  │              │
│  └─────────────┘  └─────────────┘  └─────────────┘              │
│                                                                 │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐              │
│  │  Physical   │  │   Insider   │  │  Third-Party│              │
│  │ • Theft     │  │ • Malicious │  │ • Supply    │              │
│  │ • Tailgate  │  │ • Negligent │  │   chain     │              │
│  │ • Dumpster  │  │             │  │ • API abuse │              │
│  └─────────────┘  └─────────────┘  └─────────────┘              │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### OWASP Top 10 (2021)

| Rank | Vulnerability | Description |
|------|---------------|-------------|
| A01 | Broken Access Control | Unauthorized access to resources |
| A02 | Cryptographic Failures | Weak or missing encryption |
| A03 | Injection | SQL, NoSQL, OS command injection |
| A04 | Insecure Design | Missing security controls in design |
| A05 | Security Misconfiguration | Insecure default settings |
| A06 | Vulnerable Components | Using outdated libraries |
| A07 | Auth & Session Failures | Weak authentication |
| A08 | Software/Data Integrity | Unverified updates, CI/CD issues |
| A09 | Logging & Monitoring | Insufficient detection capability |
| A10 | SSRF | Server-Side Request Forgery |

### Password Attacks

| Attack | Method | Defense |
|--------|--------|---------|
| **Brute Force** | Try all possible combinations | Account lockout, complexity |
| **Dictionary** | Try common words/passwords | Not using common passwords |
| **Rainbow Tables** | Pre-computed hash lookup | Salt passwords |
| **Credential Stuffing** | Reuse leaked credentials | Unique passwords, MFA |
| **Keylogging** | Capture keystrokes | Anti-malware, virtual keyboards |

---

## Section 5: Security Frameworks & Standards [A]

### ISO 27001/27002

ISO 27001 is the international standard for Information Security Management Systems (ISMS):

```
┌─────────────────────────────────────────────────────────────────┐
│                    ISO 27001 PDCA CYCLE                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│                    ┌───────────────┐                            │
│         ┌─────────►│     PLAN      │─────────┐                  │
│         │          │ Establish ISMS │          │                 │
│         │          └───────────────┘          │                 │
│         │                                     ▼                 │
│  ┌──────┴──────┐                      ┌───────────────┐         │
│  │    ACT      │                      │      DO       │         │
│  │  Maintain & │                      │  Implement &  │         │
│  │   Improve   │                      │   Operate     │         │
│  └──────┬──────┘                      └───────┬───────┘         │
│         │                                     │                 │
│         │          ┌───────────────┐          │                 │
│         └──────────│    CHECK      │◄─────────┘                 │
│                    │Monitor & Review│                           │
│                    └───────────────┘                            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### ISO 27001 Control Domains

| Domain | Controls |
|--------|----------|
| Organizational | Policies, roles, responsibilities |
| People | Screening, awareness, training |
| Physical | Perimeters, equipment, secure areas |
| Technological | Access control, cryptography, operations |

### NIST Cybersecurity Framework

```
┌─────────────────────────────────────────────────────────────────┐
│                 NIST CSF CORE FUNCTIONS                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────┐ │
│  │ IDENTIFY │►│ PROTECT  │►│  DETECT  │►│ RESPOND  │►│RECOVER │ │
│  └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘ └───┬────┘ │
│       │            │            │            │           │      │
│  • Asset Mgmt  • Access    • Anomalies  • Planning  • Recovery  │
│  • Business    • Training  • Security   • Comms     • Planning  │
│    Environment • Data Sec  • Monitoring • Analysis  • Improve   │
│  • Governance  • Info Prot • Detection  • Mitigation• Comms     │
│  • Risk Assess • Maint.    • Processes  • Improve              │
│  • Strategy    • Protect                                       │
│                  Tech                                          │
└─────────────────────────────────────────────────────────────────┘
```

### CIS Critical Security Controls

| Control # | Name | Priority |
|-----------|------|----------|
| 1 | Inventory of Enterprise Assets | Basic |
| 2 | Inventory of Software Assets | Basic |
| 3 | Data Protection | Basic |
| 4 | Secure Configuration | Basic |
| 5 | Account Management | Basic |
| 6 | Access Control Management | Basic |
| 7 | Continuous Vulnerability Management | Foundational |
| 8 | Audit Log Management | Foundational |
| 9 | Email & Web Browser Protections | Foundational |
| 10 | Malware Defenses | Foundational |

### COBIT for Security Governance

COBIT (Control Objectives for Information Technology) provides IT governance framework:

| Domain | Purpose |
|--------|---------|
| **EDM** (Evaluate, Direct, Monitor) | Governance oversight |
| **APO** (Align, Plan, Organize) | IT strategy alignment |
| **BAI** (Build, Acquire, Implement) | Solution delivery |
| **DSS** (Deliver, Service, Support) | Operations |
| **MEA** (Monitor, Evaluate, Assess) | Performance monitoring |

---

## Section 6: Incident Response [E]

### Incident Response Phases

```
┌─────────────────────────────────────────────────────────────────┐
│              INCIDENT RESPONSE LIFECYCLE                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌────────────┐                           ┌────────────────┐    │
│  │PREPARATION │──────────────────────────►│IDENTIFICATION  │    │
│  │            │                           │                │    │
│  │ • Policies │                           │ • Detection    │    │
│  │ • Tools    │                           │ • Analysis     │    │
│  │ • Training │                           │ • Triage       │    │
│  └────────────┘                           └───────┬────────┘    │
│        ▲                                          │             │
│        │                                          ▼             │
│  ┌─────┴───────┐                          ┌───────────────┐     │
│  │   LESSONS   │                          │  CONTAINMENT  │     │
│  │   LEARNED   │                          │               │     │
│  │             │                          │ • Short-term  │     │
│  │ • Review    │                          │ • Long-term   │     │
│  │ • Document  │                          │ • Evidence    │     │
│  └─────────────┘                          └───────┬───────┘     │
│        ▲                                          │             │
│        │                                          ▼             │
│  ┌─────┴───────┐                          ┌───────────────┐     │
│  │  RECOVERY   │◄─────────────────────────│  ERADICATION  │     │
│  │             │                          │               │     │
│  │ • Restore   │                          │ • Remove      │     │
│  │ • Monitor   │                          │   threat      │     │
│  │ • Validate  │                          │ • Patch       │     │
│  └─────────────┘                          └───────────────┘     │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Incident Classification

| Severity | Description | Response Time | Example |
|----------|-------------|---------------|---------|
| **Critical** | System-wide impact, data breach | Immediate | Ransomware, active intrusion |
| **High** | Major service disruption | < 1 hour | Malware outbreak |
| **Medium** | Limited impact, contained | < 4 hours | Single compromised system |
| **Low** | Minor incident, no data impact | < 24 hours | Phishing attempt blocked |

### Incident Response Team Structure

```
┌─────────────────────────────────────────────────────────────────┐
│                   INCIDENT RESPONSE TEAM                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│                    ┌───────────────────┐                        │
│                    │  Incident Manager │                        │
│                    │  (Team Leader)    │                        │
│                    └─────────┬─────────┘                        │
│                              │                                  │
│         ┌────────────────────┼────────────────────┐             │
│         │                    │                    │             │
│  ┌──────▼──────┐     ┌───────▼──────┐     ┌──────▼──────┐       │
│  │  Technical  │     │ Communications│     │   Legal/    │       │
│  │   Lead      │     │    Lead      │     │  Compliance │       │
│  └──────┬──────┘     └──────────────┘     └─────────────┘       │
│         │                                                       │
│    ┌────┴────┬────────────┬────────────┐                        │
│    │         │            │            │                        │
│ ┌──▼──┐  ┌───▼───┐  ┌─────▼────┐  ┌────▼────┐                   │
│ │ SOC │  │Network│  │ Forensic │  │ System  │                   │
│ │Analyst│ │ Admin │  │ Analyst  │  │  Admin  │                   │
│ └─────┘  └───────┘  └──────────┘  └─────────┘                   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Digital Forensics Process

| Phase | Activities |
|-------|------------|
| **Identification** | Recognize potential evidence sources |
| **Preservation** | Secure and protect evidence from modification |
| **Collection** | Gather evidence using forensic methods |
| **Examination** | Process collected data |
| **Analysis** | Draw conclusions from examined data |
| **Presentation** | Report findings clearly |

### Chain of Custody

```
┌─────────────────────────────────────────────────────────────────┐
│                   CHAIN OF CUSTODY FORM                         │
├─────────────────────────────────────────────────────────────────┤
│ Evidence ID: EVD-2024-001                                       │
│ Description: Hard drive from workstation WS-104                 │
│ Case Number: INC-2024-0542                                      │
├─────────────────────────────────────────────────────────────────┤
│ # │ Date/Time    │ Released By  │ Received By │ Purpose        │
│───┼──────────────┼──────────────┼─────────────┼────────────────│
│ 1 │ 2024-01-15   │ J. Smith     │ K. Wilson   │ Initial        │
│   │ 09:30        │ (IT Admin)   │ (Forensics) │ collection     │
│───┼──────────────┼──────────────┼─────────────┼────────────────│
│ 2 │ 2024-01-16   │ K. Wilson    │ Evidence    │ Secure         │
│   │ 14:00        │ (Forensics)  │ Locker      │ storage        │
└─────────────────────────────────────────────────────────────────┘
```

---

## Section 7: Compliance & Regulations [E]

### Major Compliance Frameworks

| Regulation | Scope | Key Requirements |
|------------|-------|------------------|
| **GDPR** | EU personal data | Consent, right to erasure, breach notification |
| **HIPAA** | US healthcare | PHI protection, security rule, privacy rule |
| **PCI-DSS** | Payment cards | Encryption, access control, network security |
| **SOX** | US public companies | Financial controls, audit trails |
| **CCPA** | California consumers | Privacy rights, opt-out |

### GDPR Key Principles

```
┌─────────────────────────────────────────────────────────────────┐
│                    GDPR PRINCIPLES                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. LAWFULNESS, FAIRNESS, TRANSPARENCY                          │
│     └── Process data legally and openly                         │
│                                                                 │
│  2. PURPOSE LIMITATION                                          │
│     └── Collect for specified, explicit purposes                │
│                                                                 │
│  3. DATA MINIMIZATION                                           │
│     └── Only collect what's necessary                           │
│                                                                 │
│  4. ACCURACY                                                    │
│     └── Keep data accurate and up to date                       │
│                                                                 │
│  5. STORAGE LIMITATION                                          │
│     └── Don't keep data longer than needed                      │
│                                                                 │
│  6. INTEGRITY & CONFIDENTIALITY                                 │
│     └── Ensure security of personal data                        │
│                                                                 │
│  7. ACCOUNTABILITY                                              │
│     └── Demonstrate compliance                                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### GDPR Data Subject Rights

| Right | Description |
|-------|-------------|
| Right to be Informed | Know how data is being used |
| Right of Access | Obtain copy of personal data |
| Right to Rectification | Correct inaccurate data |
| Right to Erasure | Request deletion ("right to be forgotten") |
| Right to Restrict Processing | Limit how data is used |
| Right to Data Portability | Receive data in portable format |
| Right to Object | Object to certain processing |

### PCI-DSS Requirements

| Requirement | Control Area |
|-------------|--------------|
| 1 | Install and maintain network security controls |
| 2 | Apply secure configurations |
| 3 | Protect stored account data |
| 4 | Protect cardholder data with cryptography |
| 5 | Protect systems from malware |
| 6 | Develop secure systems and software |
| 7 | Restrict access by need to know |
| 8 | Identify users and authenticate access |
| 9 | Restrict physical access |
| 10 | Log and monitor access |
| 11 | Test security regularly |
| 12 | Support security with policies |

### Vulnerability Management

```
┌─────────────────────────────────────────────────────────────────┐
│              VULNERABILITY MANAGEMENT CYCLE                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│         ┌──────────────┐                                        │
│         │   DISCOVER   │                                        │
│         │  (Scanning)  │                                        │
│         └──────┬───────┘                                        │
│                │                                                │
│                ▼                                                │
│         ┌──────────────┐         ┌──────────────┐               │
│         │  PRIORITIZE  │────────►│  REMEDIATE   │               │
│         │   (CVSS)     │         │  (Patching)  │               │
│         └──────────────┘         └──────┬───────┘               │
│                ▲                        │                       │
│                │                        ▼                       │
│         ┌──────┴───────┐         ┌──────────────┐               │
│         │    REPORT    │◄────────│    VERIFY    │               │
│         │              │         │ (Rescan)     │               │
│         └──────────────┘         └──────────────┘               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### CVSS Scoring

Common Vulnerability Scoring System (CVSS) rates vulnerabilities:

| Score Range | Severity | Response |
|-------------|----------|----------|
| 9.0 - 10.0 | Critical | Immediate remediation |
| 7.0 - 8.9 | High | Remediate within days |
| 4.0 - 6.9 | Medium | Remediate within weeks |
| 0.1 - 3.9 | Low | Remediate as resources allow |

### Data Breach Notification

| Jurisdiction | Notification Timeframe | To Whom |
|--------------|------------------------|---------|
| GDPR | 72 hours | Supervisory authority |
| HIPAA | 60 days | HHS, individuals |
| State Laws | Varies (typically 30-90 days) | Affected individuals |
| PCI-DSS | Immediately | Card brands, acquirer |

---

## Section 8: Security Tools & Technologies [A]

### Security Information and Event Management (SIEM)

```
┌─────────────────────────────────────────────────────────────────┐
│                      SIEM ARCHITECTURE                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  DATA SOURCES                     SIEM PLATFORM                 │
│  ┌─────────┐                  ┌───────────────────────────────┐ │
│  │Firewall │──┐               │  ┌─────────┐  ┌────────────┐  │ │
│  └─────────┘  │               │  │ Collect │──│ Normalize  │  │ │
│  ┌─────────┐  │  ┌─────────┐  │  └────┬────┘  └─────┬──────┘  │ │
│  │ IDS/IPS │──┼─►│  Agent  │─►│       │              │        │ │
│  └─────────┘  │  │/Syslog  │  │       ▼              ▼        │ │
│  ┌─────────┐  │  └─────────┘  │  ┌─────────────────────────┐  │ │
│  │ Servers │──┤               │  │      CORRELATION        │  │ │
│  └─────────┘  │               │  │         ENGINE          │  │ │
│  ┌─────────┐  │               │  └───────────┬─────────────┘  │ │
│  │ Apps    │──┘               │              │                │ │
│  └─────────┘                  │              ▼                │ │
│                               │  ┌────────────────────────┐   │ │
│                               │  │ ALERTS │ DASHBOARD │   │   │ │
│                               │  │        │ REPORTS   │   │   │ │
│                               │  └────────────────────────┘   │ │
│                               └───────────────────────────────┘ │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Security Tool Categories

| Category | Purpose | Examples |
|----------|---------|----------|
| **Antivirus/EDR** | Malware detection and response | CrowdStrike, Carbon Black |
| **Firewall** | Network traffic control | Palo Alto, Cisco ASA |
| **IDS/IPS** | Intrusion detection/prevention | Snort, Suricata |
| **Vulnerability Scanner** | Find weaknesses | Nessus, Qualys, OpenVAS |
| **SIEM** | Log aggregation and correlation | Splunk, QRadar, Elastic |
| **PAM** | Privileged access management | CyberArk, BeyondTrust |
| **DLP** | Data loss prevention | Symantec DLP, McAfee |
| **WAF** | Web application firewall | ModSecurity, Cloudflare |

### Penetration Testing Phases

```
┌─────────────────────────────────────────────────────────────────┐
│               PENETRATION TESTING METHODOLOGY                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. PLANNING        2. RECONNAISSANCE     3. SCANNING           │
│  ┌──────────┐       ┌──────────┐          ┌──────────┐          │
│  │ • Scope  │──────►│ • OSINT  │─────────►│ • Port   │          │
│  │ • Rules  │       │ • Passive│          │ • Vuln   │          │
│  │ • Goals  │       │ • Active │          │ • Service│          │
│  └──────────┘       └──────────┘          └────┬─────┘          │
│                                                │                │
│  6. REPORTING       5. POST-EXPLOIT      4. EXPLOITATION        │
│  ┌──────────┐       ┌──────────┐          ┌────▼─────┐          │
│  │ • Findings│◄─────│ • Pivot  │◄─────────│ • Gain   │          │
│  │ • Remedies│      │ • Persist│          │   Access │          │
│  │ • Risk   │       │ • Data   │          │ • Escalate│         │
│  └──────────┘       └──────────┘          └──────────┘          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Network Security Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                  SECURE NETWORK ARCHITECTURE                    │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  INTERNET                                                       │
│      │                                                          │
│      ▼                                                          │
│  ┌───────────────────────┐                                      │
│  │   EDGE FIREWALL       │                                      │
│  │   (Perimeter)         │                                      │
│  └───────────┬───────────┘                                      │
│              │                                                  │
│  ┌───────────▼───────────┐                                      │
│  │        DMZ            │                                      │
│  │  ┌────┐ ┌────┐ ┌────┐ │                                      │
│  │  │Web │ │Mail│ │DNS │ │                                      │
│  │  └────┘ └────┘ └────┘ │                                      │
│  └───────────┬───────────┘                                      │
│              │                                                  │
│  ┌───────────▼───────────┐                                      │
│  │   INTERNAL FIREWALL   │                                      │
│  └───────────┬───────────┘                                      │
│              │                                                  │
│  ┌───────────▼───────────────────────────────────────────────┐  │
│  │               INTERNAL NETWORK                            │  │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐        │  │
│  │  │  User VLAN  │  │ Server VLAN│  │  Admin VLAN │        │  │
│  │  └─────────────┘  └─────────────┘  └─────────────┘        │  │
│  └───────────────────────────────────────────────────────────┘  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Wireless Security Protocols

| Protocol | Encryption | Status |
|----------|------------|--------|
| WEP | RC4 (40/104-bit) | Deprecated, easily broken |
| WPA | TKIP (RC4) | Deprecated |
| WPA2 | AES-CCMP | Current standard |
| WPA3 | AES-GCMP, SAE | Latest, recommended |

---

## Section 9: Network Security Controls [I]

### Firewall Configuration

```
┌─────────────────────────────────────────────────────────────────┐
│                    FIREWALL RULE EXAMPLE                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ Rule # │ Source      │ Dest        │ Port  │ Protocol │ Action │
│────────┼─────────────┼─────────────┼───────┼──────────┼────────│
│   1    │ Any         │ Web Server  │ 443   │ TCP      │ ALLOW  │
│   2    │ Any         │ Web Server  │ 80    │ TCP      │ ALLOW  │
│   3    │ Admin Net   │ All Servers │ 22    │ TCP      │ ALLOW  │
│   4    │ Internal    │ DNS Server  │ 53    │ UDP      │ ALLOW  │
│   5    │ VPN Users   │ Internal    │ Any   │ Any      │ ALLOW  │
│  ...   │ ...         │ ...         │ ...   │ ...      │ ...    │
│  999   │ Any         │ Any         │ Any   │ Any      │ DENY   │
│                                                                 │
│ Note: Rules processed top-to-bottom, first match wins          │
│       Default deny (implicit deny) at end                      │
└─────────────────────────────────────────────────────────────────┘
```

### VPN Types

| Type | Description | Use Case |
|------|-------------|----------|
| **Site-to-Site** | Connects two networks | Branch office to HQ |
| **Remote Access** | Individual users to network | Remote workers |
| **IPSec** | Layer 3 VPN, strong security | Enterprise |
| **SSL/TLS** | Browser-based, Layer 7 | Client portals |
| **WireGuard** | Modern, lightweight | Performance-focused |

### Network Segmentation

```
┌─────────────────────────────────────────────────────────────────┐
│                   NETWORK SEGMENTATION                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────────┐   ┌─────────────────┐   ┌───────────────┐  │
│  │   Production    │   │   Development   │   │    Guest      │  │
│  │    VLAN 10      │   │    VLAN 20      │   │   VLAN 30     │  │
│  │                 │   │                 │   │               │  │
│  │ • Web Servers   │   │ • Dev Servers   │   │ • WiFi        │  │
│  │ • App Servers   │   │ • Test Systems  │   │ • Visitors    │  │
│  │ • Databases     │   │ • CI/CD         │   │ • Isolated    │  │
│  └────────┬────────┘   └────────┬────────┘   └───────┬───────┘  │
│           │                     │                    │          │
│           └──────────┬──────────┴──────────┬─────────┘          │
│                      │                     │                    │
│               ┌──────▼──────┐       ┌──────▼──────┐             │
│               │  Firewall   │       │   Router    │             │
│               │  (ACLs)     │       │  (Routing)  │             │
│               └─────────────┘       └─────────────┘             │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Zero Trust Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                  ZERO TRUST PRINCIPLES                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. NEVER TRUST, ALWAYS VERIFY                                  │
│     └── Authenticate and authorize every request                │
│                                                                 │
│  2. ASSUME BREACH                                               │
│     └── Design as if attackers are already inside               │
│                                                                 │
│  3. LEAST PRIVILEGE ACCESS                                      │
│     └── Grant minimum permissions needed                        │
│                                                                 │
│  4. MICROSEGMENTATION                                           │
│     └── Fine-grained network segmentation                       │
│                                                                 │
│  5. CONTINUOUS VERIFICATION                                     │
│     └── Real-time trust evaluation                              │
│                                                                 │
│  IMPLEMENTATION:                                                │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐         │
│  │ Identity │→ │ Device   │→ │ Network  │→ │ App/Data │         │
│  │ Verify   │  │ Health   │  │ Controls │  │ Access   │         │
│  └──────────┘  └──────────┘  └──────────┘  └──────────┘         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## Section 10: Summary & Key Takeaways [B]

### Chapter Summary

This chapter covered the essential aspects of cybersecurity and information security:

1. **Security Fundamentals**: CIA Triad, defense in depth, least privilege
2. **Authentication & Authorization**: MFA, SSO, OAuth, RBAC/ABAC
3. **Cryptography**: Symmetric/asymmetric encryption, hashing, digital signatures, PKI
4. **Malware & Threats**: Types of malware, social engineering, OWASP Top 10
5. **Security Frameworks**: ISO 27001, NIST CSF, CIS Controls, COBIT
6. **Incident Response**: Six phases, team structure, forensics
7. **Compliance**: GDPR, HIPAA, PCI-DSS, vulnerability management
8. **Security Tools**: SIEM, firewalls, IDS/IPS, penetration testing
9. **Network Security**: Firewalls, VPNs, segmentation, Zero Trust

### Key Formulas and Quick Reference

| Concept | Formula/Standard |
|---------|------------------|
| Risk | Risk = Threat × Vulnerability × Impact |
| ALE | ALE = SLE × ARO |
| CVSS | 0-10 scale (Critical > 9.0) |
| MFA | 2+ factors from different categories |

### Exam Tips

1. Memorize the CIA Triad and extended security principles
2. Know the differences between encryption types (symmetric vs asymmetric)
3. Understand NIST CSF five functions (Identify, Protect, Detect, Respond, Recover)
4. Remember incident response phases in order
5. Know major compliance requirements (GDPR 72-hour notification, PCI-DSS 12 requirements)
6. Understand authentication factor types
7. Be familiar with OWASP Top 10 vulnerabilities

---

## Hands-On Labs

### Lab 10.1: Implementing Password Policies
**Objective**: Configure strong password policies in Windows Active Directory and Linux PAM.

**Difficulty**: Intermediate

**Reference**: See `labs/lab-10.1-password-policies.md`

### Lab 10.2: Firewall Rule Configuration
**Objective**: Configure firewall rules using iptables (Linux) and Windows Firewall.

**Difficulty**: Intermediate

**Reference**: See `labs/lab-10.2-firewall-rules.md`

### Lab 10.3: Vulnerability Scanning with OpenVAS
**Objective**: Install and use OpenVAS to scan for vulnerabilities.

**Difficulty**: Advanced

**Reference**: See `labs/lab-10.3-vulnerability-scanning.md`

### Lab 10.4: Incident Response Simulation
**Objective**: Practice incident response procedures using a simulated malware infection scenario.

**Difficulty**: Advanced

**Reference**: See `labs/lab-10.4-incident-response.md`

---

## Practice Questions

### Multiple Choice Questions

1. **Which of the following is NOT part of the CIA Triad?**
   - A) Confidentiality
   - B) Integrity
   - C) Authentication
   - D) Availability

2. **What type of encryption uses the same key for encryption and decryption?**
   - A) Asymmetric
   - B) Symmetric
   - C) Hashing
   - D) Digital signature

3. **Which authentication factor type does a fingerprint scan represent?**
   - A) Something you know
   - B) Something you have
   - C) Something you are
   - D) Something you do

4. **What is the maximum time allowed to report a data breach under GDPR?**
   - A) 24 hours
   - B) 48 hours
   - C) 72 hours
   - D) 7 days

5. **Which NIST CSF function focuses on maintaining recovery plans?**
   - A) Identify
   - B) Protect
   - C) Respond
   - D) Recover

6. **What type of attack involves an attacker intercepting communication between two parties?**
   - A) DDoS
   - B) Man-in-the-Middle
   - C) SQL Injection
   - D) Cross-Site Scripting

7. **Which encryption algorithm is considered the current standard for symmetric encryption?**
   - A) DES
   - B) 3DES
   - C) AES
   - D) MD5

8. **What does SIEM stand for?**
   - A) Security Information and Event Management
   - B) Security Infrastructure and Endpoint Monitoring
   - C) System Integration and Enterprise Management
   - D) Secure Internet and Email Monitoring

9. **Which authorization model assigns permissions based on user attributes?**
   - A) RBAC
   - B) ABAC
   - C) MAC
   - D) DAC

10. **What is the first phase of incident response?**
    - A) Identification
    - B) Preparation
    - C) Containment
    - D) Eradication

### Answer Key

1. C - Authentication is not part of the CIA Triad (it's Confidentiality, Integrity, Availability)
2. B - Symmetric encryption uses the same key for both operations
3. C - Biometrics represent "something you are"
4. C - GDPR requires notification within 72 hours
5. D - Recover function includes recovery planning and improvements
6. B - Man-in-the-Middle attacks intercept communications
7. C - AES is the current standard for symmetric encryption
8. A - Security Information and Event Management
9. B - ABAC (Attribute-Based Access Control) uses attributes for decisions
10. B - Preparation is the first phase, before Identification

---

## References

1. NIST Cybersecurity Framework - https://www.nist.gov/cyberframework
2. ISO/IEC 27001:2022 Information Security Management
3. CIS Critical Security Controls - https://www.cisecurity.org/controls
4. OWASP Top 10 - https://owasp.org/www-project-top-ten/
5. GDPR Official Text - https://gdpr.eu/
6. PCI DSS Requirements - https://www.pcisecuritystandards.org/
7. SANS Incident Response Handbook
8. Cryptography and Network Security by William Stallings
