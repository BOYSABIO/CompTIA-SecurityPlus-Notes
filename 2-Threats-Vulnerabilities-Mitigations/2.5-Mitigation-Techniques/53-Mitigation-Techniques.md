# Mitigation Techniques
Mitigation techniques = **defensive strategies used to prevent or reduce the impact of threats, vulnerabilities, and attacks.**

Think of this topic as:  
**“What do we DO to stop the threats we’ve studied?”**

This includes:
- network defense
- host defense
- application defense
- privilege controls
- secure configurations
- monitoring
- containment
- hardening

Let’s break it down by category the way CompTIA expects you to know it.

---
### Network Mitigation Techniques
These prevent, detect, or contain network-based attacks.
#### **1. Firewalls**
Controls traffic based on:
- IP
- port
- protocol
- direction
- application (NGFW)
- identity (user groups)

Key features:
- packet filtering
- stateful inspection
- application-aware filtering
- implicit deny

Exam triggers:
- “Traffic blocked due to rule order”
- “Only HTTPS allowed out of segment”

#### **2. IDS/IPS**
Detect or block attacks.
- **IDS** = alerts only
- **IPS** = blocks in real time

Detects:
- port scans
- DoS/DDoS
- signatures of malware
- anomalies

#### **3. Network Segmentation**
Breaks network into smaller, isolated partitions:
- VLANs
- DMZ
- microsegmentation
- subnetting

Stops:
- lateral movement
- ARP poisoning spread
- malware propagation

#### **4. Zero Trust Network Access**
Core principles:
- never trust
- continuous authentication
- micro-permissions
- per-app access

#### **5. NAC (Network Access Control)**
Verifies device posture before allowing connection:
- OS version
- patches
- antivirus
- configuration compliance

Stops:
- rogue devices
- BYOD threats

#### **6. VPNs / Encrypted Tunnels**
Protect data in transit.

Mitigates:
- MITM attacks
- packet sniffing
- replay attacks

#### **7. Anti-DDoS / Traffic Filtering**
- rate limiting
- geoblocking
- blackhole routing
- upstream filtering
- CDNs

Exam trigger:
> “Traffic blocked due to volumetric overload.”

---
### Host & Endpoint Mitigation Techniques
These protect individual devices.

#### **1. Endpoint Detection & Response (EDR)**
Detects malicious behavior like:
- PowerShell abuse
- code injection
- privilege escalation
- persistence mechanisms

Modern replacement for signature-only AV.

#### **2. Antivirus / Anti-malware**
Signature + heuristic detection.

Mitigates:
- trojans
- ransomware
- spyware
- worms

#### **3. Application Allowlisting / Blocklisting**
Allowlisting → only approved programs run  
Blocklisting → known malicious programs are blocked

Allowlisting is more secure.

#### **4. Patch Management**
Fixes vulnerabilities before exploitation.

Mitigates:
- zero-day exposure (if patched quickly)
- missing patches
- OS and application vulnerabilities

#### **5. Secure Configuration Baselines**
Used for:
- servers
- workstations
- cloud instances
- network devices

Includes:
- disabling unused services
- secure defaults
- password policies
- logging configuration

#### **6. Memory Protection**
- DEP (Data Execution Prevention)
- ASLR (Address Space Layout Randomization)
- stack canaries
- code signing

Mitigates:
- buffer overflows
- memory corruption
- ROP-based attacks

#### **7. Host-Based Firewalls**
Protect individual systems from:
- lateral movement
- scanning
- local exploitation

---
### Application-Level Mitigation Techniques
These defend apps against code injection and logic attacks.

#### **1. Input Validation**
Critical defense against:
- SQL injection
- command injection
- XSS
- LDAP injection
- XXE
- directory traversal

Rules:
- validate _server-side_
- sanitize all user input
- allowlists are better than denylists

#### **2. Authentication Hardening**
- MFA (multi-factor authentication)
- secure password storage (salt + hash)
- token expiration
- rate limiting

Protects against:
- credential stuffing
- brute force
- session hijacking

