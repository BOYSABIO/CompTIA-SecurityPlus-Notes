# Deception & Disruption
Traditional defences like firewalls and antivirus are **reactive** - they stop or detect known attacks. `Deception` and `Disruption` are **proactive** - they try to **confuse, mislead, or slow down** attackers inside your environment.

"If they get in, make it costly, noisy, and easy to catch them."

These techniques help with:
- **Detection**: exposing intrusions early
- **Disruption**: stopping or delaying attacks
- **Intelligence**: learning how attackers operate

---

### Two Main Categories
| Category | Goal | Examples |
| --- | --- | --- |
| Deception | Trick the attacker into revealing themselves | Honeypots, Honeynets, Honeytokens, Decoy Systems |
| Disruption | Actively stop or delay the attack | Sinkholes, Tarpitting, Throttling, Sandboxing |

---

### Deception Technologies
#### Honeypots
- A decoy system designed to attract attackers
- It looks real (services, usernames, data) but it's **isolated** and **monitored**
- The goal is to observe attacker behaviour, collect intel, and trigger alerts when accessed

For example, if someone connects, it is a clear sign of malicious activity. Also, a honeypot doesn't protect data directly, it **detects and studies attacks**.

#### Honeynets
- A **network** of `Honeypots` connected together
- Simulates a realistic environment (multiple servers, traffic, vulnerabilities)
- Used for **advanced research** and **intrusion anlysis**

#### Honeytokens
- A **fake data element** placed inside real systems or databases
- Can be a bogus username, document, or API key
- If it's accessed or exfiltrated, it triggers an alert
- Can be database records, browser cookies, web page pixels, emails that you track

#### Honeyfiles
- A **fake file** placed inside real or honey net systems
- If the file is accessed or exfiltrated, it triggers an alert

For example, a fake `HR_Salaries.xlsx` file with embedded tracking metadata. If someone opens or uploads it externally, you immediately know there's a breach. `Honeytokens` are low-risk, low-cost, but highly effective **early-warning systems**.

#### Other Deceptive Techniques
- **Decoy Credentials**: fake admin logins in system files
- **Fake Network Shares or Directories**: appear valuable, but monitored
- **Canary Tokens**: trackable fake items that phone home when touched

---

### Disruptive Technologies
Now that the attacker has been lured or identified, these tools **slow, divert, or neutralize** their actions.

#### Sinkholes
- Redirect **malicious traffic** (like botnet C2 traffic or DDoS requests) to a **controlled destination** - a `black hole` or analysis server
- Used by ISPs, DNS providers, or enterprises to **disrupt malware communication**

For example, you hijack a known malware domain and redirect it to a sinkhole server that logs all traffic. `Sinkholes` **disrupt** an attack, while `Honeypots` **decieve** the attacker

#### Tarpits (Tarpitting)
- Intentionally **slow down attacker connections** by responding very slowly or keeping sessions open
- The idea is to consume attacker resources, delay scanning, or frustrate brute-force tools

For example, SMTP tarpitting slows down spammers by acknowledging each message painfully slowly

#### Sandboxing
- Running suspicious files or code in an **isolated, controled environment** to observe behaviour
- Commonly used by email filters, anivirus engines, and EDR systems
- **If a file behaves maliciously**, it's quarantined before reaching production systems

### Rate Limiting / Throttling
- Restricing how fast a user or system can make requests
- Helps **disrupt** brute force or DDoS attempts without full shutdowns

#### Other Disruptive Methods
- **Network Segmentation**: limits attacker movement
- **Automated Blocking or Blackholing**: Temporarily isolates infected endpoints
- **Trigger-based Responses**: SOAR systems can auto-quarantine or cut off compromised accounts

---

### How It All Fits Together
| Concept | Goal | Example | Category |
| --- | --- | --- | --- | 
| Honeypot | Lure attacker | Fake web server | Deception |
| Honeytoken | Trap data thief | Dake file with tracker | Deception | 
| Sinkhole | Redirect traffic | Capture botnet traffic | Disruption | 
| Tarpit | Delay attacker | Slow spam connections | Disruption |
| Sandbox | Contain malware | Observe code safely | Disruption | 

If the question is about *attracting and monitoring attackers* then `Honeypot`. If it is about *redirecting malicious traffic for analysis* then `Sinkhole`. And if it is about *running suspicious code in isolation* then `Sandboxing`.

---

### How It Ties Back to CIA & Controls
- **Detective Controls**: Honeypots, Honeyfiles, Sandboxing (reveal threats)
- **Preventive / Corrective Controls**: Sinkholes, Tarpitting, Segmentation (disrupt attacks)
- **Supports Integrity & Availability**: by keeping attackers contained and data safe