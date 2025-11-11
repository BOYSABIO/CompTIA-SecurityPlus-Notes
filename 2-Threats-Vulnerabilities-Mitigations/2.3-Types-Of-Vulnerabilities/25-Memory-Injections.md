# Memory Injections
All software that you use runs in memory. Therefore malware also runs in memory. **Nothing** infects your computer unless it's loaded from disk, run inside memory and processed by your CPU.

**What it is (short):**  
Memory injection covers techniques an attacker uses to **place and execute code inside another process’s memory** (or otherwise manipulate memory) so they can run arbitrary code, escalate privileges, hide, or persist.

**Why it matters:**

- Breaks **[[02-The-CIA-Triad#Integrity|integrity]]** and often [[02-The-CIA-Triad#Confidentiality|confidentiality]] of the victim process.
    
- Used by malware, exploit kits, post-exploitation tools, and advanced attackers.
    
- Common follow-on step after delivery vectors like phishing, watering holes, or malicious downloads.

---
### Memory Running Process
1. DLLs (Dynamic Link Libraries) 
2. Threads
3. Buffers
4. Memory management functions
5. And much more

Malware is hidden somewhere and runs as it's own process, or injects itself into a legitimate process.

---
### Memory Injection Process
You start with a target process. This target process has a **starting address** and an **ending address**. If you wanted to inject malware, you would need to inject between the two addresses.
- This allows malware to avoid malware antimalware looking for just a malicious process alone
- Also allows malware to have same rights and permissions as the process it's injecting into

---
### Common Forms Of Malware
#### DLL Injection
- Dynamic linked library - executable on system that many processes and applications use
- The malware needs to start at some location stored on your computer

The attacker puts a path as to where the malicious DLL is located somewhere on the storage drive. This link or path is taken and put inside the target process. As the process executes, it reaches the point where it needs to reference the **DLL**, follows the link, pulls in the malicious DLL, and it is then loaded into memory so the malware is then run on the system. 

#### **Buffer overflow / stack smashing**
- Overwrite return addresses on the stack to redirect execution to attacker code (shellcode).
- Classic example used to gain code execution.
#### **Heap spraying**
- Fill heap memory with attack payloads to make code execution at predictable addresses easier (used in browser exploits).

#### **Return-Oriented Programming (ROP)**
- Instead of injecting new code, chain together small legitimate instruction sequences (“gadgets”) already in memory to perform actions — commonly used when executable memory is blocked.

#### **Code injection / shellcode injection**
- Write executable payload into process memory and jump to it (e.g., via exploited vulnerability).

#### **DLL injection / reflective DLL loading**
- Inject a DLL into another process (LoadLibrary, CreateRemoteThread, reflective loaders that avoid disk writes).
- Used to run code in the context of a trusted process.

#### **Process hollowing** (aka RunPE)
- Start a benign process in suspended state, replace its memory with malicious code, then resume — hides malicious code under a legitimate process name.

#### **APC (Asynchronous Procedure Call) / Thread injection**
- Queue a procedure to execute in a target thread context (Windows APC) — stealthy execution path.

#### **Use-after-free / memory corruption**
- Exploit dangling pointers to achieve code execution or information disclosure.

#### **Kernel-mode injection / driver manipulation**
- Inject at kernel level (rootkits), much more powerful and stealthy — high impact.

----
### Detection & Mitigation (practical controls)
**System / platform mitigations**
- **DEP / NX (Data Execution Prevention)** — prevent execution of writable pages.
- **ASLR (Address Space Layout Randomization)** — randomize addresses so injected code location is unpredictable.
- **Control-Flow Integrity (CFI) / Control Flow Guard (CFG)** — prevent jumps to unexpected code.
- **Stack canaries / stack cookies** — detect stack buffer overflows.
- **W^X / executable space protection** — memory pages are either writable or executable, not both.
- **Code signing & driver signing** — block unsigned kernel modules.
- **Hardware protections** — TPM, sandboxing, virtualization-based security (VBS).

**Development & deployment**
- **Safe coding**: bounds checking, use safe memory APIs, avoid unsafe functions.
- **Compiler protections**: ASLR-friendly builds, stack protector, fortify.
- **Fuzz testing & static analysis** in dev cycle.

**Operational / detection tools**
- **EDR / behavioral blockers** — detect process hollowing, unusual remote thread creation, injected modules.
- **HIPS / IPS rules** for injection indicators (CreateRemoteThread, WriteProcessMemory).
- **Memory forensics** (Volatility, Rekall) to analyze injected code, shellcode, or anomalous modules.
- **Monitoring**: anomalous parent/child process relationships, unexpected network connections from trusted processes.

**Policy & architecture**
- **[[06-Zero-Trust#Key Principles (Messer + NIST 800-207)|Least Privilege]]**: reduce impact if a process is compromised.
- **Application whitelisting**: prevent running unknown binaries.
- **Segmentation**: prevent lateral movement after injection.
- **Patching**: many memory attacks exploit unpatched vulnerabilities.

---
### How This Ties Back
- **[[20-Common-Threat-Vectors|Threat Vectors]]** Memory injection is commonly the _post-delivery_ action after phishing, watering holes, drive-by, or supply-chain compromise.
- **[[02-The-CIA-Triad|The CIA Triad]]** Mostly attacks **integrity** (altering process behavior) and **confidentiality** (stealing secrets); can impact availability (crashes).
- **Controls:** DEP/ASLR/CFG are **[[01-Security-Controls#Control Implementation Types (How they're applied)|technical]]** controls; training, patching, least privilege are **administrative** and **technical** together.
- **Incident response:** Memory analysis (RAM dumps), process artifact inspection, and EDR telemetry are key — ties to **[[04-Authentication-Authorization-&-Accounting#Accounting - Tracking Activity|accounting]]** (logs) and **[[03-Non-repudiation|non-repudiation]]** where possible.