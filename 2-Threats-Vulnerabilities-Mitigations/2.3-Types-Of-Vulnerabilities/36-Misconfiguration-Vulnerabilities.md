# Misconfiguration Vulnerabilities
A **misconfiguration vulnerability** happens when a system is set up incorrectly, leaving it insecure even though the underlying software is fine.

> It’s not a coding bug.  
> It’s a _human error_ or _improper default setting_ that creates exposure.

Examples span:
- Cloud
- Firewalls
- Servers
- OS
- Web apps
- Identity systems
- VPNs
- Containers / virtualization
- Databases

Misconfigurations are easy to create and hard to detect — which is why attackers love them.

---
### Major Categories of Misconfiguration (Security+ must-know)

#### **Default Credentials Left in Place**
- Admin/admin
- root/root
- default SNMP strings (public/private)
- factory passwords on IoT devices

**Exam clue:**

> “System deployed with default credentials.”

#### **Unnecessary Ports, Protocols, and Services**
Examples:
- Telnet enabled
- FTP instead of SFTP
- Open RDP (3389)
- SMBv1 enabled
- Unused web services running

This directly impacts **attack surface**.

**Exam clue:**
> “Unneeded services running on a server.”

#### **Cloud Misconfigurations**
(Your strongest area — we just covered it deeply)

Examples:
- Public S3 buckets
- Misconfigured IAM roles
- Wide-open Security Groups
- Anonymous access to blob storage
- Exposed cloud APIs

**Exam clue:**
> “Publicly accessible cloud storage.”

#### **Access Control Misconfiguration**
Failures in:
- ACLs
- File permissions
- Role-based access control
- Folder sharing
- Network segmentation

Example:  
A user can access a directory they shouldn’t → **[[04-Authentication-Authorization-&-Accounting#Authorization - Granting Access|Authorization]] flaw**.

**Exam clue:**
> “Overly permissive access rights.”

#### **Directory Services Misconfiguration**
- Incorrect AD permissions
- Disabled account lockout
- Weak password policy
- No MFA on privileged accounts
- Passwords stored in GPO scripts

#### **Firewall / Network Misconfigurations**
Examples:
- Any/Any rules
- Outbound filtering disabled
- Misconfigured NAT rules
- Allowing internal traffic to bypass firewall
- Layer 3 ACLs not applied properly

#### **Missing Security Controls**
- No encryption enabled
- Logging disabled
- No TLS on websites
- Missing patches
- No input validation
- No hardening applied

**Important:**  
Missing patches = misconfiguration (in Security+ terms), NOT “zero-day.”

#### **Application Misconfiguration**
Examples:
- Debug mode left on
- Directory listing enabled
- Verbose error messages reveal SQL queries
- Misconfigured session management

**Exam clue:**
> “Application reveals stack trace or db details to users.”

#### **Virtualization Misconfiguration**
You just learned these:
- Shared clipboard enabled
- VM promiscuous mode
- Unrestricted VM-to-VM communication
- Insecure snapshots
- Hypervisor management ports public

#### **Container Misconfiguration**
Examples:
- Running containers as root
- Exposed Docker APIs
- Insecure base images
- No resource limits
- No namespace isolation

#### **Database Misconfiguration**
- Listening on open network interfaces
- No authentication
- Weak or missing encryption
- Using root DB account for application

---
### Why Misconfigurations Are So Dangerous
Because they often:
- give attackers **easy access**
- bypass authentication
- expose secrets
- leave admin functions open
- expose sensitive data
- allow lateral movement
- provide footholds without needing an exploit

Most real-world breaches = misconfig + weak IAM.

---
### Tools to Detect Misconfiguration
Security+ loves these:
- **Vulnerability scanners**
- **Configuration compliance checkers** (CIS Benchmarks, SCAP, OpenSCAP)
- **File integrity monitors**
- **Cloud security posture management (CSPM)**
- **SIEM alerts**
- **Penetration testing**
- **[[09-Change-Management|Change management processes]]**
- **Automated IaC scanning (Terraform/Snyk/etc.)**

---
### How Misconfigurations Differ From Vulnerabilities Like SQLi/Buffer Overflows

|Category|Misconfiguration|Exploit (SQLi/Overflow)|
|---|---|---|
|Cause|Human error|buggy code|
|Characteristic|insecure settings|memory or code flaw|
|Prevention|hardening, proper config|secure coding, patching|
|Attack Surface|broad|narrow|
|Root Problem|insecure defaults|logic/memory issues|

---
# How This Ties Back to Previous Topics

| Topic                                                                               | Relationship                                        |
| ----------------------------------------------------------------------------------- | --------------------------------------------------- |
| **[[34-Cloud-specific-Vulnerabilities\|Cloud vulnerabilities]]**                    | Most cloud breaches = misconfigurations             |
| **[[35-Supply-Chain-Vulnerabilities\|Supply chain]]**                               | Misconfigured updater or repo = supply chain attack |
| **[[32-Hardware-Vulnerabilities\|Hardware vulnerabilities]]**                       | Debug ports (JTAG) open = misconfiguration          |
| **[[33-Virtualization-Vulnerabilities\|Virtualization]]**                           | VM promiscuous mode = misconfig                     |
| **[[27-Race-Conditions\|Race conditions]] / [[25-Memory-Injections\|memory bugs]]** | Different category (coding vs config)               |
| **Change management**                                                               | Prevents misconfigurations                          |
| **[[06-Zero-Trust\|Zero Trust]]**                                                   | Assumes misconfigs WILL exist                       |

Misconfiguration is **not a software bug** — it's a **deployment or configuration error**.