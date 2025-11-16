# Zero-day Vulnerabilities
A **zero-day vulnerability** is a software, hardware, or firmware flaw that:
1. **Is not known to the vendor**,
2. **Has no patch available**, and
3. **Can be exploited immediately** if discovered by attackers.

> “Zero-day” refers to the fact that the vendor has had **zero days to fix it**.

This makes zero-days extremely dangerous because **defenders cannot patch something they don’t know exists**.

---
### Zero-Day vs. Zero-Day Exploit
Important distinction:
- **Zero-day vulnerability** → the flaw itself
- **Zero-day exploit** → the weaponized attack code that uses the flaw

CompTIA will sometimes try to trick you by mixing these.

Example exam clues:
- “Previously unknown vulnerability” → zero-day vulnerability
- “Attack used before patches existed” → zero-day exploit

---
### Why Zero-Days Are Dangerous
Because they bypass:
- antivirus signatures
- IPS/IDS rules
- patch management cycles
- known vulnerability scanners
- traditional hardening guides
- vendor-provided fixes

Zero-days are especially valuable to:
- nation-state APT groups
- cybercriminal ransomware groups
- penetration testers / red teams
- spyware vendors (Pegasus, Predator)

---
### Common Types of Zero-Day Vulnerabilities
A zero-day can exist anywhere:
#### **OS Kernel Zero-Days**
- Privilege escalation
- Sandbox escapes
- System-call race conditions
- Memory corruption flaws

#### **Application Zero-Days**
- Web browser exploits
- PDF readers
- Office macros
- Remote code execution in applications

#### **Browser & Script Engine Zero-Days**
Very common because browsers are huge attack surfaces:
- V8 (Chrome)
- WebKit (Safari)
- Chakra (legacy Edge)

#### **Hardware Zero-Days**
- CPU speculative execution (Spectre, Meltdown)
- Firmware bugs
- Baseband (cell modem) vulnerabilities

#### **Cloud & Virtualization Zero-Days**
- Hypervisor escape flaws
- Container breakout flaws
- Cloud API misprocessing

#### **Mobile Zero-Days**
- iOS and Android kernel flaws
- Baseband RCE
- App sandbox escapes

---
### Zero-Day Vulnerabilities vs. Other Vulnerability Categories

|Concept|Meaning|Patch Exists?|Known to Vendor?|
|---|---|---|---|
|**Zero-day vulnerability**|Unknown flaw|❌ No|❌ No|
|**N-day vulnerability**|Known flaw|✔ Patch exists|✔ Yes|
|**Unpatched system**|Admin didn’t apply patch|✔ Yes|✔ Yes|
|**Misconfiguration**|Settings incorrect|N/A|N/A|
|**Exploit kit**|Uses _known_ vulnerabilities|✔ Usually|✔ Usually|

CompTIA _loves_ asking about these differences.

---
### How Zero-Days Are Discovered
Zero-days are found through:
- **fuzzing** (feeding random or malformed input into an app)
- **reverse engineering**
- **code audits**
- **bug bounty research**
- **accidental crashes revealing memory issues**
- **nation-state research teams**

---
### How Zero-Days Are Used by Attackers
Zero-days are often used for:
- **initial intrusion**
- **privilege escalation**
- **sandbox escape**
- **persistence**
- **bypassing EDR/AV**

They often appear in:
- phishing attachments
- drive-by downloads
- malicious websites
- compromised apps or extensions
- mobile spyware

Zero-days are frequently used **alongside** other techniques:
- [[21-Phishing#Common Types Of Phishing|spear phishing]] → zero-day → backdoor → lateral movement

---
### Mitigation Strategies (Security+ Wants You to Know These)
You _cannot_ patch a zero-day, but you can **reduce the effects** of one.
#### **Defense in Depth**
Multiple layers:  
WAF → EDR → sandboxing → segmentation → least privilege → monitoring.

#### **Behavioral/Heuristic Detection**
Because signature-based detection fails.

EDR looks for:
- abnormal memory usage
- unusual API calls
- privilege escalation patterns
- ransomware-like behavior

#### **Patch as soon as vendor releases fix**
Speed matters.

#### **Virtualization & Container Isolation**
Limit blast radius.

#### **Least Privilege**
If a user or process has minimal rights, a zero-day gives attackers less access.

#### **Network Segmentation**
Attackers can’t move laterally easily.

#### **Application Whitelisting**
Only approved programs can execute — prevents arbitrary payloads.

#### **Threat Intelligence Feeds**
Alert you to active exploitation in the wild.

#### **Sandboxing / Browser Security**
Restrict what exploits can do.

---
### How Zero-Day Connects to What You’ve Already Studied

| Topic                                                                                      | Relationship                                    |
| ------------------------------------------------------------------------------------------ | ----------------------------------------------- |
| **[[25-Memory-Injections\|Memory Injection]] / [[26-Buffer-Overflows\|Buffer Overflows]]** | Common cause of zero-days                       |
| **[[27-Race-Conditions\|Race Conditions]]**                                                | Many zero-days are logic timing bugs            |
| **[[33-Virtualization-Vulnerabilities\|Virtualization]]**                                  | Hypervisor zero-days allow VM escape            |
| **[[34-Cloud-specific-Vulnerabilities\|Cloud Vulnerabilities]]**                           | Cloud APIs and IAM logic flaws can be zero-days |
| **[[37-Mobile-Device-Vulnerabilities\|Mobile Vulnerabilities]]**                           | Baseband zero-days widely used in spyware       |
| **[[35-Supply-Chain-Vulnerabilities\|Supply Chain]]**                                      | Zero-days sometimes inserted into build systems |
| **[[32-Hardware-Vulnerabilities\|Hardware Vulnerabilities]]**                              | Spectre/Meltdown were CPU-level zero-days       |
| **Defense in Depth**                                                                       | Only reliable mitigation strategy               |

Zero-days are basically the **intersection of all vulnerability classes**, before the world knows they exist.