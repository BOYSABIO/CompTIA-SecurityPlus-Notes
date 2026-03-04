# Backups
Backups exist to ensure:
> **Data can be restored after corruption, deletion, ransomware, or disaster.**

Security+ tests:
- Backup types
- Tradeoffs
- Recovery speed
- Storage impact
- RPO/RTO alignment
- Ransomware resilience

---
### Core Backup Types (Must Know Cold)
These are almost guaranteed exam material.
#### 1. Full Backup
- Copies **all data**
- Most complete
- Simplest restore process
##### Pros
- Fastest restore
- Simple
##### Cons
- Large storage use
- Slow backup time

Restore requires:  
Only the latest full backup.

#### 2. Incremental Backup
- Backs up data changed since **last backup (any type)**

Example:
- Monday: Full
- Tuesday: Incremental
- Wednesday: Incremental
##### Pros
- Smallest storage use
- Fastest backup time
##### Cons
- Slowest restore

Restore requires:  
Full backup + every incremental after it.

#### 3. Differential Backup
- Backs up data changed since **last full backup**

Example:
- Monday: Full
- Tuesday: Differential
- Wednesday: Differential
##### Pros
- Faster restore than incremental
- Moderate storage use
##### Cons
- Backup size grows daily

Restore requires:  
Full backup + latest differential only.

#### Restore Speed Comparison (Very Testable)

| Type         | Backup Speed | Storage | Restore Speed |
| ------------ | ------------ | ------- | ------------- |
| Full         | Slow         | Large   | Fast          |
| Incremental  | Fast         | Small   | Slow          |
| Differential | Medium       | Medium  | Medium        |

If exam says:
> “Minimize backup time” → Incremental  
> “Minimize restore time” → Full  
> “Balance restore speed and storage” → Differential
---

### Backup Storage Strategies
#### On-Site Backups
Stored locally.

Pros:
- Fast restore

Cons:
- Vulnerable to physical disaster

#### Off-Site Backups
Stored at separate location.

Pros:
- Survive site loss

Cons:
- Slower recovery

#### Cloud Backups
- Encrypted storage
- Scalable
- Geographic redundancy

Must still:
- Protect encryption keys
- Control access
- Test restores

---
### Backup Security (Extremely Important)
Backups themselves must be protected.
#### Encryption
Backups should be:
- Encrypted at rest
- Encrypted in transit

#### Key Management
If backup encryption keys are lost:  
Data is unrecoverable.

HSM / KMS may be used.
- **HSM:** A Hardware Security Module is a physical hardware device that provides secure storage and management of cryptographic keys. HSMs are used to protect sensitive data, such as encryption keys, by isolating them from the rest of the system and providing an additional layer of security.
- **KMS (Key Management Service):** A Key Management Service is a system that provides a centralized way of managing cryptographic keys. KMS can be used to generate, distribute, and manage encryption keys for backups, as well as other sensitive data.

#### Immutable Backups (Ransomware Defense)
Immutable = cannot be altered or deleted.

Critical against:
- Ransomware
- Insider deletion

Exam trigger:
> “Prevent ransomware from encrypting backups” → Immutable backups
---
### The 3-2-1 Rule (Very Testable)
Have:
- **3 copies** of data
- On **2 different media types**
- With **1 copy off-site**

This is a classic Security+ concept.

---
### Backup Frequency & RPO
Backup frequency determines:

Recovery Point Objective (RPO)

Example:
- Daily backups = up to 24h data loss
- Hourly backups = up to 1h data loss

Security+ often ties:  
Backup frequency ↔ acceptable data loss

---
### Backup Testing (Connect to Previous Topic)
Backups must be:
- Verified
- Tested
- Restored periodically

If backups exist but fail during restore:  
Recovery testing failure

---
### Snapshots vs Backups (Exam Trap)
Snapshots:
- Point-in-time copy
- Often same storage system
- Fast restore
- Not always isolated

Backups:
- Separate storage
- Long-term retention
- Better disaster protection

Snapshot ≠ full backup strategy.

---
### Backup & Ransomware Scenarios
Security+ frequently asks:
- Organization hit with ransomware
- Backups also encrypted
- What went wrong?

Correct answer:
- No offline/immutable backups
- Poor backup segmentation
- No access control

---
### Backup Types in Cloud
Cloud backups may include:
- Automated snapshots
- Cross-region replication
- Lifecycle policies

But still require:
- Encryption
- Access control
- Testing

---
### How Backups Connect to Everything We’ve Covered

| Topic                                                    | Connection                        |
| -------------------------------------------------------- | --------------------------------- |
| [[74-Data-Types-&-Classifications\|Data Classification]] | Determines retention requirements |
| [[75-States-Of-Data\|States of Data]]                    | Protects data at rest             |
| [[76-Protecting-Data\|Protecting Data]]                  | Backup encryption                 |
| [[77-Resiliency\|Resiliency]]                            | Enables recovery                  |
| [[78-Capacity-Planning\|Capacity Planning]]              | Backup storage growth             |
| RTO/RPO                                                  | Defines frequency                 |
| [[42-Other-Malware-Types\|Ransomware]]                   | Offline backups are critical      |
| [[55-Cloud-Infrastructure\|Cloud Security]]              | Replication & retention policies  |

Backups are the **final safety net** in cybersecurity architecture.