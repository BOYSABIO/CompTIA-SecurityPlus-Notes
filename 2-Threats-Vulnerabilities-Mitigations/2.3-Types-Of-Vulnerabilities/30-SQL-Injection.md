# SQL Injection
**SQL Injection (SQLi)** is an attack where an attacker manipulates user input so that it becomes part of the SQL query executed by a backend database.

> In simple terms:  
> The application trusts user input → attacker turns that input into **SQL commands**.

SQLi targets:
- **[[02-The-CIA-Triad#Confidentiality|Confidentiality]]** → steal data
- **[[02-The-CIA-Triad#Integrity|Integrity]]** → modify/delete data
- **[[02-The-CIA-Triad#Availability|Availability]]** → drop tables or create infinite loops

It’s an **Input Validation + Application Logic Vulnerability**, _not_ a memory bug.

---
### **How It Works (under the hood)**
A vulnerable application does something like:

```SQL
SELECT * FROM users WHERE username = ' " + userInput + " ';
```

If the attacker enters:
```SQL
' OR '1'='1
```

The resulting SQL becomes:
```SQL
SELECT * FROM users WHERE username = '' OR '1'='1';
```

→ Always TRUE → attacker logs in without credentials.
This is why **parameterized queries** are mandatory.

---
### **Types of SQL Injection**

#### **Classic / In-Band SQLi**
Attacker uses the same channel to send payload and receive data.
- **Error-based SQLi**  
    Uses DB errors to reveal information.
- **Union-based SQLi**  
    Combines results using `UNION SELECT` to pull data from other tables.

#### **Blind SQL Injection**
No direct output — the attacker infers data through yes/no responses or timing.
- **Boolean-based blind SQLi**  
    Example:  
    `AND (SELECT 1 FROM users WHERE username='admin')=1`
- **Time-based blind SQLi**  
    Example:  
    `'; IF (SELECT COUNT(*) FROM users)>0 WAITFOR DELAY '0:0:5'--`

Timing tells the attacker “true or false.”

#### **Out-of-band SQLi**
Database sends data to a remote server (DNS lookup, HTTP request).  
Used when normal channels are blocked.

---
### **What SQL Injection Allows (practical capabilities)**
Depending on DB permissions, an attacker may:
- Dump entire databases
- Extract usernames/password hashes
- Modify table data
- Delete tables (`DROP TABLE`)
- Create new admin accounts
- Execute OS commands (if DB supports it, e.g., xp_cmdshell)
- Pivot deeper into the network

It’s extremely powerful.

---
### **Why It Happens**
Fundamentally:  
**User input is concatenated directly into SQL statements.**

Root causes:
- Lack of input validation
- Poor or no parameterization
- Missing or misconfigured ORM protections
- Debug code left open
- Over-permissioned database accounts

---
### **Mitigations (what CompTIA loves)**
#### **Parameterized Queries / Prepared Statements (BEST ANSWER)**
Ensures user input never becomes part of SQL code.

Example:
```SQL
SELECT * FROM users WHERE username = ?
```

#### **Stored Procedures**
Safer than inline queries, but not perfect if they concatenate input internally.

#### **Input Validation / Whitelisting**
Reject unexpected characters (`'`, `--`, `;`, etc.)

#### **Escaping / Sanitization**
Less ideal — can be bypassed — but still valid in some contexts.

#### **Least Privilege**
DB accounts can only do what’s necessary (read-only when possible).

#### **Web Application Firewalls (WAF)**
Can detect common SQLi patterns.

#### **ORM (Object-Relational Mapping)**
Some ORMs reduce SQLi risk by removing raw SQL calls.

---
### **SQL Injection vs Other Attacks (important distinctions)**

|Attack|Target|Mechanism|
|---|---|---|
|**SQL Injection**|Database|Tampering with SQL queries|
|**Command Injection**|Operating system|Injecting shell commands|
|**XSS**|Browser/user|Injecting JavaScript|
|**Buffer Overflow**|Memory|Overwrite memory with data|
|**Race Condition**|Logic/timing|Manipulate execution order|

CompTIA will try to confuse these — reading the scenario carefully matters.

---
### **How It Connects to Previous Topics**

#### **Integrity**
Attacker can modify, corrupt, or delete data.

#### **Confidentiality**
Attacker can dump database contents.

#### **Least Privilege**
Database service accounts should have limited rights to reduce impact.

#### **Input Validation**
Same root problem as some memory vulnerabilities — trusting untrusted input.

#### **[[28-Malicious Updates|Malicious updates]] & [[20-Common-Threat-Vectors#Supply Chain & Third-Party Threats|supply chain]]**
A poisoned web app update can reintroduce SQLi into your environment.

#### **[[27-Race-Conditions|Race conditions]]**
While different, SQLi and race conditions often appear together in exploit chains:
- SQLi for initial access
- Race condition exploit for privilege escalation

---
### **CompTIA Exam Triggers**
If you see these phrases, answer is almost always SQL injection:
- “Attacker enters `' OR '1'='1`…”
- “Malicious input alters database query…”
- “Backend returned unexpected data after crafted input…”
- “Prevented by parameterized queries…”
- “WAF detected UNION SELECT…”
- “Time delays used for information extraction…”

Watch for key words like:
- UNION
- SELECT
- DROP
- OR 1=1
- -- (comment)
- sleep / delay