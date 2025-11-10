# Impersonation
**Impersonation** is a **social engineering technique** where an attacker pretends to be someone trusted or with authority to gain access, information, or assistance.

The attacker puts on a mask - not to hide, but to be believed

---
### The Goal
The attacker isn't using technical exploits - they're exploiting human trust and procedures.

| Objective                | Example                                                    |
| ------------------------ | ---------------------------------------------------------- |
| Gain **Physical Access** | Pretending to be IT support or delivery staff              |
| Gain **Logical Access**  | Calling helpdesk to reset a password                       |
| Gain **Information**     | Pretending to be a new employee asking for network details |
Impersonation is about **psychological manipulation**, not technical hacking.

---
### Common Impersonation Scenarios

| Scenario                       | Description                                                          | Example                                                         |
| ------------------------------ | -------------------------------------------------------------------- | --------------------------------------------------------------- |
| In-person impersionation       | Attacker physically enters facility pretending to belong             | Hi, I'm from the fire inspection team, need to check the alarms |
| Phone-based impersonation      | Attacker calls pretending to be an employee, tech support, or vendor | This is IT - can you verify your login credentials for testing  |
| Online impersonation           | Attacker pretends to be a coworker or partner via email or chat      | Fake Teams or Slack message asking for access                   |
| Vendor / Service impersonation | Pretending to be external service provider or delivery driver        | Fake badge or uniform to bypass security                        |

---
### Impersonation vs [[21-Phishing|Phishing]]
| Aspect  | Impersonation                                      | Phishing                                  |
| ------- | -------------------------------------------------- | ----------------------------------------- |
| Method  | Person-to-person deception (physical, phone, live) | Message or email deception                |
| Medium  | Direct interaction                                 | Digital communication                     |
| Example | Pretending to be IT staff on a call                | Fake password reset email                 |
| Goal    | Gain trust, access, or info                        | Get click, credential, or install malware |
Phishing = written trap
Impersonation = in-person or real-time deception

---
### Techniques Used In Impersonation
| Technique           | Description                               | Example                                                  |
| ------------------- | ----------------------------------------- | -------------------------------------------------------- |
| Pretexting          | Creating a believable backstory or reason | I'm here to audit your security logs; management sent me |
| Authority           | Acting as someone in charge or official   | I'm from corporate IT                                    |
| Urgency             | Pressuring or immediate action            | This is an emergency                                     |
| Familiarity / Trust | Acting friendly, name-dropping coworkers  | Oh yeah, I worked with karen in accounting               |
| Technical Jargon    | Using insider language to sound credible  | Your VLAN 10 connection needs reconfiguration            |
| Uniforms / Badges   | Physical props to appear legitimate       | Wearing a delivery vest or fake ID                       |
Impersonation attacks don't break systems - they break procedures

---
### Targets Of Impersonation Attacks
Attackers usually target **human facing roles** that have access or trust privileges:

| Target                        | Reason                                     |
| ----------------------------- | ------------------------------------------ |
| Receptionists / Front desk IT | Control access, usually helpful and polite |
| Helpdesk / IT support         | Can reset passwords or grant access        |
| Maintenance / Security Staff  | Have physical keys or control panels       |
| Finance / HR staff            | Handle sensitive data or payments          |

---
### Impersonation + Pretexting
These two often appear together:
- **Pretexting** is the story or reason
- **Impersonation** is the role the attacker plays

*Hi, I'm the new systems auditor (impersonation). The boss said you'd give me access to the admin console (pretext)*

---
### Mitigation Strategies
| Control Type                                                                                      | Example                                                      | Goal                            |
| ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------- |
| [[01-Security-Controls#Control Implementation Types (How they're applied)\|Procedural]]           | Always verify identity through callback or company directory | Prevent blind trust             |
| [[01-Security-Controls#Control Implementation Types (How they're applied)\|Physical]]             | Security badges, mantraps, sign-in policies                  | Prevent unauthorized entry      |
| [[01-Security-Controls#Control Implementation Types (How they're applied)\|Technical]]            | Multi-factor authentication (MFA), least privilege access.   | Reduce impact of social success |
| [[01-Security-Controls#Control Implementation Types (How they're applied)\|Training & Awareness]] | Teach employees to challenge unknown individuals or requests | Build vigilance                 |
CompTIA likes:
- Verify identity before providing access
- Train employees to recognize social engineering
- Use MFA to prevent password-based impersonation

