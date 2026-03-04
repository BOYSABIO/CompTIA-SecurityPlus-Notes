# Protecting Data
Protecting data means applying **technical, administrative, and physical controls** to ensure:
- **[[02-The-CIA-Triad#Confidentiality|Confidentiality]]** – unauthorized users can’t read it
- **[[02-The-CIA-Triad#Integrity|Integrity]]** – data can’t be altered undetected
- **[[02-The-CIA-Triad#Availability|Availability]]** – authorized users can access it when needed

Everything in this topic is about **choosing the right control based on**:
- Data **type**
- Data **classification**
- Data **state**
- **Threat model**
---
### **Encryption (Primary Data Protection Control)**
Encryption is the **default answer** in many data-protection questions — but only when applied correctly.

#### **2.1 Encryption at Rest**
Protects **stored data**.

Examples:
- Full-disk encryption (BitLocker, FileVault)
- Database encryption
- Encrypted cloud storage
- Encrypted backups

Used when:
- Devices may be lost or stolen
- Storage is shared or cloud-based

Exam trigger:
> “Lost laptop / stolen drive” → **Encrypt data at rest**

#### **2.2 Encryption in Transit**
Protects **data moving across networks**.

Examples:
- TLS (HTTPS)
- IPsec (VPNs)
- SSH / SFTP
- Secure email protocols

Used when:
- Preventing eavesdropping
- Protecting API calls
- Securing remote access

Exam trigger:
> “Prevent eavesdropping / MITM” → **Encrypt data in transit**

#### **2.3 Encryption in Use (Limited but Important)**
Encryption does **not naturally protect data in memory**.

Mitigations:
- Secure enclaves / TEEs
- Memory isolation
- Least privilege
- Application sandboxing

Security+ does not go deep here — just understand the limitation.

---
### **Access Control (Who Can Touch the Data)**
Encryption protects data **if stolen**.  
Access control protects data **from being accessed in the first place**.

#### **3.1 Logical Access Controls**
- ACLs (Access Control Lists)
- RBAC (Role-Based Access Control)
- Least privilege
- MFA for sensitive data access

Exam trigger:
> “Only authorized users should access data” → **Access control**

#### **3.2 Physical Access Controls**
- Locked server rooms
- Secure storage
- Badge access
- Mantraps

Protects against:
- Physical data theft
- Unauthorized device access

---
### **Data Loss Prevention (DLP)**
DLP focuses on **preventing sensitive data from leaving the organization**.

Monitors:
- Email
- Web uploads
- File transfers
- Cloud sharing

Detects patterns like:
- Credit card numbers
- SSNs
- Medical data

Exam trigger:
> “Prevent sensitive data from being emailed or uploaded” → **DLP**

DLP is **classification-driven**.

---
### **Data Masking, Tokenization, and Obfuscation**
These protect data by **reducing exposure**, not by encrypting everything.
#### **5.1 Data Masking**
Replaces sensitive data with partially hidden values.

Example:
- `****-****-****-1234`

Used for:
- Displays
- Logs
- Customer support systems

#### **5.2 Tokenization**
Replaces sensitive data with a random token.

Example:
- Credit card number → token stored instead

Used heavily in:
- Payment systems
- PCI environments

Key idea:
> Original data stored securely elsewhere.

#### **5.3 Obfuscation**
Makes data harder to understand but **not cryptographically secure**.

Used for:
- Source code
- Scripts
- Intellectual property protection

Exam note:
> Obfuscation ≠ encryption
---
### **Hashing & Integrity Controls**
Used to protect **data integrity**, not confidentiality.

Examples:
- Password hashing
- File integrity monitoring
- Digital signatures

Exam trigger:
> “Detect unauthorized modification” → **Hashing / integrity checks**
---
### **Key Management (Often Tested Indirectly)**
Encryption is useless if keys are mishandled.

Key management includes:
- Secure key storage (HSM, KMS)
- Key rotation
- Key revocation
- Separation of keys and data

Exam trigger:
> “Protect encryption keys” → **HSM / KMS**
---
### **Backups & Data Resilience**
Data protection also includes **recoverability**.

Key ideas:
- Regular backups
- Offline / immutable backups
- Encrypted backups
- Tested restore procedures

Exam trigger:
> “Recover after ransomware” → **Backups**

Availability is part of data protection.

---
### **Data Lifecycle Protection**
Protection must apply **throughout the data lifecycle**:
1. Creation
2. Storage
3. Use
4. Sharing
5. Archival
6. Destruction

Secure destruction:
- Crypto-shredding
- Secure wiping
- Physical destruction

Exam trigger:
> “Ensure data cannot be recovered after disposal” → **Secure destruction**
---
### **Cloud-Specific Data Protection Considerations**
Cloud adds risk through:
- Misconfigured storage
- Over-shared access
- Replication

Controls:
- Encryption (default + customer-managed keys)
- Private endpoints
- IAM restrictions
- DLP
- Logging

Exam reminder:
> **Data sensitivity does not change in the cloud.**
---
### **How Protecting Data Connects to Previous Topics**
This topic is a **convergence point**:

| Previous Topic                                                                 | Connection                       |
| ------------------------------------------------------------------------------ | -------------------------------- |
| **[[74-Data-Types-&-Classifications\|Data Types & Classification]]**         | Determines protection strength   |
| **[[75-States-Of-Data\|States of Data]]**                                      | Determines protection method     |
| **[[12-Encrypting-Data\|Encryption]] & [[11-Public-Key-Infrastructure\|PKI]]** | Core protection mechanisms       |
| **DLP**                                                                        | Prevents data exfiltration       |
| **[[52-Segmentation-&-Access-Control\|Access Control]]**                       | Enforces least privilege         |
| **[[73-Secure-Communication\|Secure Communication]]**                          | Protects data in transit         |
| **[[34-Cloud-specific-Vulnerabilities\|Cloud Security]]**                      | Misconfiguration = data exposure |
| **Incident Response**                                                          | Impact depends on data protected |
