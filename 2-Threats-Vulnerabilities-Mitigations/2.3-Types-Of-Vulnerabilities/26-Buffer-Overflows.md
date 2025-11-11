# Buffer Overflows
A **buffer overflow** happens when a program writes more data into a memory buffer (array) than it was allocated for, so the extra bytes overwrite adjacent memory. In other words, the extra data overflows into another area of memory.
If that adjacent memory contains control data (like a saved return address on the stack), an attacker can change program flow and execute arbitrary code.

**Plain language:** you feed a function more bytes than it expects and those bytes smash neighboring memory — sometimes including the address the program will return to.

---
### **Common types**
- **Stack-based buffer overflow** — overwrites stack data (saved EIP/return address, frame pointer, local vars). Often used to hijack control flow.
- **Heap-based buffer overflow** — corrupts heap metadata or adjacent heap-allocated data; commonly used to corrupt program state or craft arbitrary writes.
- **Off-by-one** — a small overflow (one byte) that can still corrupt control structures.
- **Integer overflow → buffer overflow** — wrong size calculations lead to undersized buffers.

---
### **Typical exploitation techniques**
- **Overwrite return address** on stack with address of injected shellcode → program jumps there (classic).
- **Return-Oriented Programming (ROP)**: when execution of injected code is blocked (DEP), chain together short instruction sequences (gadgets) from existing code to perform actions.
- **Heap exploitation**: corrupt heap metadata to get arbitrary write/execute.
- **Format-string + overflow combos**: use multiple primitives to read/write memory.

Tie back: these are **memory-injection** vectors — buffer overflows are often the initial primitive that allows code injection or ROP chains.

---
### **Why it’s dangerous**
- Full remote code execution (RCE) — attacker runs code as the vulnerable process.
- Privilege escalation if the process runs with elevated rights.
- Persistence, data exfiltration, lateral movement follow from successful RCE.

(CIA): primarily **[[02-The-CIA-Triad#Integrity|integrity]]** and **[[02-The-CIA-Triad#Confidentiality|confidentiality]]**; can also break **[[02-The-CIA-Triad#Availability|availability]]** (crash service).

---
### **Mitigations (practical & exam keywords)**
- **DEP / NX (Data Execution Prevention / No-eXecute)** — mark memory pages non-executable to stop executing injected code.
- **ASLR (Address Space Layout Randomization)** — randomize addresses of code/stack/heap to make gadgets/addresses unpredictable.
- **Stack canaries / stack cookies** — small value placed before return address; modified value indicates overwrite.
- **Safe languages / bounds-checked APIs** — use Java/.NET, or use safe C functions (or explicit bounds checks).
- **Compiler hardening**: stack protector, fortify, PIE (Position Independent Executables).
- **Code reviews, fuzz testing, static analysis** — find overflows before release.
- **Least privilege / sandboxing** — reduce impact if exploited.
- **W^X / DEP+ASLR combined** — makes exploitation much harder; ROP often used to bypass DEP, so combine defenses.

---
### **Detection & response**
- **EDR/HIPS**: watch for unusual memory modifications, suspicious child processes, or network connections from a normally benign process.
- **Crash analysis / core dumps**: look for overwritten return addresses or weird stack frames.
- **Fuzzing logs**: failures during testing can point to overflow vulnerabilities.
- **Memory forensics (Volatility)**: find injected code, abnormal modules, or suspicious thread contexts.

---
### **Exam-friendly comparisons / pitfalls**
- **Buffer overflow** ≠ format string — both are memory bugs but different primitives.
- **DEP** prevents executing injected shellcode; **ASLR** obscures gadget addresses. Both used together.
- **ROP** is the going-around-DEP technique (it reuses existing executable code).
- If question mentions overwriting a return address → think **stack-based buffer overflow**.
- If question mentions heap metadata or use-after-free → think **heap exploits**, not stack overflows.

---
### **Short example (conceptual)**
Vulnerable C:

```
char buf[64]; gets(buf); // no bounds checking — dangerous
```

Attacker supplies >64 bytes: excess data overwrites saved EIP; control flow hijacked.

Modern mitigations make `gets()` exploitation uncommon in well-built systems — that’s why safe APIs and compiler protections matter.

---
### **How this links to earlier topics**
- **[[25-Memory-Injections#Memory Injections|Memory Injections]]**: buffer overflows are a primary memory-injection method.
- **[[20-Common-Threat-Vectors#Common Threat Vectors|Threat Vectors]]**: often follow phishing/drive-by -> malicious file -> exploit.
- **Controls**: DEP/ASLR/stack canaries are _[[01-Security-Controls#Control Implementation Types (How they're applied)|technical controls]]_; training and secure development are _administrative_.