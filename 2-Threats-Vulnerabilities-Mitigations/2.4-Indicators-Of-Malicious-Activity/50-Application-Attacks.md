# Application Attacks
Application attacks target **software**, not the OS or network.  
These exploit vulnerabilities in:
- Web applications
- APIs / microservices
- Business logic
- Input-handling
- Authentication flows
- Authorization checks
- Data validation
- Memory use

CompTIA broadly categorizes these attacks into:
1. **Input validation vulnerabilities**
2. **Logical/business logic attacks**
3. **Authentication/authorization attacks**
4. **Session/credential attacks**
5. **Memory/overflow exploitation**
6. **API-specific attacks**

Let’s hit each category with exam-focused clarity.

---
### Input Validation Attacks (Most Important Category)
These occur because the application **trusts user input**.
These include:

##### **1. [[30-SQL-Injection|SQL Injection]]**
Inject SQL commands into user input fields.

Exam trigger:
> “' OR 1=1 --”

#### **2. [[31-Cross-Site-Scripting|XSS (Cross-Site Scripting)]]**
Inject JavaScript into web pages.

Types:
- **Stored** (persistent)
- **Reflected** (nonpersistent)
- **DOM-based** (client-side)

#### **3. Command Injection**
User input triggers **OS commands**.

Example:
```bash
; rm -rf /
```

Exam trigger:
> “Input caused the server to execute system-level commands.”

#### **4. LDAP Injection**
Manipulates directory queries.

Example:
```
*)(uid=*))(|(uid=*
```

#### **5. XML Injection**
Attack XML parsers or modify XML data structures.

Often related to:
- SAML
- SOAP
- Config files

#### **6. XXE (XML External Entity Attack)**
The most important XML attack.

Attacker uses external entities to:
- read local files
- perform SSRF
- cause DoS

Exam trigger:
> “Application processed XML that referenced external resources.”

#### **7. Directory Traversal / Path Traversal**
Attacker accesses files outside the intended folder.

Example:
```bash
../../../etc/passwd
```

#### **8. Insecure Deserialization**
Attacker manipulates serialized objects to:
- trigger remote code execution
- escalate privileges
- tamper with objects

Exam trigger:
> “Modified serialized input triggered unexpected behavior.”

---
### Business Logic / Logic-Based Attacks
These exploit **the way the application is supposed to work**, not input parsing.

Examples:
- unlimited password reset attempts
- manipulating transaction sequence
- bypassing workflow steps
- negative quantities (refund fraud)
- skipping multi-factor steps

Exam trigger:
> “User manipulated app behavior without exploiting code vulnerabilities.”

---
### Authentication & Authorization Attacks
These target **identity and access control**.

#### **1. Credential Stuffing**
Attackers use lists of known username/password pairs.

Exam trigger:
> “Attack used breached credentials from another site.”

#### **2. Brute Force / Password Spraying**
- brute force = many passwords for one account
- spraying = one password across many accounts

#### **3. Broken Access Control**
User accesses functions they shouldn’t.

Examples:
- Insecure direct object reference (IDOR)
- Accessing another user’s account by changing `user_id`
- Bypassing admin-only endpoints

Exam trigger:
> “User accessed another user’s data by modifying URL.”

#### **4. Session Hijacking**
Attacker steals session ID (cookie) to impersonate a user.

#### **5. Session Fixation**
Attacker forces a user to use a specific session token, then logs in as them later.

#### **6. CSRF (Cross-Site Request Forgery)**
Attacker tricks a logged-in user into performing actions without their knowledge.

Example:
- victim clicks malicious link
- link causes their bank session to transfer money

Exam trigger:
> “Action performed using victim's authenticated session without their intent.”

---
### API-Specific Attacks
APIs are a huge part of modern apps and highly tested.

#### **1. Injection in APIs**
Same attacks as web forms:
- SQLi
- Command injection
- XSS (in API responses)

#### **2. Broken Object Level Authorization (BOLA)**
The biggest modern API vulnerability.

Example:
- API returns data for `user_id=1001`
- attacker changes it to `1002`
- gets someone else’s data

Exam trigger:
> “Attacker modified an ID in an API request and accessed another user’s information.”

#### **3. Rate Limiting Failures**
APIs that allow millions of requests without limit.

Leads to:
- brute force
- enumeration
- resource exhaustion

#### **4. Enumeration**
Predictable IDs, URLs, or API endpoints:

Example:
```
GET /api/user/1001 GET /api/user/1002 GET /api/user/1003
```

---
### Memory Vulnerabilities (Application-Level)
We studied these earlier, but they belong in this section too:
- **Buffer overflows**
- **Integer overflows**
- **Race conditions**
- **Use-after-free**

Exam trigger for memory corruption:
> “Application crashed after unexpected large input.”

---
### Code Injection & Remote Code Execution (RCE)
Some application attacks lead directly to RCE.

Examples:
- command injection
- deserialization flaws
- broken file upload handling
- vulnerable libraries

Exam trigger:
> “Attacker gained the ability to execute arbitrary code.”

RCE is extremely severe.

---
### File Upload Vulnerabilities
Web apps that allow file uploads can be tricked into accepting:
- PHP shells
- JavaScript payloads
- malicious executables
- overwritten system files

Exam trigger:
> “Uploaded file executed server-side code.”

---
### Exploiting Weak Cryptography in Applications
- weak hashing (MD5, SHA-1)
- insecure password storage
- predictable session IDs
- no salting
- plaintext passwords

These enable:
- credential theft
- session prediction
- forging authentication tokens

---
### How This Connects to Previous Topics

| Topic                                                                                                    | Relationship                                  |
| -------------------------------------------------------------------------------------------------------- | --------------------------------------------- |
| **[[49-Malicious-Code\|Malicious code]]**                                                                | Many app attacks inject malicious code        |
| **[[25-Memory-Injections\|Memory injections]]**                                                          | Part of RCE and buffer overflow exploitation  |
| **[[21-Phishing\|Phishing]]**                                                                            | Delivers malicious files exploiting app vulns |
| **Web attacks**                                                                                          | SQLi, XSS, CSRF = core web attack types       |
| **APIs & cloud**                                                                                         | BOLA and rate limiting issues                 |
| **[[04-Authentication-Authorization-&-Accounting#Authentication - Verifying Identity\|Authentication]]** | Credential stuffing, IDOR, session hijacking  |
| **[[15-Obfuscation\|Obfuscation]]**                                                                      | Attackers obfuscate injected scripts          |
| **[[38-Zero-day-Vulnerabilities\|Zero-day]]**                                                            | Often used to exploit application flaws       |

Application security ties MANY domains together.