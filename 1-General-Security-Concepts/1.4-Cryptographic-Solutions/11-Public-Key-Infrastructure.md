# Public Key Infrastructure (PKI)
**Public Key Infrastructure (PKI)** is the entire **system of technologies, policies, and procedures** that manages **digital certificates and public / private key pairs**

PKI is how we **trust, verify, and use** encryption on the internet

It supports:
- `Confidentiality` (via encryption)
- `Integrity` (via hashing and digital signatures)
- `Authentication` (via certificate)
- `Non-repudiation` (proof of identity and origin)

So **PKI** is the practical framework that makes cryptography usable and trustworthy across users, devices, and organizations.

---

### Core Concept: Asymmetric Cryptography
**PKI** relies on **asymmetric encryption** - which uses TWO keys that are mathematically related but not identical:
| Key Type | Function | Example Use |
| --- | --- | --- |
| Public Key | Shared freely with anyone | Used to encrypt data or verify digital signatures |
| Private Key | Kept secret by the owner | Used to decrypt data or create digital signatures |

*Rule of Thumb*:
- **Encrypt** with public, **decrypt** with private
- **Sign** with private, **verify** with public

This dual-key system enables secure communication without needing to pre-share a secret

---

### The Role Of PKI
**PKI** provides a trusted system for managing keys and certificates, answering three big questions:
1. **Who are you?** - Identify verification (certificate)
2. **Can I trust you?** - Create authority (CA) validation
3. **Is your key valid?** - Certificate lifecycle (issuance, revocation, expiration)

---

### PKI Components (Building Blocks)
#### Certificate Authority (CA)
- The *trusted root* of PKI
- Issues, manages, renews, and revokes digital certificates
- Validates identities before issuing certs

Types of **CA**:
| Type | Description |
| --- | --- | 
| Root CA | The ultimate trust anchor. It's certificate is self-assigned and trusted by all devices |
| Intermediate / Subordinate CA | Issued by the **Root CA** to distribute the load and risk. Signs end-entity certificates (like for websites) |

If the **Root CA** is compromised, the entire trust chain collapses.

#### Registration Authority (RA)
- Acts as a **middleman** between the user and the **CA**
- Verifies the requesters identity before a certificate is issued
- Think of it as the *Front Desk* of the **CA**

#### Certificate Database / Repository
- Stores issued certificates and certificate revocation lists (CRLs)
- Publicly accessible - so systems can verify certificate status

#### Certificate Revocation List (CRL)
- A list of **invalid** or **revoked** certificates maintained by the **CA**
- Used when keys are compromised or employees leave
- Systems check this to ensure a certificate is still trusted

*Newer alternative*: **OCSP** (Online Certificate Status Protocol)
- Checks certificate validity in **real time** rather than downloading a whole list

#### Digital Certificate
- A digital document that **binds a public key to an identity** (person, server, or device).
- Signed by a **CA** to prove it's authentic

The digital Certificate contains:
- Subject (owner) info
- Public key
- Issuer (CA)
- Validity period
- Serial number
- Digital signature of the **CA**

A digital certificate is like a **driver's license for encryption** - it proves who you are, issued by a trusted authority

---

### How The Trust Chain Works
1. The **CA's Root Certificate** is trusted by your system (pre-installed in your OS / Browser)
2. The **CA signs** a certificate for a website or user
3. When you visit the site, your browser verifies:
    - The certificate was issued by a **trusted CA**
    - The certificate is **valid** (date + not revoked)
    - The certificate **matches the site's domain name**
4. If all checks pass - connection is trusted and secure

This creates a **Chain Of Trust** from your device -> **CA** -> certificate owner

---

### How PKI Supports Common Security Services
| Goal | PKI Function | Example |
| --- | --- | --- | 
| Confidentiality | Encrypts data with public / private keys | HTTPS traffic |
| Integrity | Uses digital signatures + hashing | Signed documents |
| Authentication | Validates identity via certificate | Smart cards, VPNs |
| Non-repudiation | Digital signatures can't be denied | Email signing (S/MIME)

---

### Common PKI Use Cases
| Use Case | Description |
| --- | --- |
| HTTPS / TLS | Web encryption and authentication |
| Email encryption (S/MIME) | Encrypt and sign email messages |
| Code signing | Verify software came from a trusted publisher |
| Document signing | Digital signatures for legal or business docs |
| VPN authentication | Cert-based user or device access |
| Smart cards / tokens | Physical credential tied to digital certificate |
| Wi-Fi authentication (EAP-TLS) | 802.1X wireless security using client certs |

CompTIA often asks which technology relies on certificates to authenticate clients to a wireless network and that would be `EAP-TLS`.

---

### Certificate Lifecycle
| Stage | Description |
| --- | --- | 
| Request | User or device requests a cert (via RA or CSR)
| Issuance | CA verifies identity and issues certificate |
| Use | Certificate used for encryption / signing / authentication |
| Renewal | Issued again before expiration to maintain trust |
| Revocation / Expiration | Invalidated (key compromise, employee leaves, etc)

---

### Exam Tips
- PKI != encryption itself - It's the infrastructure that manages keys and trust
- Root CA compromise - This is catestrophic -> all subordinate certs are untrusted
- CRL vs OCSP:
    - CRL = static list, downloaded periodically
    - OCSP = real-time check
- Digital signature vs encryption:
    - Signature = integrity + authentication
    - Encryption = confidentiality

---

## Related Notes
- [[18-Certificates]]
- [[12-Encrypting-Data]]
- [[16-Hashing-&-Digital-Signatures]]
- [[73-Secure-Communication]]
