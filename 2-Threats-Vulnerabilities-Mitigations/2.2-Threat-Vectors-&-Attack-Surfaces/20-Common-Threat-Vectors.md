# Common Threat Vectors
A **Threat Vector** (also called an **attack vector**) is the path or method that a threat actor uses to gain unauthorized access to a target.

*How the bad guys get in*

It's the *delivery channel* for cyberattacks 

---

### Threat Vector vs Threat Actor vs Vulnerability

| Term                 | Meaning                                   | Example                           |
| -------------------- | ----------------------------------------- | --------------------------------- |
| [[19-Threat-Actors]] | The person or group performing the attack | Hacker, insider, nation-state     |
| Vulnerability        | A weakness that can be exploited          | Unpatched systems, weak password  |
| Threat Vector        | The path or method used to exploit it     | Phishing email, malicious website |
A threat vector is **how**, not **who** or **what**.

---

### Common Threat Vectors
CompTIA break these into categories by how the attack *reaches* the system or user.

#### Email and Social Engineering
Still the #1 way attackers break organizations

| **Attack Type**                     | Description                                                           | Example                                |
| ----------------------------------- | --------------------------------------------------------------------- | -------------------------------------- |
| **Phishing**                        | Tricking users into revealing information or clicking malicious links | Fake "account suspension" emails       |
| **Spear Phishing**                  | Targeted phishing against specific people or roles                    | CFO receives fake invoice email        |
| **Whaling**                         | Phishing aimed at high-level executives                               | CEO targeted with fake legal notice    |
| **Business Email Compromise (BEC)** | Impersonating executives to request wire transfers or data            | **Urgent Payment** email from fake CEO |
| **Malicious Attachments / Links**   | Email carries infected files or URLs leading to drive-by downloads    | Attached PDF with embedded macro       |
If the vector involves **Human manipulation via email**, it's **social engineering vector**.

#### Web-Based Threats
Attacks that come through internet browsing or web services.

| Attack Type                | Description                                                   | Example                                      |
| -------------------------- | ------------------------------------------------------------- | -------------------------------------------- |
| Malicious Websites         | Host malware or fake login pages.                             | Phishing websites mimicking banks            |
| Drive-By Downloads         | Website exploits browser vulnerabilities automatically        | Visiting a page infects your system silently |
| Watering Hole Attacks      | Compromise websites often visited by a specific group         | Attackers infect an industry-specific portal |
| Malversting                | Malicious ads that deliver malware via legitimate ad networks | Ads on a news site trigger malware download  |
| Cross-Site Scripting (XSS) | Injecting code into trusted web apps to steal cookies/data    | Malicious comment field on a forum           |

#### Removable Media
Attackers use **physical storage devices** to deliver malicious software.

| Vector                             | Description                                                                         | Example                                       |
| ---------------------------------- | ----------------------------------------------------------------------------------- | --------------------------------------------- |
| USB / External Drives              | Malware spread via auto-run files or infected executables                           | "Free USB drive" dropped in the parking lot   |
| BadUSB Attacks                     | Reprogrammed USB device acts like a keyboard or network adapter to execute commands | USB injects PowerShell commands automatically |
| Removeable Media Data Exfiltration | Insider copies sensitive data onto removeable drivers                               | Unauthorized USB used by employee             |
*Dropped USB drive that infects systems*: ==Removeable media vector== + ==social engineering== 

#### Cloud-Based Threats
Cloud introduces new vectors due to **shared responsibility and connectivity**

| Vector                       | Description                                              | Example                                       |
| ---------------------------- | -------------------------------------------------------- | --------------------------------------------- |
| Misconfigured Cloud Services | Poorly set access controls expose data                   | Public S3 bucket leaks customer info          |
| Compromised API Keys         | Leaked credentials allow unauthorized cloud access       | Developer accidentally uploads keys to GitHub |
| Insecure Interfaces          | Poorly secured web APIs used for attacks                 | Attackers exploit open API endpoints          |
| Cloud Malware Injection      | Malware added to cloud-hosted applications or containers | Compromised Docker Image                      |
Clues like *publicly accessible storage* or *cloud misconfiguration* -> Cloud Threat

#### Mobile & Wireless Threats
Attacks targeting mobile devices, networks, and connectivity.

| Vector                           | Description                           | Example                                   |
| -------------------------------- | ------------------------------------- | ----------------------------------------- |
| Malicious Apps / Sideloading     | Apps from untrusted sources           | Fake Banking app installs malware         |
| SMS Phishing (Smishing)          | Phishing via text message             | *Your account locked* link text           |
| Voice Phishing (Vishing)         | Attacker tricks users via phone calls | Fake tech support call                    |
| Rogue Access Points / Evil Twins | Fake Wi-Fi mimics legitimate networks | *Free airport Wi-Fi* stealing credentials |
| Bluetooth Attacks                | Exploiting bluetooth vulnerabilities  | Bluejacking, Bluesnarfing                 |
If you see wireless or mobile + fake Wi-Fi -> Evil Twin or Rogue AP vector

#### [[19-Threat-Actors#Insider Threats|Insider Threats]]
Attacks that originate from *within* the organization.

| Type                | Description                           | Example                                         |
| ------------------- | ------------------------------------- | ----------------------------------------------- |
| Malicious Insider   | Employee intentionally causes harm    | Leaking data or sabotaging systems              |
| Negligent Insider   | Employee accidentally exposes data    | Clicking phishing link or misconfiguring access |
| Compromised Insider | Legitimate user's account is hijacked | Stolen credentials used by attacker             |
Legitimate access but misuses it = Insider Threat

#### Supply Chain & Third-Party Threats
Attackers exploit **trusted partners or software providers** to compromise targets indirectly.

| Vector                       | Description                                            | Example                                   |
| ---------------------------- | ------------------------------------------------------ | ----------------------------------------- |
| Software Supply Chain Attack | Compromising legitimate software updates or vendors    | SolarWinds breach                         |
| Third-Party Access Abuse     | Vendors or partners with excessive network permissions | HVAC vendor used to breach retail network |
| Hardware Supply Chain Attack | Tampering with hardware or firmware before delivery    | Pre-installed backdoor on network device  |
Trusted partner or software update leads to compromise

#### Network Based Threats
| Vector                   | Description                          | Example                          |
| ------------------------ | ------------------------------------ | -------------------------------- |
| Unsecured Protocols      | Data transmitted in cleartext        | Telnet, FTP, HTTP                |
| Man-in-the-Middle (MitM) | Intercepting and altering traffic    | ARP poisoning, session hijacking |
| DNS Poisoning / Spoofing | Redirects users to malicious sites   | Fake DNS responses               |
| Open Ports / Services    | Unnecessary network services exposed | Open RDP or SMB ports exploited  |

#### Emerging Vectors 
| Vector                   | Description                                  | Example                              |
| ------------------------ | -------------------------------------------- | ------------------------------------ |
| IoT (Internet of Things) | Weakly secured devices on networks           | Smart cameras with default passwords |
| AI-Powered Attacks       | Using AI for deepfakes or automated phishing | Synthetic voice mimicking CEO        |
| Deepfake Media           | Manipulated audio/video used for deception   | Fake video call for fraud            |
| Social Media Vectors     | Phishing or misinformation campaigns         | Impersonation accounts               |
