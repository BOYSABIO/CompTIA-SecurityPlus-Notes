# Blockchain Technology
**Blockchain** is a **distributed, immutable digital ledger** that records transactions securely across a network of computers.

It's a shared database that everyone can see, but no one can easily alter

Each record (block) in the chain is cryptographically linked to the previous one - making it **tamper-evident and transparent**

Blockchain's main goal isn't `confidentiality` - it's `integrity` and **trust without a central authority**

---

### Core Characteristics
| Property | Description | 
| --- | --- |
| Distributed | Copies of the ledger exist on many nodes - no single point of control |
| Immutable | Once the data is recorded, it can't be modified without breaking the chain |
| Transparent | Every participant can verify transactions |
| Cryptographically Linked | Each block contains the hash of the previous block |
| Consensus-based | Network participants agree on valid transactions before adding them |

---

### Structure Of A Blockchain
Each **block** contains:
- **Transaction data** (e.g., who sent what to whom)
- **Timestamp**
- **Hash of the previous block** (links the chain)
- **Nonce / Proof Data** (used for vaildation)

**Chaining** happens because each block's header includes the **hash of the previous block**, forming a continuous chain - if one block changes, every subsequent hash breaks

*This makes blockchains temper-evident by design*

---

### Cryptographic Foundations
**Hashing**
- Each block's data is hashed (e.g., SHA-256)
- Any tiny change to data -> completely different hash -> invalidates the block

**Digital Signatures**
- Used to sign and verify transactions
- Confirms the **authentication** of who created the transaction

**Public / Private Key**
- Every participant has a **key pair**:
    - Private key -> signs transactions
    - Public key -> verifies signatures and identity

**Merkle Trees**
- Used to efficiently verify large sets of transactions within a block
- Each transaction is hashed, then combined and hashed again up the tree until one **root hash** summarizes all the transactions

*If one transaction changes*, the Merkle root changes -> whole block invalid

---

### Consensus Mechanisms
Because there's no central authority, blockchain networks must agree on which transactions are valid - that's the consensus process
| Mechanism | Description | Example | Strength |
| --- | --- | --- | --- |
| Proof of Work (PoW) | Nodes compete to solve complex math puzzles (mining). First to solve adds the block | Bitcoin | High security, high energy use |
| Proof of Stake (PoS) | Validators are chosen based on how much cryptocurrency they "stake" | Ethereum (post merge) | Energy Efficient |
| Delegated Proof of Stake (DPoS) | Participants vote for delegates who validate blocks | EOS | Fast, democratic |
| Proof of Authority (PoA) | Only trusted nodes validate blocks (common in private chains) | Enterprise blockchains | Centralized trust, fast |

You don't need math or deep details - just understand **consensus = agreement without central authority**

---

### Security Principles In Blockchain
| Security Property | How Blockchain Provides It |
| --- | --- |
| `Integrity` | Cryptographic hashes make tampering obvious |
| Authentication | Digital ssignatures verify sender identities |
| Non-repudiation | Signed transactions can't be denied later |
| Availability | Decentralization prevents single points of failure |
| Transparency | Public ledgers are visible to all participants |

Blockchain **does not** inherently provide `confidentiality` - everything on a public blockchain is visible, though sometimes pseudonoymous

---

### Types Of Blockchains
| Type | Description | Example Use |
| --- | --- | --- |
| Public (permissionless) | Anyone can join and participate; full transparent | Bitcoin, Ethereum |
| Private (Permissioned) | Access restricted to approved users | Hyperledger, enterprise systems |
| Consortium | Managed by a group of organizations jointly | Banking networks |
| Hybrid | Combines public transparency with private access controls | Supply chain tracking |

**Public Blockchain**
: Open and decentralized

**Private Blockchain**
: Controlled by one organization

---

### Common Uses Of Blockchain
| Use Case | Description |
| --- | --- |
| Cryptocurrency transactions | Bitcoin, Ethereum - transfer of digital assets |
| Smart contracts | Self-executing agreements coded on chain |
| Supply chain management | Track product movement with immutable records |
| Digital identity verification | Decentralized IDs using cryptographic keys |
| Voting system | Transparent, verifiable elections (in pilot stages) |
| Secure recordkeeping | Medical records, property titles, audits |

---

### Weaknesses & Limitations 
| Issue | Description |
| --- | --- |
| Scalability | Large blockchains can be slow to update |
| Energy consumption | PoW models (like bitcoin) use massive computing power |
| Privacy concerns | Public data visibility - not confidential |
| Irreversibility | Mistaken or fraudulent transactions can't be undone easily |
| Key management risk | Loosing a private key = losing access forever |

Blockchain prioritizes `Integrity` and `Availability`, sometimes at the expense of `Confidentiality`

---

### Blockchain vs Traditional Databases
| Feature | Blockchain | Traditional DB |
| --- | --- | --- | 
| Control | Decentralized | Centralized |
| Mutability | Immutable | Editable |
| Verification | Consensus-based | Admin-controlled |
| Transparency | Public / shared | Private |
| Security Model | Integrity first (hashing, signatures) | Access control-based |\


---

### Blockchain & The CIA Triad
| CIA Principle | How Blockchain Supports It |
| --- | --- |
| Confidentiality | Limited (public data often visible) |
| Integrity | Very strong (hash-linked, tamper-evident) |
| Availability | High (decentralized redundancy) |