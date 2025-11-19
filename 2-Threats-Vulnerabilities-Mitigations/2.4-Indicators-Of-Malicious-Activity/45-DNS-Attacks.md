# DNS Attacks
DNS (Domain Name System) translates **domain names → IP addresses**.  
Because of this, attacking DNS lets an attacker:
- Redirect victims
- Intercept traffic
- Deny access
- Manipulate name resolution
- Poison caches
- Hijack domains

CompTIA loves this topic.

---
### **DNS Poisoning / DNS Cache Poisoning**
This is the _most important_ DNS attack.
#### What it is:
Attacker inserts false DNS records into a DNS resolver’s cache.

Example:
- You try to visit `bank.com`
- DNS server returns attacker-controlled IP
- You land on a phishing site

#### How it happens:
- Compromising a DNS server
- Exploiting weak transaction IDs (older systems)
- Sending forged DNS responses faster than the legitimate one
- Local cache poisoning via malware

#### Exam triggers:
- “Users are redirected to a malicious site”
- “DNS cache contained incorrect A records”
- “DNS response spoofing”

**This compromises [[02-The-CIA-Triad#Integrity|INTEGRITY]].**

---
### **DNS Spoofing / DNS Response Tampering**
Similar to cache poisoning, but happens _in transit_.  
Attacker intercepts/forges DNS response packets.

#### Example:
- MITM attacker responds with fake IP
- Victim’s machine never gets the legitimate DNS response

#### Exam clue:
> “Attacker sent forged DNS responses faster than the real server.”

---
### **DNS Hijacking**
Attacker gains **control** over a DNS server or domain registrar account.
This is bigger than poisoning because it modifies:
- Authoritative DNS
- Registrar records
- Name server entries
- DNS zones

Results:
- Full domain takeover
- Users redirected to malicious IP everywhere

#### Exam trigger:
> “DNS records at registrar were modified.”

Mitigation:
- Registrar lock
- MFA on domain accounts
- DNSSEC

---
### **Domain Hijacking**
Similar to DNS hijacking but focused on **ownership** transfer.

Examples:
- Attacker steals registrar credentials
- Changes domain ownership
- Takes over entire domain identity

Exam trigger:
> “Attacker changed ownership information and took control of the domain.”

---
### **DNS Amplification Attack (DDoS)**
A **volumetric DDoS attack** using DNS servers.

#### How it works:
1. Attacker spoofs victim’s IP
2. Sends small DNS request to open resolvers
3. DNS servers reply with LARGE responses to the victim
4. Victim receives massive traffic → overwhelmed

Amplification ratio can be huge (up to 100x+).

#### Exam trigger:
- “Small requests → massive DNS responses”
- “Traffic from DNS servers overwhelming victim”
- “Reflective DDoS attack”

Mitigation:
- Disable open resolvers
- Use rate limiting
- Cloud DDoS services

---
### **DNS Tunneling**
A covert communication method where attackers encode data inside **DNS queries and responses**.

Uses:
- Exfiltrating data
- Command and control (C2)
- Bypassing firewalls since DNS is often allowed everywhere

#### Example:
`secret_data.company.com`  
→ data encoded in subdomain → attacker-controlled DNS server decodes it.

#### Exam trigger:
> “DNS used to exfiltrate data through allowed outbound traffic.”

**This is a major Security+ favorite.**

Mitigation:
- DNS inspection / DNS firewall
- Detect anomalous DNS patterns
- Block unnecessary external DNS resolvers

---
### **Typosquatting (not strictly DNS but often tested here)**
Attacker registers domains that look similar to legitimate ones:
- gooogle.com
- faceboook.com
- amaz0n.net

Used for:
- phishing
- malware delivery
- ad-based redirection

Often paired with DNS manipulation.

---
### **Pharming**
Redirecting traffic to malicious sites by poisoning:
- local hosts file
- DNS resolver
- DHCP configuration (malicious DNS server assignment)

Exam trigger:
> “All users on the network were redirected to a fake financial website.”

Pharming = **mass redirection**.

---
### **Zone Transfer Attacks**
DNS zone transfers are used between DNS servers to synchronize data.

If not restricted, attackers can:
- request full zone transfers
- learn subdomains, hostnames, internal structure

Exam trigger:
> “DNS server allowed zone transfers from unauthorized hosts.”

Mitigation:
- Restrict AXFR to authorized IPs
- DNSSEC does NOT prevent this — it ensures integrity, not access control

---
### **DNSSEC (Defense)**
DNSSEC = DNS Security Extensions  
Provides:
- digital signatures for DNS records
- authenticity
- integrity

Stops:
- spoofing
- cache poisoning
- tampering

Does NOT:
- encrypt DNS
- stop amplification attacks
- stop DDoS
- secure endpoints

Exam trigger:
> “DNS responses are digitally signed.”

---
### How This Connects to Previous Topics

| Topic                                                          | Relationship                                               |
| -------------------------------------------------------------- | ---------------------------------------------------------- |
| **[[44-Denial-Of-Service\|DoS]]**                              | DNS amplification is major DDoS vector                     |
| **[[21-Phishing\|Phishing]]**                                  | DNS hijacking → phishing pages                             |
| **[[39-An-Overview-Of-Malware\|Malware]]**                     | Malware uses DNS tunneling for C2                          |
| **[[38-Zero-day-Vulnerabilities\|Zero-day]]**                  | DNS servers sometimes exploited with unknown flaws         |
| **MitM attacks**                                               | DNS spoofing is often part of MitM                         |
| **[[36-Misconfiguration-Vulnerabilities\|Misconfigurations]]** | Open resolvers & public zone transfers are misconfigs      |
| **[[35-Supply-Chain-Vulnerabilities\|Supply chain]]**          | DNS registrar accounts compromised in supply chain attacks |
