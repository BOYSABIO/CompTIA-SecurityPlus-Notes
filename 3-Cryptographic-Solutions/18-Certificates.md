# Certificates
A **Digital Certificate** is an **electronic credential** that binds a **public key** to a specific identity (a person, device, or organization)

Think of it like a digital driver's license for encryption - it proves who you are and lets others trust your public key.

It's issued and verified by a **Certificate Authority (CA)** within a **Public Key Infrastructure (PKI)**

---

### Purpose Of Certificates
Certificates provide **trust** in digital communications through four key principles. 
| Goal | Description |
| --- | --- | 
| Authentication | Confirms the entity's identity (e.g., website, server, user) |
| `Integrity` | Prevents data from being altered undetected |
| `Confidentiality` | Enables encryption via public keys |
| Non-repudiation | Provides proof that data came from a specific source |

---

### Certificate Components
Each digital certificate contains specific fields that define *who, what, and how* it's trusted.
| Field | Description |
| --- | --- |
| Subject | Entity the certificate belongs to (e.g., example.com) |
| Issuer | The Certificate AUthority that issued it |
| Public Key | The key associated with the subject |
| Serial Number | Unique identifier for the certificate |
| Validity Period | "Not before" and "Not after" dates |
| Signature | Digital signature of the CA (verifies authenticity) |
| Extensions | Extra info like usage type or constraints |

The Certificate Authorities digital signature is what makes a certificate *trusted* - without it, it's just a file with data.

---

### How Certificates Work In PKI
Here's how the trust process happens (using HTTPS as an example):
1. **Server sends its certificate** (contains public key + info)
2. **Browser Checks:**
    - Is the certificate **issued by a trusted CA?**
    - Is it **valid and not expired?**
    - Is it **not revoked?**
    - Does the **domain name match?**
3. If all checks pass, browser **trusts the server's identity** and establishes encrypted communication

The **chain of trust** leads from your browser's **trusted root CA** -> intermediate CA -> the website's certificate.

---

### Certificate Authority Hierarchy
| CA Type | Description | Example |
| --- | --- | --- |
| Root CA | The ultimate trust anchor (self-signed) | DigiCert Global Root CA |
| Intermediate / Subordinate CA | Issued by the root; signs end-entity certificates | Let's Encrypt R3 |
| Issuing CA | Issues the actual end-user or device certificates | Web or email certificates |
| Registration Authority (RA) | Verifies identities and forwards requests to the CA |

**Root CA**
: Ultimate trust anchor

**Registration Auhtority**
: Verities the identity before issuing a cert

---

### Certificate Lifecycle
| Stage | Description |
| --- | --- |
| Request (CSR) | Entity submits a Certificate Signing Request with their public key |
| Issuance | CA validates identity an dsigns the certrificate |
| Distribution | Ceritificate is installed and used in systems |
| Renewal | Issued again before expiration |
| Revocation | Certificate invalidated before expiration (e.g., compromised key) |

If a kye is compromised or an employee leaves, revoke the certificate via a **CRL** or **OCSP**

---

### Certificate REvocation
| Method | Description | Strength |
| --- | --- | --- |
| CRL (Certificate Revocation List) | List of revoked certificates published by the CA | Slower, older method |
| OSCP (Online Certificate Status Protocol) | Real-time validation of certificate status | Faster, more modern |

**OSCP**
: Real-time revocation checking

**CRL**
: Offline list of invalid certs

---

### Common Certification Types
| Certification Type | Description | Example Use |
| --- | --- | --- |
| Root | Self-signed CA certificate (top of trust chain) | Trusted by OS / browsers |
| Intermediate / Subordinate | Issued by root to delegate trust | "R3" intermediate for let's encrypt |
| Server (SSL/TLS) | Authenticates servers for HTTPS | Web servers |
| Client | Authenticates users/devices | VPN, 802.1X authentication |
| Code Signing | Verifies software authenticity | Signed apps / drivers |
| Email / S/MIME | Encrypts & signs email messages | Secure corporate email |
| Document Signing | Used in PDF's or contracts | Legal or business docs |
| Machine / Device | For IoT or endpoint identification | Smart devices sensors |
| Wildcard | Covers a domain and all subdomains | `*.example.com` |
| SAN (Subject Alternative Name) | Covers multiple specific domains | `example.com`, `mail.example.com` |

**SAN Cert**
: Certificate for multiple domains

**Wildcard Cert**
: Certificate for all subdomains

**Self-signed Cert**
: Issued and signed by same org

---

### Certificate Formats (File Types)
| Extension | Format | Description |
| --- | --- | --- |
| .CER / .CRT | DER or PEM | Base certificate (public key only) |
| .PEM | Base46 ASCII format (-----BEGIN CERTIFICATE-----) | Common for web servers |
| .DER | Binary format of X.509 certificate | Used in java environments |
| .PFX / .P12 | PKCS#12 format (includes public + private key) | Common for windows systems |
| .P7B | PKCS#7 (chain of certs, no private key) | Used for certificate bundles |

**.PFX or .P12**
: Certificate file that includes private key

**.P7B**
: Certificate chain only

---

### Certificate Attributes / Extensions
Certificates can specify how they're used via extensions:
| Extension | Purpose |
| --- | --- |
| Key Usage | Defines what the key can do (signing, encryption, key exchange) |
| Extended Key Usage (EKU) | Defines specific applications (server auth, email protection, code signing) | 
| Basic Constraints | Identifies if the certificate can issue other (CA = True) |
| SAN (Subject Alternative Name) | Lists additional hostnames or domains |

**Key Usage / EKU**
: Certificate field that defines its purpose

**SAN**
: Certificate for multiple hostnames

---

### Trust Models
| Model | Description | Example |
| --- | --- | --- |
| Hierarchical (Most Common) | Root -> Intermediate -> End-Entity | Internet PKI |
| Bridge | Links multiple PKI hierarchies for cross-trust | Large organizations or governments |
| Web of Trust | Peer-based trust (no central CA) | PGP / GPG |
| Mesh | Multiple entities trust each other directly | Internal federations |

**Web of Trust**
: Used in PGP where users verify each other's identities

---

### Certificate Validation Steps (At a Glance)
1. **Check signature** - was it signed by a trusted CA?
2. **Check validity period** - not expired or not yet valid?
3. **Check revocation status** - CRL or OCSP
4. **Check name match** - domain name matches certificate
5. **Check purpose** - key usage and extensions are correct

