# Indicators Of Compromise
**Indicators of Compromise** = observable evidence that suggests a system, network, or account has been compromised.

IoCs are:
- forensic clues
- log entries
- file changes
- behavioral anomalies
- unexpected communications
- security alert patterns

They DO NOT tell you the full story by themselves.  
They signal: **“Something is wrong — investigate further.”**

---
### Categories of IoCs (Security+ Focus)
IoCs fall into multiple domains:
1. **Network Indicators**
2. **Host/Endpoint Indicators**
3. **Security Control Indicators**
4. **User/Account Indicators**
5. **File/System Indicators**
6. **Application Indicators**

Let’s break these down the way the exam expects you to understand them.

---
### Network Indicators
These come from:
- firewalls
- routers
- IDS/IPS
- packet captures
- SIEM logs

Examples:
##### ✔ Unusual Outbound Traffic
If a workstation suddenly sends:
- encrypted data to unknown IPs
- traffic to foreign countries
- traffic at odd hours

→ possible C2 (command-and-control).

##### ✔ C2 Traffic Patterns
- Repeated beaconing
- DNS tunneling
- HTTP requests to weird domains
- Traffic in predictable timed intervals

##### ✔ DNS Indicators
- DNS requests for random subdomains
- DNS tunneling patterns (long, encoded-looking strings)
- Queries to known malicious domains

##### ✔ Anomalous Port Activity
- SSH on port 2222
- RDP on port 3389 from the internet
- SMB across subnets

Exam trigger:
> “Outbound traffic to unknown external IPs every 60 seconds.”

---
### Host / Endpoint Indicators
These are found through:
- EDR
- OS logs
- Sysmon
- Security agents

Examples:
##### ✔ Unexpected Processes
- Powershell running encoded commands
- cmd.exe launched by Word
- unknown executables in temp folders

##### ✔ High CPU, GPU, or Memory Spikes
This often points to:
- Cryptominers
- Malware loops
- DDoS bots

##### ✔ Unauthorized Changes
- New user accounts
- Modified registry keys
- New scheduled tasks
- Changed system binaries

##### ✔ File Integrity Changes
Detects rootkits or tampering.

Exam trigger:
> “Critical OS files changed from baseline hash.”

---
### File & Malware Indicators
##### ✔ Suspicious File Hashes
- MD5/SHA-256 hashes matching known malware
- Files that change hashes unexpectedly

##### ✔ Unexpected File Names / Extensions
- `.exe` masquerading as `.pdf`
- Double extensions: `invoice.pdf.exe`
- Files with random names

##### ✔ Droppers and Payloads
A tiny file that immediately makes outbound connections to download more malware.

---
### Account/User Indicators
##### ✔ Impossible Travel
User logs in from:
- Germany → 2 minutes later from New York  
    This is impossible based on human limitations.

##### ✔ Login Pattern Anomalies
- Login at unusual hours
- Multiple failed attempts
- Successful login from new country

##### ✔ Privilege Escalation
- Standard user suddenly running privileged commands
- Account added to the Domain Admins group

##### ✔ Authentication Failures
Often a sign of credential stuffing.

Exam trigger:
> “User account logged in successfully after thousands of failed attempts.”

---
### Log Indicators
Exam wants you to understand what logs show.

##### ✔ Security Log Anomalies
- Large amounts of failed logins
- Sudden log clear events
- Unauthorized access to sensitive folders

##### ✔ Application Log Indicators
- Unexpected application crashes
- Errors referencing DLL injection
- Unexpected plugin/module loads

##### ✔ System Events
- New services installed
- Services stopping unexpectedly
- Kernel messages indicating memory corruption

---
### Email Indicators (Phishing Evidence)
- Unexpected attachments
- Spoofed sender address
- Incorrect domains
- Mismatched links

Exam trigger:
> “Email domain uses homoglyph characters.”

---
### Web/Browser Indicators
- Browser opens on its own
- Redirects to malicious sites
- Unknown extensions installed
- Self-signed or suspicious certificates
- HSTS bypasses

---
### SIEM Correlation IoCs
SIEMs correlate multiple events into one indicator.

Examples:
- Multiple hosts beaconing to same malicious IP
- Lateral movement patterns
- Privilege escalation → file access → outbound transfer
- Host connecting to TOR network

Exam trigger:
> “SIEM shows correlated events across multiple systems pointing to a coordinated attack.”

---
### Behavioral Indicators (Very Modern Security+ Content)
Behavioral IoCs detect **patterns**, not specific signatures.

Examples:
- User performs actions they never normally do
- Host performs actions way outside baseline
- Application uses more resources than usual
- Repetitive timed beacon patterns
- Malware-like command sequences

This is what EDR systems specialize in.

---
### Cloud IoCs
Security+ now expects you to know cloud-specific signs.

Examples:
- Unexpected IAM role changes
- API calls from unusual regions
- Cloud resources spun up unexpectedly
- Outbound traffic from cloud that shouldn’t exist
- S3 bucket access from unknown identities

---
### Important Exam Distinctions

##### **IoCs ≠ incidents**
IoC is _evidence_, not proof.

##### **IoCs ≠ attack type**
IoCs suggest an attack but don’t define the attack itself.

##### **IoCs need correlation**
A single IoC is rarely enough — SIEM correlation is key.

##### **Not all anomalies are IoCs**
Some anomalies are benign, but suspicious.

---
# How This Connects to Previous Topics

| Topic                                         | Connection                                                      |
| --------------------------------------------- | --------------------------------------------------------------- |
| **[[39-An-Overview-Of-Malware\|Malware]]**    | IoCs show malware behavior (hashes, processes, network traffic) |
| **App attacks**                               | Logs show SQLi, XSS, CSRF attempts                              |
| **[[45-DNS-Attacks\|DNS attacks]]**           | DNS tunneling & poisoning leave IoCs                            |
| **[[48-Replay-Attacks\|Replay]] & MITM**      | Unusual ARP/DNS patterns = IoCs                                 |
| **[[46-Wireless-Attacks\|Wireless attacks]]** | Repeated deauth frames = IoCs                                   |
| **[[43-Physical Attacks\|Physical attacks]]** | Unexpected logins from badge/NFC replay                         |
| **SIEM/SOC**                                  | IoCs are used to trigger alerts                                 |
| **[[06-Zero-Trust\|Zero trust]]**             | IoCs feed into adaptive security posture                        |
