# Hashing & Digital Signatures
Main points:
- **Encryption** = `Confidentiality` (keeps data secret)
- **Hashing & Signatures** = `Integrity` & `Authenticity` (ensures data isn't changed and proves who sent it)

Encryption *hides* what you send while Hashing & Signatures prove that *what* you sent hasn't been tampered with and *who* it came from.

---

### What Is Hashing?
**Hashing** is a **one-way mathematical process** that converts any input data (file, password, message) into a fixed-length string called a **hash value** or **digest**.

Think of it like a digital fingerprint - unique to the data, but you can't reverse it.

#### Key Properties Of A Hash Function
| Property | Description | Why It Matters |
| --- | --- | --- |
| Deterministic | Same input always gives same output | Reliable verification |
| One-way | Can't derive the original input from the hash | Protects secrets (passwords) |
| Collision-resistant | Two different inputs shouldn't produce the same hash | Prevents tampering or forgery |
| Avalanche effect | Small input change -> big output change | Detects even tiny changes |

Verifying data `Integrity` = **Hashing**

#### Common Hash Algorithms
| Algorithm | Output Length | Notes |
| --- | --- | --- |
| MD5 | 128-bit | Obsolete - collisions possible |
| SHA-1 | 160-bit | Weak - replaced by SHA-2/3 |
| SHA-2 | 244/256/384/512-bit | Industry standard; strong and widely used |
| SHA-3 | Variable length | Modern design, less common yet |
| HMAC | Depends on underlying hash | Adds secret key for authentication (used in TLS, IPsec)

HMAC-SHA256 means hashing + secret key -> verifies `Integrity` and `Authenticity`

#### Common Uses Of Hashing
| Use Case | Description | Example |
| --- | --- | --- |
| Integrity verification | Ensure data hasn't changed | File checksums (SHA256sum) |
| Digital signatures | Sign the hash, not the whole message | Sign message digest with private key |
| Password storage | Store hashed passwords not plaintext | bcrypt, PBKDF2, Argon2 |
| Message authentication | Verify both data and sender identity | HMAC |

Hashing doesn't hide data - it proves data hasn't changed

---

### What Is A Digital Signature?
A **digital signature** is a cryptographic technique that verifies:
1. `Integrity` - message wasn't changed
2. **Authenticity** - it came from the claimed sender
3. **Non-repudiation** - the sender can't deny having sent it

It's like a **tamper-proof seal + signature** combined

#### How It Works (Step-by-Step)
Let's say Alice sends Bob a signed message

**Alice's Side - Creating the Signature**
1. Alice hashes the message using a has algorithm (e.g., SHA-256)
2. She encrypts the **hash** (not the full message) with her **private key**
3. That encrypted hash = **digital signature**
4. She sends Bob the message + the signature

**Bob's Side - Verifying the Signature**
1. Bob decrypts the signature using **Alice's public key**
2. He gets the original hash
3. He hashes the message himself
4. If both hashes match -> message is authentic and unaltered

`Integrity` - Hashes match - message not changed

**Authentication** - Only Alice's private key could create that signature

**Non-repudiation** - Alice can't deny sending it (since only she controls her private key)

#### Digital Signatures & PKI
Digital signatures depend on **Public Key Infrastructure (PKI)**
- Certificates link public keys to identities (users, websites, organizations)
- The **Certificate Authority (CA)** ensures the signature came from a trusted entity

A digital signature isn't just about the math - it's about the **trust chain** behind the key

#### Digital Signature Example
Let's illustrate with HTTPS (website signing):
- The web server's private key signs the TLS certificate
- The CA's public key verifies it
- Your browser trusts the CA, so it trusts the website

This is how PKI ties integrity and trust into encryption.

---

### Hashing + Signing In Practice
| Technology | Use | Notes |
| --- | --- | --- |
| Code Signing | Software developers sign apps or drivers | Confirms authentication (e.g. Windows Drivers) |
| Email Signing (S/MIME) | Verify sender and message integrity | Digital signature on email |
| Document Signing (PDFs) | Legal or business documents | Aobe digital signatures |
| TLS Certificates | Validate servers | PKI signatures verify site identity |

Prove the message came from a specific sender and wasn't modified -> **Digital Signature**

---

### Hashing vs Encryption vs Signing
| Property | Hashing | Encryption | Digital Signature |
| --- | --- | --- | --- |
| Purpose | Verify integrity | Protect confidentiality | Verify identity + integrity |
| Reversible | No | Yes (with key) | Verifiable (with public key) |
| Key Used? | No | Yes (symmetric / asymmetric) | Yes (private key signs, public verifies) |
| Example | SHA-256 | AES | SHA-256 + RSA |

---

### Common CompTIA Questions & Traps
| Trick Question | Correct Thinking |
| --- | --- | 
| Which ensures integrity of downloaded file | Hashing |
| Which ensures sender identity and prevents denial | Digital Signature |
| Which encrypts data for confidentiality | Encryption |
| Which hashing algorithm is no longer secure | MD5 or SHA-1 |
| Which part of digital signature proves authenticity | The private key (used to sign) |

---

### HMAC - Hybrid Concept
**HMAC** (Hash-based Message Authentication Code) adds a shared secret key to the hashing process:
- Ensures `integrity` (hash) and **authentication** (secret key)
- Common in IPsec, TLS, and API authentication

HMAC-SHA256 means: hash with a secret key using SHA-256 -> verifies both sender and mesage integrity

---

## Related Notes
- [[03-Non-repudiation]]
- [[11-Public-Key-Infrastructure]]
- [[21-Phishing]]
- [[49-Malicious-Code]]
