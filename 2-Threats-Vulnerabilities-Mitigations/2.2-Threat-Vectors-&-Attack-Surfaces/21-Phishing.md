# Phishing
**Phishing** is a **social engineering attack** that uses **deceptive** communication (usually email, but also test, calls, or messages) to trick people into revealing sensitive information or installing malware.

It's bait - and you're the fish

---
### Phishing = Social Engineering + Deception Channel
| Aspect             | Description                                                                                                |
| ------------------ | ---------------------------------------------------------------------------------------------------------- |
| Social Engineering | Exploits human trust, fear, urgency, or curiosity                                                          |
| Delivery Channel   | Usually **email** but can also be text, or voice [[20-Common-Threat-Vectors#Email and Social Engineering]] |
| Goal               | Steal credentials, deliver malware, or trick the victim into taking a specific action (click, open, pay)   |

---
### Common Types Of Phishing
| Type                     | Description                                                        | Example                                                             |
| ------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------- |
| Phishing (generic)       | Mass, untargeted messages sent to many users                       | "Your account will be deactivated - click here to verify"           |
| Spear Phishing           | Targeted attack aimed at a specific person or group                | Fake email to HR asking for payroll data                            |
| Whaling                  | High-value target (executive, CEO, CFO)                            | "CEO subpoena" or fake legal request email                          |
| Smishing (SMS Phishing)  | Attack via text message                                            | "Your package is delayed - click this link"                         |
| Vishing (Voice Phishing) | Attack via phone or voicemail                                      | Fake call from "tech support" asking for access                     |
| Angler Phishing          | Uses **social media** to impersonate companies or support accounts | Fake twitter "customer support" account replying to user complaints |
Look for clues in the question like "text message, CEO, Phone Call, Twitter"

---
### How Phishing Works (Lifecycle)
Phishing attacks follow a predictable pattern:
1. **Preparation** - Attacker registers a fake domain, creates email templates
2. **Delivery** - Phishing email or message sent to target
3. **Deception** - Message uses social cues (urgency, fear, authority, curiosity)
4. **Action** - Victim clicks link, opens attachment, or provides info
5. **Exploitation** - Attacker steals credentials or installs malware

---
### Phishing Characteristics (What To Look For)
Phishing emails usually have **red flags** you can spot:

| Indicator                 | Description                              |
| ------------------------- | ---------------------------------------- |
| Urgency or fear           | Immediate action required                |
| Spoofed sender            | `support@paypal1.com` (notice the 1)     |
| Suspicious links          | Hover shows mismatched or shortened URLs |
| Unexpected attachements   | Especially ZIPs, macros, or PDFs         |
| Generic greeting          | "Dear customer", "Dear user"             |
| Too good to be true       | "You've won a free gift card!"           |
| Spelling / Grammar issues | Often a tell for fake communications     |
Hover over links and check domains - phishing emails often use look-alike domains or subdomains

---
### Targets & Motivation
Attackers use phishing for various end goals:

| Goal             | Example                                      |
| ---------------- | -------------------------------------------- |
| Credential theft | Fake Microsoft 365 or banking login page     |
| Financial gain   | Wire fraud (Business email compromise)       |
| Malware delivery | Ransomware, keyloggers via attachments       |
| Espionage        | Collect sensitive corporate or personal data |
If a question mentions **wire transfer or fake invoices**, that's a ==Business Email Compromise== **(BEC)** a Phishing subtype

---

### Business Email Compromise (BEC)
- A **targeted phishing attack** where attackers impersonate executives or partners
- Goal: trick employees into sending payments, gift cards, or sensitive data
- Often combined with domain spoofing or look-alike email addresses

Email impersonating an executive requesting money -> Whaling / BEC

---
### Phishing Techniques

| Technique                     | Description                                                                    |
| ----------------------------- | ------------------------------------------------------------------------------ |
| Spoofing                      | Faking an identity (email address, caller ID, domain)                          |
| Clone Phishing                | Copying a legitimate message but replacing attachments / links                 |
| Typosquatting / URL Hijacking | Registering domains that look similar to legitimate ones (e.g., Micros0ft.com) |
| Credential Harvesting         | Fake login pages that collect usernames / passwords                            |
| Malicious Attachments         | Files that execute code or drop malware                                        |
| Link Manipulation             | Using shortened URLs or encoded links to disguise destinations                 |

---
### Phishing Prevention & Mitigation

| Control Type                                                                                                  | Examples                                                                                                     | Goal                                    |
| ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ | --------------------------------------- |
| [[01-Security-Controls#Control Type Table\|Technical Controls]]                                               | Spam filters, DNS filtering, link protection, email gateways                                                 | Block phishing messages before delivery |
| User Awareness                                                                                                | Security training, phishing simulations                                                                      | Educate employees to recognize attacks  |
| [[04-Authentication-Authorization-&-Accounting#Authentication - Verifying Identity\|Authentication Controls]] | [[16-Hashing-&-Digital-Signatures#What Is A Digital Signature?\|Digital Signatures]], DMARC/DKIM/SPF records | Validate legitimate senders             |
| Incident Response                                                                                             | Report suspicious emails, quarantine analysis                                                                | Detect and contain attempts             |
CompTIA loves to test these:
- User Training = Best prevention
- SPF, DKIM, DMARC = authenticates sender domain
- Report suspicious email = proper user response

---
### Email Authentication Technologies
| Protocol                                                                | Function                                                                                 |
| ----------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| SPF (Sender Policy Framework)                                           | Verifies mail server is authorized to send for domain                                    |
| DKIM (DomainKeys Identified Mail)                                       | Uses cryptographic signatures to verify sender's domain                                  |
| DMARC (Domain-based Message Authentication, Reporting, and Conformance) | Ties SPF & DKIM together and defines what to do if a message fails (reject / quarantine) |
Ensure email came from legitimate domain and hasn't been modified = DKIM
Prevent spoofing by validating authorized servers = SPF
Combine both and enforce policy = DMARC