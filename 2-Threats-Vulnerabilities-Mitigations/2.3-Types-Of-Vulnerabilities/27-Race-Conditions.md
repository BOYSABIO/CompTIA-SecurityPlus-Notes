# Race Conditions
A **race condition** happens when a program’s **output or behavior depends on the timing or order of operations** in concurrent processes or threads — and an attacker can manipulate that timing to produce undesired results.

In simple terms:  
> Two or more processes “race” to use or modify the same resource — and whoever wins can change the outcome.

---
### **Core Concept**

A race condition is not about injecting code directly (like a buffer overflow), but rather about **logic flaws** that occur because **multiple operations happen without proper synchronization**.

If an attacker can influence that timing — they can **read**, **write**, or **replace** data between steps.

**[[02-The-CIA-Triad|CIA]] Link:** Primarily attacks **integrity** (data modified at wrong time) and sometimes **confidentiality** (unauthorized access).

---
### **Common Types**

|Type|Description|Example|
|---|---|---|
|**TOCTOU (Time-of-Check to Time-of-Use)**|The program checks a condition, then acts on it — but the condition changes in between.|App checks that a file is safe, then opens it — attacker replaces the file after the check.|
|**Resource Contention**|Two threads/processes access the same variable or resource concurrently without proper locks.|Two banking transactions update the same balance simultaneously, causing incorrect totals.|
|**Privilege Race**|Attackers exploit timing around privilege changes.|Gaining elevated privileges during a momentary admin context switch.|

_Exam keyword:_ “Time-of-check to time-of-use (TOCTOU)” = **Race condition vulnerability**.

---
### **Example Scenario**
A program:
1. Checks if a user has permission to open `/tmp/config`.
2. Confirms it’s safe.
3. Opens the file.

An attacker quickly **replaces the file** between step 2 and 3 with a **symlink** to `/etc/passwd` or a privileged file.

Result → The program reads/writes to the wrong file **with elevated privileges**.

**CompTIA loves this example** because it demonstrates **improper input validation** + **poor synchronization**.

---
### **Real-World Examples**

|Example|Description|
|---|---|
|**TOCTOU File Attack**|Swapping or linking files between permission check and open.|
|**Authentication Race**|Submitting multiple login requests during a password reset.|
|**Banking Transaction Race**|Triggering multiple withdrawals before the system updates balance.|
|**Privilege Escalation in OS**|Exploiting process scheduling around privilege checks (common in older UNIX/Linux).|

---
### **How It Relates to Other Topics**

| Related Topic                                                                                        | Connection                                                                                                         |
| ---------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| **[[26-Buffer-Overflows\|Buffer Overflows]]**                                                        | Both exploit poor code handling, but buffer overflow corrupts memory directly; race condition abuses logic timing. |
| **Integrity Controls**                                                                               | Race conditions break data integrity (wrong file, wrong data).                                                     |
| **[[09-Change-Management#Change Management\|Change Management]]**                                    | Both need proper sequencing of operations.                                                                         |
| **[[04-Authentication-Authorization-&-Accounting#Authorization - Granting Access\|Access Control]]** | Often tied to improper enforcement — system uses old access info.                                                  |

---
### **Mitigation Strategies**

| Level                    | Countermeasure                                                                           | Description                                 |
| ------------------------ | ---------------------------------------------------------------------------------------- | ------------------------------------------- |
| **Coding / Development** | Synchronize access to shared resources (locks, semaphores, atomic ops).                  | Prevent multiple writes at once.            |
| **System**               | Use temporary file permissions securely (`O_EXCL` flag, random names, safe directories). | Prevent file swap attacks.                  |
| **OS / Kernel**          | Patch privilege escalation bugs; enforce kernel-level locks.                             | Maintain process isolation.                 |
| **Operational / Policy** | Apply least privilege; separate duties.                                                  | Reduce impact if exploited.                 |
| **Testing**              | Fuzz and stress test for timing-based issues.                                            | Detect concurrency flaws before deployment. |

_CompTIA focus:_ Look for **“improper synchronization,” “TOCTOU,” “timing issue,” or “simultaneous access”** — all signal a **race condition**.

---
### **Detection & Prevention in Practice**
- **Static analysis** can catch unsynchronized shared variable access.
- **Fuzzing** or **stress testing** at high concurrency rates reveals timing bugs.
- **File integrity monitoring (FIM)** tools can detect unauthorized file changes between operations.
- **EDR** logs may show rapid sequential file access patterns.

---
### **Technical Example (Simple TOCTOU Attack)**

```bash
# Victim script 
if [ -w /tmp/userfile ]; then     
	echo "Authorized" > /tmp/userfile 
fi
```

Attacker runs:
```bash
ln -sf /etc/passwd /tmp/userfile
```

→ Between the check and write, `/tmp/userfile` points to `/etc/passwd`.

Result: overwrites `/etc/passwd` line with “Authorized” — **integrity compromise** and possible **privilege escalation**.

