# States Of Data
This topic answers one deceptively simple question:
> **Where is the data right now?**

Because the **correct protection depends entirely on the data’s state**, not just its classification.

Security+ loves to give you a scenario and ask:
- _“Which control BEST protects this data?”_

The answer is almost always determined by the **state of data**.

---
### **The Three States of Data (Must Memorize Exactly)**
There are **three** — no more, no less.

| State               | Meaning                         |
| ------------------- | ------------------------------- |
| **Data at Rest**    | Stored, not actively moving     |
| **Data in Transit** | Actively moving between systems |
| **Data in Use**     | Being actively processed        |

Every exam question about data protection maps to **one of these three**.

---
### **Data at Rest**
#### **What it is**
Data that is **stored on a medium**.

Examples:
- Files on disk
- Databases
- Backups
- Snapshots
- USB drives
- Cloud object storage

If the data is **sitting still**, it is _at rest_.

#### **Primary Risks**
- Theft of storage media
- Unauthorized access
- Data exfiltration after breach

#### **Primary Controls**
- **Disk encryption** (BitLocker, FileVault)
- **Database encryption**
- **Access control (ACLs, permissions)**
- **Key management (HSM, KMS)**

#### **Exam Triggers**
> “Lost laptop” → Data at rest  
> “Stolen hard drive” → Data at rest  
> “Protect stored data” → Encryption at rest
---
### **Data in Transit**
#### **What it is**
Data that is **moving between systems**.

Examples:
- Web traffic
- Email transmission
- API calls
- File transfers
- VPN traffic

If the data is **crossing a network**, it is _in transit_.

#### **Primary Risks**
- Eavesdropping
- On-path (MITM) attacks
- Packet capture

#### **Primary Controls**
- **TLS (HTTPS)**
- **IPsec (VPNs)**
- **SSH / SFTP**
- **Encrypted email protocols**

#### **Exam Triggers**
> “Protect data while being transmitted” → Encryption in transit  
> “Prevent eavesdropping” → TLS / IPsec  
> “Secure communication between systems” → Data in transit controls
---
### **Data in Use (Most Commonly Missed)**
#### **What it is**
Data that is **actively being processed by the system**.

Examples:
- Data in RAM
- Data being processed by a CPU
- Data inside application memory
- Open files actively used

This is the **hardest state to protect**.

#### **Primary Risks**
- Memory scraping
- Malware reading process memory
- Privilege escalation attacks

#### **Primary Controls**
- **Process isolation**
- **Trusted execution environments (TEE)**
- **Secure enclaves**
- **Application sandboxing**
- **Least privilege**

Encryption alone **does not protect data in use**.

#### **Exam Triggers**
> “Data being processed” → Data in use  
> “Memory-based attack” → Data in use  
> “Protect sensitive data while applications run” → Data in use controls
---
### **Mapping States of Data to Controls (Exam Gold)**
This is one of the **most important tables** in Security+.

| State      | Best Control                 |
| ---------- | ---------------------------- |
| At rest    | Encryption, access control   |
| In transit | TLS / IPsec                  |
| In use     | Memory protection, isolation |

If you ever feel stuck on a question:
1. Identify the data state
2. Apply the matching control
---
### **Relationship to Data Classification**
Data classification tells you **how strong** protection must be.  
Data state tells you **which type** of protection to use.

Example:
- Restricted data + at rest → strong encryption + strict ACLs
- PII + in transit → TLS
- Authentication secrets + in use → secure memory handling

These two topics are always tested **together**.

---
### **Cloud Context (Very Testable)**
Cloud environments involve **all three states constantly**:
- At rest → encrypted storage (S3, disks, databases)
- In transit → TLS between services
- In use → memory inside VMs/containers

Exam trick:
> “Cloud provider encrypts storage by default”  
> → Still need **encryption in transit and access control**
---
### **Common Exam Traps**
#### **Trap 1: Encryption Everywhere**
Encryption is powerful, but:
- It protects **at rest** and **in transit**
- It does **not** protect data in use

#### **Trap 2: Confusing Transit vs Use**
- Moving over a network → _in transit_
- Inside RAM being processed → _in use_

#### **Trap 3: Overthinking**
Security+ does **not** expect deep cryptographic memory protections — just **correct categorization**.

---
### **How States of Data Connect to Previous Topics**
This topic is a **bridge** across many areas we’ve covered:

| Previous Topic                                                              | Connection                                |
| --------------------------------------------------------------------------- | ----------------------------------------- |
| **[[12-Encrypting-Data\|Encryption]]**                                      | Applied differently per data state        |
| **[[73-Secure-Communication\|Secure Communication]]**                       | Protects data in transit                  |
| **[[74-Data-Types-&-Classifications#Data Types and Classifications\|DLP]]** | Prevents data leakage regardless of state |
| **[[55-Cloud-Infrastructure\|Cloud Security]]**                             | Data exists in all states simultaneously  |
| **[[25-Memory-Injections\|Memory Attacks]]**                                | Target data in use                        |
| **[[54-Hardening-Techniques\|Hardening]]**                                  | Reduces exposure of data in use           |
| **[[06-Zero-Trust\|Zero Trust]]**                                           | Controls access to data in all states     |
| **Incident Response**                                                       | Impact depends on state + classification  |

States of data explain **why different controls exist**, not just _what they are_.