# Hardening Techniques
Hardening = **secure-by-default configuration + reducing unnecessary functionality**.
It answers 3 questions:
1. **What services don’t need to run? Disable them.**
2. **What access isn’t required? Remove it.**
3. **What configuration isn’t optimal? Fix it.**

This ties directly to:
- Segmentation
- Least privilege
- [[06-Zero-Trust|Zero Trust]]
- Vulnerability management
- [[53-Mitigation-Techniques|Mitigation techniques]]
- Secure baselines

Hardening affects _every_ layer: OS, applications, network hardware, identity, cloud platforms, virtual systems, containers.

---
### **Types of Hardening (What Security+ Cares About)**
##### **2.1 OS Hardening**
Making the operating system itself resilient.

Key actions:
- Remove bloatware/unneeded packages
- Disable unused services (FTP, Telnet, SMBv1, Guest account)
- Restrict ports with host-based firewalls
- Enforce strong password + lockout policies
- Enable BitLocker / FileVault (if required)
- Apply strict update policy → patch critical vulnerabilities
- Apply secure baselines (DISA STIGs, CIS Benchmarks)

**Exam trigger:**  
_"Which technique reduces the attack surface on a workstation?" → Disable unnecessary services."_

##### **2.2 Application Hardening**
Ensuring applications run with minimal exposure.

Actions:
- Remove default credentials
- Disable directory browsing and/or debug interfaces
- Enforce secure API keys / tokens
- Enable TLS/HTTPS
- Patch third-party libraries (e.g., Log4j type issues)
- Apply runtime protections like RASP
- Restrict plugins, macros, and extensions (browser hardening)

Exam notes:
- Browsers: disable Flash/Java, block unnecessary extensions.
- Office files: disable macros unless explicitly required.

##### **2.3 Network Hardening**
Securing routers, switches, firewalls, load balancers, WAPs.

Typical steps:
- Disable unused network ports (switch port security)
- Disable default admin credentials
- Disable insecure protocols: Telnet, TFTP, HTTP, SMBv1
- Implement management plane separation (OOB management)
- Use ACLs to restrict traffic flow
- Enable DHCP snooping, Dynamic ARP inspection, 802.1X
- VLAN separation / segmentation

Exam trigger:
- _"Disable unused switch ports" → port security / network hardening._
- _"Use SSH instead of Telnet" → secure protocol replacement._

##### **2.4 Server & Service Hardening**
Hardening individual server roles:

**Web Servers (IIS/Apache/Nginx):**
- Disable directory listing
- Enforce TLS
- Disable weak ciphers
- Apply secure headers (HSTS, CSP)

**Database Servers:**
- Remove default databases
- Restrict remote connections
- Enforce least privilege accounts
- Disable xp_cmdshell in SQL Server (classic exam point)

**Email Servers:**
- Enable SPF/DKIM/DMARC
- Disable open relays (classic exam trigger)

##### **2.5 Account & Credential Hardening**
Protecting identity, which attackers often target.

Techniques:
- MFA everywhere
- Disable stale/unused accounts
- Use password vaulting
- Enforce privilege separation (admins vs users)
- Implement account lockout policies
- Rotate credentials regularly
- Group Policy enforcement

This directly reinforces:
- Zero Trust
- [[04-Authentication-Authorization-&-Accounting|AAA]]
- IAM fundamentals

##### **2.6 Virtualization & Container Hardening**
Hypervisors and containers introduce new risks.

**Virtualization hardening:**
- Isolate VM networks
- Disable unnecessary hypervisor services
- Keep VM templates patched
- Limit VM escape attack surface
- Use secure snapshots

**Container hardening:**
- Run containers as non-root
- Use signed and trusted images
- Limit container capabilities
- Apply image scanning (SCA)
- Use orchestrator policies (Kubernetes RBAC, pod security)

Exam trigger:  
_"How do you prevent malicious images?" → Use image signing & scanning."_

##### **2.7 Cloud Hardening**
Cloud misconfigurations = one of the biggest Security+ themes.

Key cloud-hardening concepts:
- Secure S3 buckets / storage permissions
- Disable public access unless required
- Restrict IAM roles
- Enforce MFA for console access
- Log everything (CloudTrail, Azure Monitor)
- Use security groups + NSGs
- Rotate access keys
- Disable old API versions

Exam favorite:  
_"Misconfigured cloud storage causing data exposure." → Fix access policies / storage permissions._

##### **2.8 Mobile Device Hardening**
Through MDM/UEM solutions.

Controls:
- Enforce full device encryption
- Disable sideloading
- Enforce app allowlisting
- Disable untrusted network connections
- Require screen locks
- Remote wipe capability
- Containerization for BYOD

Exam trigger:  
_"Prevent users from installing unauthorized apps" → Implement MDM allowlisting."_

---
### **Configuration Baselines (Very Exam Relevant)**
Hardening is not “random tweaks.” It is **baseline-driven**.

Common baseline frameworks:
- **CIS Benchmarks** (very exam relevant)
- **DISA STIGs**
- **Vendor best practices** (Microsoft, Cisco)
- **NIST 800-53 / 800-171 derived controls**

Once a baseline is set:
- Systems are audited for drift
- Automated compliance tools detect deviations
- CI/CD pipelines enforce configuration templates

Exam phrase:  
_"Ensure consistent security posture across all systems." → Apply configuration baselines._

---
### **Patch Management Integration**
Hardening and patching are distinct but integrated.

Hardening removes unnecessary functionality.  
Patching removes vulnerabilities.

Together = minimal attack surface + minimal exploitable flaws.

Exam trigger:  
_"Which comes first?" → Hardening normally precedes patching, followed by continuous maintenance._

---
### **Relationship to Previous Topics (Memory Reinforcement)**
Hardening ties back to almost every topic we've covered:
- **[[53-Mitigation-Techniques|Mitigation Techniques:]]** hardening is a proactive mitigation strategy
- **[[52-Segmentation-&-Access-Control|Segmentation & Access Control:]]** disabling services & restricting ports reinforces segmentation
- **[[51-Indicators-Of-Compromise|Indicators of Compromise:]]** proper hardening reduces lateral movement pathways
- **[[50-Application-Attacks|Application Attacks:]]** many (SQLi, XSS) require insecure configurations to succeed
- **[[29-Operating-System-Vulnerabilities|OS Vulnerabilities:]]** hardening prevents exploitability
- **[[06-Zero-Trust|Zero Trust:]]** hardening enforces the "deny-by-default" mindset
- **[[43-Physical Attacks|Physical Security:]]** restrict ports, disable interfaces
- **[[11-Public-Key-Infrastructure|PKI & Encryption:]]** TLS, certificate hardening
- **[[08-Deception-&-Disruption|Deception/Disruption:]]** hardened endpoints limit attacker footholds

Hardening is essentially the practical glue that binds all previous security principles.