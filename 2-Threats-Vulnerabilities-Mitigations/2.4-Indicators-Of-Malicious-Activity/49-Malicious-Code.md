# Malicious Code
**Malicious code** refers to any code—script, binary, macro, payload, injected snippet—that performs unwanted or harmful actions on a system.

It is NOT just malware itself.  
It also includes:
- embedded payloads
- injected code
- scripts used by attackers
- malicious macros
- self-replicating routines
- persistent logic hidden inside applications

Security+ uses “malicious code” to describe **HOW** malware performs actions, not just the malware type.

---
### Malicious Code vs Malware (Critical Distinction)
**Malware** = the whole malicious application or program.  
**Malicious code** = the **parts of the malware** that actually perform harmful actions.

Example:
- A Trojan is the malware
- The keylogger inside it is malicious code
- The PowerShell payload it launches is malicious code

CompTIA loves this conceptual separation.

---
### Major Categories of Malicious Code (Security+ Focus)
Here are the specific types you need to know.

#### **1. Script-Based Malicious Code**
Attackers use scripts to automate exploitation or payload execution:
##### ✔ PowerShell
- Built-in Windows automation tool
- Frequently abused by fileless malware
- Can download, decode, and execute payloads in memory
- Runs with high privilege if not restricted

Exam trigger:
> “Attack used obfuscated PowerShell commands.”

##### ✔ Bash / Shell Scripts
Used in Linux or macOS environments to:
- download malware
- escalate privileges
- modify configs

##### ✔ Python, JavaScript, VBScript
Often used for:
- droppers
- C2 communication
- browser-based attacks

Exam trigger:
> “Malicious script executed through the browser.”

#### **2. Macro Malware**
Macros embedded in:
- Word
- Excel
- PowerPoint
- PDFs

Often:
- downloads additional payloads
- installs keyloggers
- steals documents

##### Exam triggers:
- “User enabled macros”
- “Document triggered malicious behavior”
- “Office macro downloaded additional code”

#### **3. Injection-Based Malicious Code**
##### ✔ Code Injection
Attacker inserts code into a legitimate process.

Examples:
- [[25-Memory-Injections#DLL Injection|DLL injection]]
- Process hollowing
- Shellcode injection
- Remote thread creation

Used for:
- stealth
- persistence
- evading AV
- running malware inside trusted processes (like explorer.exe)

##### ✔ [[26-Buffer-Overflows|Buffer Overflow]] Payloads
Overflow → EIP/RIP redirected → attacker’s code executes.

Malicious code embedded into:
- exploit payloads
- shellcode
- ROP chains

#### **4. Self-Modifying Malicious Code**
Very important for obfuscation.

##### ✔ Polymorphic Code
- Same functionality
- Different code on each infection
- Breaks signature-based detection

##### ✔ Metamorphic Code
- Fully rewrites itself
- Even harder to detect
- Behavior-based detection needed

Exam trigger:
> “Malware changes its own code every time it runs to avoid detection.”

#### **5. Logic Bombs**
Malicious code that triggers based on:
- date
- event
- system state
- user action

Often placed by insiders.

Exam trigger:
> “Code executed only after administrator account deletion.”

#### **6. Backdoor / Payload Code**
Malicious code used to:
- install backdoors
- open ports
- create persistence
- hook into authentication

Example:
- malware drops a DLL that starts on boot
- attacker inserts backdoor code into a service binary

#### **7. Droppers & Downloaders**
Not malware by themselves — they deliver malicious code.

##### ✔ Dropper
Installer _contains_ the malicious payload.

##### ✔ Downloader
Installer fetches payload from the internet.

Exam trigger:
> “Small program installed additional malware.”

#### **8. Fileless Malware Code**
Malicious code that never touches disk.

Uses:
- PowerShell
- WMI
- Registry run keys
- Reflective DLL injection

Exam trigger:
> “Malicious code executed entirely in memory.”

---
### How Malicious Code Gets Injected or Executed
These mechanisms matter for the exam:

##### ✔ Social Engineering
User executes malicious macro/script.

##### ✔ Exploits
Memory corruption = attacker injects shellcode.

##### ✔ Supply Chain
Software update includes malicious code.

##### ✔ Compromised websites
Drive-by malware that injects code via browser.

##### ✔ Insider threat
Employee inserts malicious code into production environment.

---
### Goals of Malicious Code
Malicious code can be designed to:
- modify system behavior
- steal data
- install ransomware
- exfiltrate files
- create persistence
- escalate privilege
- establish C2 channels
- weaken security controls
- masquerade as legitimate code

---
### Detecting Malicious Code
Security+ wants you to know these methods:

##### ✔ Signature-based
Works poorly vs polymorphic/metamorphic malware.

##### ✔ Heuristic/Behavioral
Detects suspicious actions (PowerShell execution, privilege escalation).

##### ✔ Integrity Checking
HMAC, hashing, tripwire-style comparisons.

##### ✔ Sandboxing
Executes code in isolated environment.

##### ✔ EDR/XDR
Modern behavioral monitoring.

---
### Preventing Malicious Code Execution

##### ✔ Application Control
Allowlisting only approved apps.

##### ✔ Script Control
Restrict PowerShell, macros, WSH.

##### ✔ Macro Security
Disable macros from untrusted documents.

##### ✔ Code signing
Ensures code authenticity.

##### ✔ Sandboxed browsers
Prevents browser-based injection.

##### ✔ Secure coding and input validation
Stops buffer overflow and injection entry points.

---
### How This Connects to Previous Topics

| Topic                                                           | Connection                                  |
| --------------------------------------------------------------- | ------------------------------------------- |
| **[[39-An-Overview-Of-Malware\|Malware types]]**                | Malicious code = payloads used by malware   |
| **[[25-Memory-Injections\|Memory injections]]**                 | Core mechanism for malicious code execution |
| **[[15-Obfuscation\|Obfuscation]]**                             | Polymorphic/metamorphic malicious code      |
| **[[24-Other-Social-Engineering-Attacks\|Social engineering]]** | Users trigger malicious macros/scripts      |
| **[[38-Zero-day-Vulnerabilities\|Zero-day]]**                   | Exploits deliver malicious code sections    |
| **[[35-Supply-Chain-Vulnerabilities\|Supply chain]]**           | Code is inserted into legitimate apps       |
| **[[16-Hashing-&-Digital-Signatures\|Hashes & integrity]]**     | Used to detect tampered or malicious code   |

Malicious code ties all your malware knowledge together.