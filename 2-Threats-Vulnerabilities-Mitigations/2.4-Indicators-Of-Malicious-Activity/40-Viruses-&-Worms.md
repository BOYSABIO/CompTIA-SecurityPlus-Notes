# Viruses & Worms
This is the #1 point Security+ tests.

#### **Virus**
✔ Needs **user action** to spread  
✔ Must attach to a **host file**, program, or boot sector  
✔ Often hides inside:
- executables (.exe)
- documents (macros)
- scripts
- boot sector / MBR

> _A virus cannot self-replicate across systems without user involvement._

#### **Worm**
✔ **Self-replicating**  
✔ Uses network or OS vulnerabilities to spread automatically  
✔ Spreads without a file attachment  
✔ Often causes resource exhaustion (network or CPU)

> _A worm spreads itself across systems without user action._

**Exam Trigger:**  
If the scenario says “self-propagating” → the answer is always **worm**.

---
### How Viruses Work (Infection Steps)
Most viruses follow this pattern:
1. **Infection** → attaches to files
2. **Trigger** → runs when user opens the infected file
3. **Payload execution** → malicious activity
4. **Replication** → infects other files or drives
5. **Activation** → logic bomb sometimes included

Viruses require:
- someone to run an infected file
- someone to share a file (email, USB, file server)

---
### Types of Viruses (Exam Focus)

#### **File Virus**
Attaches to .exe or application files.

#### **Macro Virus**
Uses scripting languages like VBA in Word/Excel.

**Exam clue:**
> “Document attachment containing macro code.”

#### **Boot Sector Virus**
Infects the Master Boot Record.  
Runs before OS even loads.

#### **Multipartite Virus**
Infects multiple parts of a system (file + boot).

#### **Polymorphic Virus**
Changes its code on each infection to evade signatures.

#### **Metamorphic Virus**
Rewrites its own internal code structure.  
Harder than polymorphic.

#### **Stealth Virus**
Hides modifications to files and system calls.

---
### How Worms Work (Self-Propagation Steps)
A worm follows:
1. **Network scanning** (find vulnerable systems)
2. **Exploit** (use unpatched flaw or credential weakness)
3. **Replication** (copies itself across systems)
4. **Propagation** (keeps spreading without user action)
5. **Payload** (DDoS, backdoor, ransomware, botnet)

---
### Famous Worm Examples (Good for remembering patterns)

#### **Morris Worm (1988)**
One of the first internet worms — exploited:
- password guessing
- buffer overflow
- sendmail flaw

#### **ILOVEYOU (2000)**
Technically a worm, spread through email automatically.

#### **SQL Slammer (2003)**
Tiny worm (376 bytes).  
Spread across the world in **10 minutes**, caused massive outages.  
Used a buffer overflow in SQL Server.

#### **Conficker (2008)**
Massive worm infection, used multiple techniques.

#### **WannaCry (2017)**
Ransomworm — worm + ransomware.  
Used EternalBlue exploit to spread automatically.

---
### Real-world Impact Differences

| Malware        | Impact Style                                         |
| -------------- | ---------------------------------------------------- |
| **Virus**      | Slow, infects files locally, spreads via user        |
| **Worm**       | Fast, infects entire networks, spreads automatically |
| **Ransomworm** | Rapid encryption and destruction across network      |

Worms → usually cause **network congestion** or **horizontal propagation**.

---
### How Viruses & Worms Are Detected

#### **Viruses:**
- File scanning
- Signatures
- Checksums / integrity monitoring
- Behavioral detection (macro activity)

#### **Worms:**
- Network anomaly detection (port scanning behavior)
- IDS/IPS alerts
- Abnormal traffic patterns
- Rapid spread across subnets

---
### How to Prevent Viruses & Worms

#### Virus Mitigation
- Application whitelisting
- Disable macros
- AV/EDR
- User training
- Email filtering
- Patch management

#### Worm Mitigation
- Patch OS and applications
- Firewalls blocking unnecessary ports
- Network segmentation
- IDS/IPS
- Least privilege
- NAC (Network Access Control)

---
### How This Connects to Previous Topics

| Previous Topic                                                                                | Connection                                           |
| --------------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| **[[39-An-Overview-Of-Malware\|Malware overview]]**                                           | Worms/viruses are primary families                   |
| **[[38-Zero-day-Vulnerabilities\|Zero-day]]**                                                 | Worms often spread using zero-days (ex: EternalBlue) |
| **[[25-Memory-Injections\|Memory vulnerabilities]]**                                          | Worms frequently use buffer overflows                |
| **[[36-Misconfiguration-Vulnerabilities\|Misconfigurations]]**                                | Worms exploit open ports, weak settings              |
| **[[34-Cloud-specific-Vulnerabilities\|Cloud]]/[[37-Mobile-Device-Vulnerabilities\|mobile]]** | Modern worms target cloud APIs & mobile ecosystems   |
| **[[35-Supply-Chain-Vulnerabilities\|Supply chain]]**                                         | Viruses can infect installers or updates             |
