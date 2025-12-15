# Secure Communication
Secure communication is about ensuring that **data in transit** maintains:
- **[[02-The-CIA-Triad#Confidentiality|Confidentiality]]** (no eavesdropping)
- **[[02-The-CIA-Triad#Integrity|Integrity]]** (no tampering)
- **[[04-Authentication-Authorization-&-Accounting#Authentication - Verifying Identity|Authentication]]** (know who you’re talking to)
- **[[03-Non-repudiation|Non-repudiation]]** (proof of origin, in some cases)

This topic operationalizes many of the crypto concepts we covered earlier.

---
### **Core Goals of Secure Communication**
Every secure communication mechanism is trying to solve one or more of these:

| Goal            | Meaning in Practice               |
| --------------- | --------------------------------- |
| Confidentiality | Encryption prevents eavesdropping |
| Integrity       | Hashing / MACs detect tampering   |
| Authentication  | Certificates, keys, credentials   |
| Non-repudiation | Digital signatures provide proof  |

**Exam mindset:**  
If data is _moving_, think **secure communication**, not “data at rest.”

---
### **Encryption in Transit (Foundation)**
#### **2.1 Symmetric Encryption**
- Same key encrypts and decrypts
- Fast
- Used for bulk data transfer

Examples:
- AES (Advanced Encryption Standard)

#### **2.2 Asymmetric Encryption**
- Public/private key pairs
- Used for:
    - Key exchange
    - Authentication
    - Digital signatures

Examples:
- RSA
- ECC (Elliptic Curve Cryptography — more efficient)

#### **2.3 Hybrid Encryption (Very Important)**
Most secure communication uses:
- Asymmetric crypto → establish trust & exchange keys
- Symmetric crypto → encrypt the session

**TLS uses hybrid encryption.**  
This is one of the most important takeaways.

---
### **TLS (Transport Layer Security)**
#### **3.1 What TLS Is**
TLS is the **standard protocol** for securing data in transit over IP networks.

It provides:
- Encryption
- Integrity
- Authentication

TLS replaced SSL (SSL is deprecated).

#### **3.2 TLS Handshake (High-Level Flow)**
1. Client connects to server
2. Server presents **certificate**
3. Client validates certificate (CA trust chain)
4. Keys are exchanged securely
5. Encrypted session begins

You do **not** need packet-level detail for Security+, just the concept.

#### **3.3 TLS Versions**
- TLS 1.2 → still widely used
- TLS 1.3 → faster, more secure (preferred)

Exam trigger:
> “Modern secure communication” → TLS 1.3

---
### **Certificates & PKI (Reinforcement)**
Secure communication relies heavily on **PKI**.
#### **4.1 Digital Certificates**
Certificates bind:
- Public key
- Identity (domain, organization)
- CA signature

Used for:
- Server authentication
- Client authentication (sometimes)

#### **4.2 Certificate Authorities (CAs)**
Trusted third parties that issue certificates.

Trust model:
- Root CA → Intermediate CA → Server cert

#### **4.3 Certificate Validation**
Client checks:
- Signature validity
- Expiration date
- Revocation status (CRL / OCSP)

Exam trigger:
> “Verify server identity” → certificate validation

---
### **Secure Communication Protocols (Very Testable)**
#### **5.1 HTTPS**
- HTTP over TLS
- Protects web traffic

If you see:
> “Secure web communication” → HTTPS

#### **5.2 Secure Email Protocols**
- **SMTPS** (SMTP over TLS)
- **IMAPS** (IMAP over TLS)
- **POP3S** (POP3 over TLS)

Provides:
- Encryption in transit
- Authentication

#### **5.3 Secure File Transfer**
- **SFTP** (SSH File Transfer Protocol)
- **FTPS** (FTP over TLS)

Exam trap:
- SFTP ≠ FTP + SSL
- SFTP runs over **SSH**

#### **5.4 Secure Remote Access**
- **SSH** (Secure Shell)
- Uses asymmetric keys for authentication

Exam trigger:
> “Secure remote administration” → SSH

---
### **IPsec (Network-Layer Secure Communication)**
#### **6.1 What IPsec Is**
A suite of protocols that secures **IP traffic at Layer 3**.

Used for:
- VPNs
- Site-to-site tunnels
- Remote access VPNs

#### **6.2 IPsec Components**
- **AH (Authentication Header)** → integrity & authentication
- **ESP (Encapsulating Security Payload)** → encryption + integrity

ESP is used far more commonly.

#### **6.3 IPsec Modes**
- **Transport mode** → encrypts payload only
- **Tunnel mode** → encrypts entire packet (used for VPNs)

Exam trigger:
> “Site-to-site VPN” → IPsec tunnel mode

---
### **Secure Wireless Communication (Quick Tie-In)**
Wireless adds risk because the medium is shared.

Controls:
- WPA3 (preferred)
- Strong encryption (AES)
- Mutual authentication

This reinforces why **encryption in transit is critical**.

---
### **Secure Communication in the Cloud**
Cloud-native secure communication includes:
- TLS everywhere (service-to-service)
- Private endpoints
- Encrypted APIs
- Mutual TLS (mTLS — both client and server authenticate)

Cloud exam angle:
> “Prevent eavesdropping between services” → encrypted internal traffic

---
### **Common Secure Communication Attacks**
Knowing _what breaks secure communication_ is exam-relevant:
- **On-path (MITM) attacks** → prevent with TLS
- **Downgrade attacks** → prevent with strong config
- **Certificate spoofing** → prevent with validation
- **Replay attacks** → prevented with nonces/timestamps

---
### **How Secure Communication Connects to Previous Topics**
This topic is deeply integrated with what we’ve already covered:

| Previous Topic                                                                | Connection                                      |
| ----------------------------------------------------------------------------- | ----------------------------------------------- |
| **[[12-Encrypting-Data\|Encryption]]**                                        | TLS, IPsec, SSH rely on encryption              |
| **[[11-Public-Key-Infrastructure\|PKI]] & [[18-Certificates\|Certificates]]** | Enable authentication & trust                   |
| **[[47-On-path-Attacks\|On-path Attacks]]**                                   | TLS/IPsec mitigate MITM                         |
| **[[70-Network-Appliances\|Firewalls & Appliances]]**                         | TLS termination, inspection                     |
| **[[60-Intrusion-Prevention\|Intrusion Prevention]]**                         | Encrypted traffic limits inspection             |
| **[[55-Cloud-Infrastructure\|Cloud Infrastructure]]**                         | Encrypted service communication                 |
| **[[06-Zero-Trust\|Zero Trust]]**                                             | Encrypted, authenticated connections everywhere |
| **[[50-Application-Attacks\|Application Security]]**                          | HTTPS is mandatory                              |
| **VPNs**                                                                      | Secure remote communication                     |

Secure communication is the **default assumption** in modern security architecture.