# The CIA Triad
These are the fundamentals of security (security objectives to maintain) and sometimes referred to as AIC.  
The **CIA Triad** represents the three core goals of information security:

| Letter | Principle | Goal | Simple Definition | 
| --- | --- | --- | --- | 
| C | Confidentiality | Privacy | Only authorized people can access information |
| I | Integrity | Accuracy | Data and systems are trustworthy and unaltered | 
| A | Availability | Access | Information and resources are accessible when needed | 

---

### Confidentiality 
Preventing unauthorized access to data. **WHO CAN SEE IT**.  

Examples:
- Encryption (data is unreadable without a key)
- Access control lists (ACLs) on files or networks (limit who has access to certain information)
- Multifactor authentication (MFA)
- Least privilege (users only get the access they need)
- Steganography (hiding data in images or files)
- Physical security (locked doors, badges)

Common Threats:
- Social engineering
- Eavesdropping/sniffing
- Data leaks or insider misuse

---

### Integrity
Ensuring data is accurate, consistent, and unaltered (either by accident or by a malicious actor). Data is stored and transferred as intended. **CAN I TRUST THIS**.

Examples:
- Hashing (MD5, SHA-256) to verify files
- Digital signatures (Mathematical scheme to verify integrity of data)
- Checksums / CRCs
- Version control systems
- Database constraints / input validation
- Certificates
- Non-repudiation (proof of integrity)

Common Threats:
- Unauthorized modification (malware, tampering)
- Human error or corrupted transfers
- Replay or man-in-the-middle attacks

---

### Availability
Keeping systems and data accessible and functional for authorized users. Ensuring access for users. **CAN I GET TO IT WHEN I NEED IT**.

Examples:
- Redundancy (RAID, failover systems) (Systems that can always be running)
- Backups
- Disaster recovery plans
- Load balancing
- DDoS protection
- UPS / power protection
- Patching (stability and closing security holes)

Common Threats:
- DDoS attacks
- Hardware failure
- Ransomware
- Natural disasters or power loss

---

### How They Work Together
These three principles balance each other - strengthening one can weaken another
| Example | Which Conflicts? | 
| --- | --- | 
| Encrypting all traffic improves **confidentiality** but may reduce **availability** (adds processing tools) | |
| Allowing open public access improves **availability** but reduces **confidentiality** | |
| Strict change control improves **integrity** but may slow down updates or **availability** | |

| Scenario | Violated Principle | 
| --- | --- | 
| A hacker steals customer records | Confidentiality | 
| A database is corrupted after a patch | Integrity | 
| A DDoS attack takes down your website | Availability | 
| A user modifies logs to hide activity | Integrity & Confidentiality |

---

## Related Notes
- [[01-Security-Controls]]
- [[03-Non-repudiation]]
- [[06-Zero-Trust]]
- [[76-Protecting-Data]]
