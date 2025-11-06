# Key Exchange
**Key exchange** is the **process of securely sharing encryption keys** between two parties (like client and server) ao that they can encrypt and decrypt privately.

Answers: *How do we both end up with the same secret key - without anyone else learning it*

This is the heart of encryption in practice. You can't use symmetric encryption until both sides safely share that key.

---

### Why Key Exchange Matters
- **Symmetric encryption** (like AES) is fast but requires a **shared secret key**
- **Asymmetric encryption** (like RSA or Diffie-Hellman) is slower but can be used to **securely exchange** that key
- So modern systems combine them (hybrid encryption)

`Asymmetric Encryption` is used to **lock the key** inside an envelope
`Symmetric Encryption` is used to **lock the data** inside a safe

---

### Two Main Categories Of Key Exchange
| Method | Description | Example |
| --- | --- | --- |
| Static (pre-shared) | The key is manually configured ahead of time | Shared key in WPA2-PSK Wi-Fi, VPN pre-shared key |
| Dynamic (Ephemeral) | Keys are generated *on the fly* for each session | TLS, IPsec using Diffie-Hellman |

Static = *same key reused*; Dynamic = *new key each time*

---

### Common Key Exchange Methods
#### Diffie-Hellman (DH)
This is the **classic algorithm** for secure exchange:
- Developed in the 1970s
- Allows two parties to **generate a shared secret** over an insecure network **without ever sending the key itself**
- Based on complex math involving modular arithmetic and large prime numbers

How it works (Conceptually Simplified):
1. Both parties agree on public base numbers
2. Each side generates its own private key
3. They compute and exchange public values
4. Each side performs a final calculation combining its private key with the other side's public value
5. Both end up with the **same shared secret**, even though it was never transmitted

**Key advantage**: Even if someone captures all traffic, they can't compute the shared key without the private values

**Diffie-Hellman Variants**:
- **DH Groups**: Define the mathematical parameters and key size
- **DHE (Diffie-Hellman Ephemeral)**: Generates a temporary key for each session - enables **Perfect Forward Secrecy (PFS)**
- **ECDH (Elliptic Curve Diffie-Hellman)**: Uses elliptic curve cryptography - same security, smaller keys - faster and lighter for mobile or IoT

If you see **Perfect Forward Secrecy** or **Ephemeral Keys** it's most likely **DHE** or **ECDHE**

#### RSA (Key Exchange Variant)
RSA isn't primarily a key exchange algorithm, but it's often used for **securely sending a symmetric key** during TLS handshakes.
1. The client generates a random symmetric key
2. Encrypts it using the server's public RSA key (from its certificate)
3. Server decrypts it with its private RSA key
4. Both now share that symmetric session key

**Downside**: RSA key exchange doesn't provide **Perfect Forward Secrecy** - if the server's private key is compromised later, old sessions can be decrypted. This is why modern TLS prefers **ECDHE**

#### Elliptic Curve Diffie-Hellman (ECDH)
- Modern, efficient version of DH
- Uses **elliptic curve mathematics** instead of large prime numbers
- Offers the same security with **smaller key sizes** (better performance)
- Common in TLS 1.3, mobile, IoT, and VPNs

| Algorithm | Key Size | Equivalent RSA Strength |
| --- | --- | --- |
| ECDH 256-bit | about RSA 3072-bit | Much faster & lighter |

If you see mobile, VPN, or performance focused security - ECC or ECDH

#### Pre-Shared Keys (PSK)
- A **static key** configured on both sides ahead of time
- No key exchange occurs - both already know the key
- Used in smaller or simpler setups like WPA2-Personal Wi-Fi or small-site VPNs

PSK = Easy setup, less secure (if leaked, all sessions are compromised)

----

### Perfect Forward Secrecy (PFS)
This is a **security property** provided by ephemeral key exchange (DHE / ECDHE)

Even if the long-term private key is compromised later, past session data **cannot be decrypted**, because each session used a unique, temporary key.

---

### EXAM PITFALLS
| Misunderstanding | Clarification |
| --- | --- |
| Diffie-Hellman encrypts data | No, it generates a shared key for encryption |
| RSA provides Perfect Forward Secrecy | No, only DHE / ECDHE do |
| Key exchange uses symmetric encryption | No, key exchange uses asymmetric, but result is a symmetric key |
| TLS only uses asymmetric encryption | It uses both (asymmetric for key exchange, symmetric for data)