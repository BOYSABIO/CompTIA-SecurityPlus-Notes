# Operating System Vulnerabilities
Operating systems (Windows, Linux, macOS, mobile OSs, network appliances) all contain **built-in attack surfaces**. These vulnerabilities arise when OS components, services, or drivers behave in insecure ways or expose interfaces that attackers can abuse.

This topic ties directly into:
- **Memory attacks** → [[26-Buffer-Overflows|buffer overflow]], [[25-Memory-Injections|memory injection]]
- **Logic flaws** → [[27-Race-Conditions|race conditions]]
- **Supply chain issues** → [[28-Malicious Updates|malicious updates]]
- **Privilege/access** → [[22-Impersonation|impersonation]], privilege escalation
- **[[01-Security-Controls#Control Types by Function|Control types]]** → hardening, patching, least privilege

---
### Categories of OS Vulnerabilities
#### **Memory Vulnerabilities**
These overlap heavily with what you just learned.
- **Buffer overflows (stack/heap)**
- **Use-after-free**
- **Race conditions (TOCTOU)**
- **Memory corruption**  
    Attackers exploit these to execute code, escalate privileges, or bypass security.

**Mitigations:** DEP, ASLR, CFI, stack canaries, compiler hardening.

#### **Privilege Escalation Vulnerabilities**
These weaknesses allow attackers to gain **higher privileges** than intended.

Types:
- **Vertical escalation:** User → Admin/Root
- **Horizontal escalation:** User A → User B
- **Kernel-level escalation:** Full system compromise

Examples:
- Misconfigured `sudo` rules
- Services running with excessive privileges
- Vulnerable drivers or kernel modules
- Impersonation tokens leaked (e.g., Windows Token Duplication attacks)

**Mitigation:** Least privilege, patching, secure kernel configuration, driver signing.

#### **Improper Access Control**
When OS fails to enforce correct permissions or boundaries.

Examples:
- World-readable sensitive files
- Incorrect NTFS or Linux ACLs
- Misconfigured SELinux/AppArmor profiles
- Weak file ownership
- Service accounts with unnecessary rights

Impact → breaks **[[02-The-CIA-Triad#Integrity|integrity]]** and **[[02-The-CIA-Triad#Confidentiality|confidentiality]]**.

#### **Insecure Default Configurations**
Out-of-the-box settings are frequently insecure.

Examples:
- Default passwords
- Unnecessary open ports/services
- Telnet or FTP enabled
- Anonymous shares
- Weak audit/log settings

**This is why OS hardening exists** — disabling, tightening, removing.

#### **Unpatched Software**
OSes constantly release patches for:
- Zero-days
- Privilege escalations
- Memory vulnerabilities
- Driver flaws
- Network stack bugs

Unpatched systems become part of:
- Ransomware outbreaks
- Worm propagation
- Remote code execution attacks
- Malicious update impersonation attempts

You’ve already seen how **supply chain + malicious updates** play into this.

#### **Driver & Kernel-Level Vulnerabilities**
Kernel = most privileged part of OS.  
Driver weaknesses can compromise kernel integrity.

Examples:
- Unsigned drivers
- Vulnerable third-party drivers (VERY common in Windows)
- Kernel-mode buffer overflows
- Race conditions in the kernel scheduler

Attackers love these because:
- They bypass AV/EDR
- They enable rootkits
- They disable defenses (tamper protection)

#### **Boot & Firmware Vulnerabilities**
These affect the system _before_ the OS loads.

Examples:
- Bootloader exploits
- UEFI/BIOS vulnerabilities
- Improper Secure Boot configurations
- Evil Maid attacks
- Modified kernel images

Impacts → full compromise of **integrity** and **[[11-Public-Key-Infrastructure#How The Trust Chain Works|trust chain]]**.

Mitigations: Secure Boot, TPM, measured boot.

#### **OS Service / Daemon Vulnerabilities**
OS includes background processes that may be exploitable.

Examples:
- SMB vulnerabilities (WannaCry → SMBv1)
- RDP exploits (BlueKeep)
- SSH misconfigurations
- RPC/DCOM vulnerabilities
- Print Spooler exploits (PrintNightmare)

**These are frequently used for lateral movement** inside networks.

#### **Authentication & Credential Vulnerabilities**
OS credential handling issues can be exploited.

Examples:
- Passwords stored in memory (LSASS leaks)
- Hash extraction (Mimikatz)
- Kerberos vulnerabilities (Golden/Silver tickets)
- Cached credentials
- Weak local admin passwords

Mitigations: Credential Guard, password vaults, LAPS, MFA.

#### **Logging & Auditing Weaknesses**
Not vulnerabilities directly — but lack of logging enables attackers to hide.

Examples:
- Disabled audit policies
- Incomplete logging
- Logs stored locally (can be wiped)
- Logs lacking integrity controls

Relates back to **AAA – [[04-Authentication-Authorization-&-Accounting#Accounting - Tracking Activity|Accounting]]**.

---
# How OS Vulnerabilities Are Exploited
Attackers typically exploit OS vulnerabilities through:
- **Local privilege escalation**
- **Remote code execution**
- **Kernel exploits**
- **DLL/Library injection**
- **Malicious drivers**
- **Process hollowing**
- **Memory manipulation**
- **Unauthorized file writes (TOCTOU)**

These step directly from previous topics like **memory injections, buffer overflows, race conditions**, and **malicious updates**.

---
# Mitigation Strategies (CompTIA-Focused)

|Mitigation|Description|
|---|---|
|**OS Hardening**|Disable unnecessary services, remove bloat, close ports|
|**Patch Management**|Regular OS, driver, and firmware patching|
|**Least Privilege**|Users and services get only what they need|
|**Application Whitelisting**|Only approved apps can run|
|**Code Signing / Driver Signing**|Ensures kernel integrity|
|**Memory Protection**|DEP, ASLR, stack canaries|
|**Secure Configurations**|Strong ACLs, secure boot, audit policies|
|**Sandboxing / Virtualization**|Containers, VM isolation|
|**Anti-malware + EDR**|Behavior monitoring, exploit prevention|
|**Network Segmentation**|Limits impact if OS is breached|

---
# CompTIA Exam Triggers
If you see these phrases, the answer is very likely “operating system vulnerability”:
- “Outdated OS version”
- “Driver vulnerability”
- “Privilege escalation from user to admin”
- “Unpatched kernel flaw”
- “Default configuration weakness”
- “Service running under admin/system privileges”
- “Access control permissions incorrectly set”
- “Race condition in system process”
- “Memory corruption in OS component”

They _love_ questions like:

> “Which of the following vulnerabilities would allow an attacker to escalate privileges through a kernel exploit?”

