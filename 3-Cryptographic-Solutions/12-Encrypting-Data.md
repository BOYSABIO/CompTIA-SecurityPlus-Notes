# Encrypting Data
**Encryption** is the process of **converting plaintext into ciphertext** so that only authorized parties can read it.

Decryption reverses that process back into plaintext.

Think of it like locking data in a digital safe - only someone with the key can open it.

Encryption is a **core method of ensuring `confidentiality` in the CIA Triad**

---

### Core Terms To Know
| Term | Definition |
| --- | --- | 
| Plaintext | The original readable data |
| Ciphertext | The encrypted, unreadable data |
| Cipher | The algorithm or method used to encrypt / decrypt |
| Key | The secret value used with the cipher to lock or unlock data |
| Encryption strength | Determined by key length (longer = stronger) and algorithm security |
| Cryptanalysis | The study of breaking or defeating encryption |

---

### The Main Types Of Encryption
#### Symmetric Encryption (Secret-Key Encryption)
- Same key used to encrypt and decrypt
- Very fast - ideal for encrypting large amounts of data (e.g. files, full disks, VPN tunnels)
- The challenge: securely sharing the key

| Feature | Description |
| --- | --- |
| Speed | Fast - minimal processing overhead |
| Key use | One shared key |
| Best for | Bulk data encryption |
| Weakness | Key distribution (how do you share it safely) |

Common algorithms:
- **AES** (Advanced Encryption Standard) - modern standard; secure and efficient
- **3DES** (Triple DES) - legacy replacement for old DES
- **Blowfish / Twofish** - older but still conceptually relevant
- **ChaCha20** - lightweight alternative for mobile / IoT devices

Modern **AES** (for extra context):
- **ECB** (Electronic Codebook): Insecure - identical blocks = identical ciphertext
- **CBC** (Cipher Block Chaining): More secure, uses initialization vector (IV)
- **GCM** (Galois / Counter Mode): Adds authentication + speed - common in modern TLS

AES with 256-bit keys is the **gold standard** for most use cases today.

#### Asymmetric Encryption (Public-Key Encryption)
- Uses **two different but mathematically linked keys**: one public, and one private
- Public key encrypts data; private key decrypts it
- Slower than symmetric encryption but enables **secure key exchange** and **digital signatures**

| Feature | Description |
| --- | --- | 
| Keys | Two related keys (public / private) |
| Best for | Key exchange, authentication, signing |
| Speed | Slower than symmetric |
| Used in | PKI, SSL / TLS, email, SSH |

Common Algorithms:
- **RSA** (Rivest-Shamir-Adleman): Widely used for digital signatures and key exchange
- **ECC** (Elliptic Curve Cryptography): Smaller key sizes, same strength - ideal for mobile / IoT
- **Diffie-Hellman** (DH): Used for securely exchanging symmetric keys
- **ElGamal**: Another asymmetric system, less common

Asymmetric = key exchange and digital signatures

Symmetric = bulk data encryption

---

### How They Work Together
Most real world systems (like HTTPS/TLS, VPNs, email) use **both**:
1. Asymmetric encryption first to **securely exchange symmetric key**
2. Symmetric encryption then encrypts all data using that shared key (because it's faster)
- This is called a **Hybrid Encryption System**

Example (TLS Handshake):
1. Browser connects to website - retrieves server's certificate (public key)
2. Browser generates a random symmetric key - encrypts it with the server's public key
3. Server decrypts that key with its private key
4. Both now share the same symmetric key - use it for all data transfer

---

### Key Concepts Related to Encryption
#### Key Exchange
- How encryption keys are securely shared between parties
- **Diffie-Hellman (DH)** and **Elliptic Curve Diffie-Hellman (ECDH)** are standard methods

#### Key Stretching
- Strengthening weak passwords by running them through algorithms like **PBKDF2**, **bycrypt**, or **scrypt** repeatedly to slow down brute force attacks

#### Key Rotation
- Changing encryption keys periodically to limit exposure if one is compromised

#### Key Escrow
- Storing a copy of encryption keys with a trusted third party for recovery or compliance purposes

#### Ephemeral Keys
- Temporary, short-lived keys used in session encryption (like **Perfect Forward Secrecy** in TLS)

---

### Encryption At Rest, In Transit, And In Use
| Type | Description | Example |
| --- | --- | --- |
| At Rest | Data stored on disk | Full-disk encryption, database encryption |
| In Transit | Data being transmitted | HTTPS, VPN, TLS |
| In Use | Data actively processed in memory | Secure enclaves, encrypted RAM, homomorphic encryption (advanced) |

Know that **TLS** protects data in transit and **BitLocker** protects data at rest.

---

### Hashing vs Encryption (Common Confusion)
| Feature | Encryption | Hashing |
| --- | --- | --- |
| Reversible? | Yes (with key) | No (one-way) |
| Purpose | `Confidentiality` | `Integrity` |
| Example Algorithms | AES, RSA | SHA-256, MD5 |
| Use Cases | Secure Data | Verify file or password |

Hashing = fingerprint (detects changes); Encryption = safe (protects content)

---

### Common Encryption Applications
| Use Case | Technology | Example |
| --- | --- | --- |
| Secure websites | TLS/SSL | HTTPS | 
| Secure email | S/MIME, PGP | Signed & encrypted mail |
| Full Disk Encryption | BitLocker, FileVault | Laptop or drive protection |
| VPNs | IPsec, SSL VPN | Secure remote access |
| Wireless encryption | WPA3, EAP-TLS | Wi-Fi security |

---

### Encryption In The CIA Triad
| CIA Principle | How Encryption Supports It |
| --- | --- |
| Confidentiality | Prevents unauthorized access |
| Integrity | Often paired with hashing and signatures |
| Availability | Encrypted backups ust still be accessible with proper keys |

---

### WATCH OUT FOR
- Symmetric = one key, fast bulk encryption
- Asymmetric = two keys, slower, used for key exchange and signatrues
- Public encrypts / private decrypts (for confidentiality)
- Private signs / public verifies (for authenticity and non-repudiation)
- PKI != encryption itself - PKI manages trust and keys, encryption performs data protection
- Diffie-Hellman = key exchange, AES = symmetric data encryption

