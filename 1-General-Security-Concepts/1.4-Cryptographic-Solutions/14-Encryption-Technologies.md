# Encryption Technologies
These are **specific tools, protocols, and systems** that use encryption to protect data in different **states**:
- **At Rest** - Stored on a disk or media
- **In Transit** - Moving over networks
- **In Use** - Being processed in memory

Each of these has different risks and different solutions 

---

### Data At Rest (Stored Data)
The goal is to protect stored data from unauthorized access if the device is lost, stolen, or compromised

| Method | Description | Example |
| --- | --- | --- |
| Full Disk Encryption (FDE) | Encrypts the entire storage drive, including OS and files | BitLocker (windows), FileVault (macOS), LUKS (Linux) |
| Volume / Partition Encryption | Encrypts specific partitions or volumes instead of entire disk | VeraCrypt, TrueCrypt |
| Database Encryption | Encrypts stored records or fields in databases | Transparent Data Encryption (TDE) in SQL Server, Oracle |
| File-Level Encryption | Encrypts specific files or folders | EFS (Encrypting File System) |
| Hardware Security Modules (HSMs) | Dedicated devices that generate and store cryptogrphic keys securely | Used by certificate authorities and banks |
| Self-Encrypting Drives (SEDs) | Drives with built-in hardware-based encryoption | Common in enterprise laptops and servers |

If a laptop is stolen and the drive is encrypted, confidentiality is maintained - as long as the encryption key is protected

#### Key Management for Data at Rest
- Keys are often protected using TPM (Trusted Platform Module) chips
- **TPM**: Hardware chip that stores cryptographic keys and verifies boot integrity
- **HSM**: External hardware for key management at scale (e.g. certificate authority)
- If keys are lost or compromised, encrypted data becomes unrecoverable

---

### Data In Transit (Across Networks)
The goal is to prevent eavesdropping, tampering, and impersonation during communication.

| Technology | Description | Example Use |
| --- | --- | --- |
| TLS (Transport Layer Security) | Encrypts data over web traffic (HTTP - HTTPS) | Secure websites, APIs |
| IPsec (Internet Protocol Securit) | Encrypts IP packets at the network layer | VPN tunnels, site-to-site connections |
| SSL VPNs / SSL/TLS VPNs | Use TLS for encrypted remote access | Client-to-server VPNs |
| SSH (Secure Shell) | Secure remote administration | Manage servers securely |
| S/MIME (Secure/Multipurpose Internet Mail Extensions) | Encrypts and signs email files directly using certificates | Corporate email encryption |
| PGP / GPG (Pretty Good Privacy) | Encrypts and signs email files directly using user-managed keys | Personal or open source email security |
| Wireless Encryption (WPA3) | Encrypts Wi-Fi traffic | Home / enterprise networks |
| DNSSEC | Secures DNS queries and responses to prevent spoofing | Domain protection |

TLS (application-layer encryption) and IPsec (network-layer encryption) are **both used to protect data in transit**, but different layers

---

### Data In Use (Processed (In RAM))
*Newer and less visible but growing in importance*: The goal is to protect data while it's being actively used - in memory or during computation.

| Technology | Description | Example |
| --- | --- | --- |
| Secure Enclaves / Trusted Execution Environments (TEE) | Isolated hardware memory areas that protect data during use | Intel SGX, AMD SEV |
| Homomorphic Encryption | Advanced cryptography that allows computation on encrypted data | Used in privacy-preserving cloud analysis |
| RAM Encryption / Memory Protection | Protects data temporarily stored in memory | Used in secure hardware or OS-level features |

---

### End-to-End Encryption (E2EE)
- Data is encrypted by the **sender** and only decrypted by the **recipient**
- No intermediary (even the service provider) can read the contents

Examples:
- Signal, WhatsApp, iMessage - encrypted between users, not in servers
- S/MIME or PGP - user-to-user email encryption

End-to-end encryption protects data in transit and ensures true confidentiality, even from service providers.

---

### Network-Level Encryption Technologies
| Technology | Function | Common Use |
| --- | --- | --- |
| IPsec (Transport vs Tunnel Mode) | Encrypts packets | Site-to-site or client VPNs | 
| SSL/TLS | Encrypts application sessions | HTTPS, secure APIs |
| MACsec (Media Access Control Security) | Encrypts traffic at layer 2 | Enterprise LANs |
| DNSSEC | Validates DNS integrity | Domain security |
| Email Encryption (S/MIME, PGP) | Encrypts mail content | Secure messaging |

Be ready to identify which layer or purpose each technology serves 

---

### Encryption Technologies For Wireless Networks 
| Standard | Encryption Method | Notes |
| --- | --- | --- |
| WEP | RC4 (weak) | Depreciated - easily cracked |
| WPA / WPA2 | TKIP (old) or AES (stronger) | WPA2-AES still common |
| WPA3 | SAE (Simultaneous Authentication of Equals) | Modern, resistant to offline dictionary attacks |

When it comes to securing a wifi always choose **WPA3-AES (CCMP)**

---

### File & Communication Encryption Tools
| Tool | Description | Example Use |
| --- | --- | --- |
| BitLocker / FileVault | Full Disk Encryption | Protects Laptops |
| GPG / PGP | File or email encryption | Send secure files |
| OpenVPN / IPsec | Network encryption | Remote access |
| S/MIME | Email encryption using certificates | Enterprise messaging | 
| SSH | Encrypted command-line access | Secure server management |
| HTTPS (TLS) | Web encryption | Secure web traffic |

---

### Encryption Layers & Examples
| Encryption Layer | Technology Example | Protects |
| --- | --- | --- |
| Physical | Self-encrypting drives | Data At Rest |
| Network | IPsec, MACsec | Data In Transit |
| Transport / Session | TLS, SSH | Application Data |
| Application | S/MIME, PGP | User messages | 
| Storage / File System | BitLocker, FileVault | Stored files |

---

### Key Takeaways for COMPTIA
1. **TLS and IPsec** - most common *data in transit* encryption protocols
2. **BitLocker and FileVault** - full disk enryption = *data at rest*
3. **S/MIME and PGP** - Email encryption technologies
4. **WPA3** - modern wireless encryption (uses AES and SAE)
5. **HSM and TPM** - secure key storage
6. **Perfect Forward Secrecy** - provided by ephemeral key exchange (DHE / ECDHE)
7. **End-to-end Encryption** - Sender -> recipient, not readable by intermediaries

---

## Related Notes
- [[11-Public-Key-Infrastructure]]
- [[12-Encrypting-Data]]
- [[73-Secure-Communication]]
- [[74-Data-Types-&-Classifications]]