#### **3. Authorization Controls**
- RBAC
- ABAC
- least privilege
- strict access control for APIs

Stops:
- broken access control (IDOR)
- privilege escalation

#### **4. Secure Coding Practices**
- input sanitization
- error handling
- remove debugging data
- secure file uploads
- parameterized queries
- escaping output

#### **5. Code Review & Static Analysis**
Tools detect:
- insecure functions
- logic flaws
- hardcoded keys
- injection points

#### **6. WAF (Web Application Firewall)**
Blocks:
- XSS
- SQL injection
- command injection
- API abuse

---
### Identity & Access Management Mitigation Techniques

#### **1. Principle of Least Privilege**
Minimize each user’s access.

Mitigates:
- insider threats
- unauthorized access
- malware escalation

#### **2. Privilege Auditing & Review**
Regularly review rights:
- remove stale access
- eliminate privilege creep

#### **3. MFA (Multi-factor Authentication)**
Adds strong resistance to:
- credential theft
- password spraying
- MITM attacks

#### **4. Password Policies**
- complexity
- expiration (role-based)
- lockout thresholds
- uniqueness

#### **5. Account Lockout / Rate Limiting**
Stops brute-force and credential stuffing.

---
### Cloud & Virtualization Mitigation Techniques

#### **1. Cloud Security Groups**
Network ACLs for cloud environments.

Mitigate:
- SSH/RDP exposure
- misconfigured open ports

#### **2. Hypervisor Hardening**
Stops:
- VM escape
- snapshot tampering

Includes:
- patching hypervisor
- restricting VM management interfaces

#### **3. API Security**
Protect against:
- BOLA
- enumeration
- injection

Includes:
- rate limiting
- authentication
- authorization checks

#### **4. Cloud Monitoring / SIEM**
Detect:
- anomalous API calls
- resource abuse
- privilege escalation
- unapproved cloud instances

---
### Data Protection Mitigation Techniques

#### **1. Encryption**
- at rest (FDE, database encryption)
- in transit (TLS)

#### **2. DLP (Data Loss Prevention)**
Prevents:
- copying sensitive files
- exfiltration by email or USB
- cloud data leakage

#### **3. Tokenization & Masking**
Used for compliance (PCI, GDPR).

#### **4. Backups & Snapshots**
Mitigate:
- ransomware
- accidental deletion
- system corruption

---
### Physical Mitigation Techniques
- locks
- mantraps
- intrusion detection
- cameras
- facility segmentation
- RFID shielding
- visitor logs

Stops:
- tailgating
- hardware implants
- rogue access points

---
### Incident Response & Containment Techniques
Mitigation also includes **responding** to threats.

Steps:
1. **Detection** (SIEM/EDR alerts)
2. **Analysis**
3. **Containment** (isolate host or segment)
4. **Eradication**
5. **Recovery**
6. **Lessons learned**

Containment methods:
- isolate affected VLAN
- disable network port
- block malicious IP
- quarantine host

---
# How This Connects to Previous Topics

| Topic                                                               | Connection                                                             |
| ------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| **[[39-An-Overview-Of-Malware\|Malware]]**                          | EDR, AV, application control, network controls mitigate malware spread |
| **[[50-Application-Attacks\|Application attacks]]**                 | Input validation, WAF, secure coding are direct defenses               |
| **[[45-DNS-Attacks\|DNS attacks]]**                                 | DNSSEC, sinkholing, segmentation help                                  |
| **[[46-Wireless-Attacks\|Wireless attacks]]**                       | 802.1X, WPA3, PMF mitigate them                                        |
| **[[47-On-path-Attacks\|On-path]] & [[48-Replay-Attacks\|replay]]** | TLS, encryption, nonces, mutual auth                                   |
| **[[06-Zero-Trust\|Zero Trust]]**                                   | Microsegmentation + identity-first access control                      |
| **[[51-Indicators-Of-Compromise\|IoCs]]**                           | IoCs trigger mitigation and response workflows                         |

This topic basically summarizes all the defensive strategies you’ve been learning.