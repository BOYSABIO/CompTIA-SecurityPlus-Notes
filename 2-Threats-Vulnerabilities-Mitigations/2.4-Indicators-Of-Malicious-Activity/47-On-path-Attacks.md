# On-path Attacks
**On-path attack (formerly “man-in-the-middle”)** =  
An attacker secretly positions themselves _between_ two endpoints and can:
- **observe** (eavesdrop)
- **modify** (alter messages)
- **inject** (insert new content)
- **redirect** (send to malicious destination)

… without either party knowing.
This compromises **[[02-The-CIA-Triad#Confidentiality|confidentiality]]** and **[[02-The-CIA-Triad#Integrity|integrity]]**, and sometimes **[[02-The-CIA-Triad#Availability|availability]]**.

---
### The Three Core Abilities of On-Path Attackers
Every MITM/on-path attack has some combination of:

#### **Interception (Eavesdropping)**
Reading traffic in transit.
#### **Modification (Tampering)**
Changing packets: altering DNS responses, injecting JavaScript, editing data.
#### **Impersonation (Spoofing)**
Acting as one endpoint to the other.

**CompTIA loves questions where attacker “intercepts and modifies communications.” → on-path attack.**

---
### How Do Attackers Get “In the Middle”?
They must **redirect traffic through them**, usually using:

#### **1. ARP Poisoning (LAN MITM)**
The most important one.

Attackers send fake ARP replies like:
- “I am the gateway”
- “Send your traffic to my MAC address”

Clients update their ARP tables → traffic flows _through the attacker_.

**Exam triggers**:
- “Attacker is flooding ARP tables”
- “Gateway MAC address changed”
- “Unencrypted traffic observed from the victim”

Mitigation:
- Dynamic ARP Inspection (DAI)
- Static ARP entries
- VLAN segmentation
- Encryption (TLS)

#### **2. MAC Spoofing / MAC Flooding**
##### MAC Spoofing
Attacker impersonates another device’s MAC address.
##### MAC Flooding
Attacker overloads the switch’s CAM table → switch fails open → floods all traffic → attacker sniffs frames.

Mitigation:
- Port security
- Sticky MAC
- VLAN separation

#### **3. DNS Spoofing / DNS Poisoning**
A form of MITM for redirection:
- Attacker responds with forged DNS reply
- Victim visits malicious IP instead of real server
- Attacker proxies traffic and captures credentials

This is how many _evil twin_ attacks work.

#### **4. DHCP Spoofing**
Attacker runs a rogue DHCP server that hands out:
- wrong default gateway
- wrong DNS server
- attacker’s IP as router

Result: ALL traffic routes through attacker.

**Exam trigger:**
> “Clients received incorrect gateway/DNS information from DHCP.”

#### **5. Evil Twin (Wireless MITM)**
Attacker builds a fake Wi-Fi AP → victims connect → attacker intercepts traffic.

Often paired with:
- DNS spoofing
- captive portal credential harvesting
- SSL-strip attacks

#### **6. HTTPS Downgrade / SSL-Strip**
Attacker redirects HTTPS → HTTP:
- Removes HTTPS links
- Victim thinks they’re secure
- Traffic becomes plaintext
- Attacker captures credentials

Mitigation:
- HSTS (forces HTTPS)
- Certificate pinning
- Modern browsers warn on downgrade

#### **7. Proxy-based MITM**
Attacker installs or forces a proxy (malicious or misconfigured):
- Transparent proxy
- WPAD (Web Proxy Auto-Discovery) abuse
- Malware modifying proxy settings
- Corporate MITM inspection gone wrong

#### **8. VPN hijacking / Session hijacking**
Attacker steals session tokens or cookies via MITM → impersonates user.

---
### On-Path Attack Examples (CompTIA Wants You to Recognize These)

#### **1. ARP Poisoning**
Most common LAN MITM.
#### **2. DNS Spoofing**
Redirect user to malicious site.
#### **3. Evil Twin Attack**
Wireless MITM.
#### **4. HTTPS Downgrade / SSL Strip**
Forced insecure connection.
#### **5. Proxy Manipulation**
Traffic forced through attacker-controlled gateway.
#### **6. Session Hijacking**
Steal session tokens mid-transit.

---
### What On-Path Attacks Are NOT (Common Exam Traps)
- **Replay attack**  
    → Re-sending captured packets, NOT necessarily in the middle.
- **Refactoring/injection**  
    → Code modification, not intercepting traffic.
- **DNS amplification / DDoS**  
    → Availability attack, not eavesdropping.
- **Wireless jamming**  
    → Not on-path, just DoS.
- **Spoofing alone**  
    → May be used for MITM, but not MITM itself.

---
### On-Path Attack Goals
Attackers gain:
- **Credentials** (login details, session tokens)
- **Sensitive data** (emails, chats, financial)
- **Ability to modify transactions**
- **Traffic redirection**
- **MITM persistence** (long-term access)

---
### Strong Mitigations (Exam-Focused)

#### **1. Encryption**
- TLS / HTTPS (end-to-end)
- SSH
- VPN

Even if MITM captures packets, they can't decrypt them (unless downgrade attack).

#### **2. Certificate Pinning**
Prevents fake certs in MITM downgrades.

#### **3. DHCP Snooping**
Prevents rogue DHCP servers.

#### **4. Dynamic ARP Inspection (DAI)**
Stops ARP spoofing.

#### **5. Port Security**
Prevents MAC flooding.

#### **6. Network Segmentation**
Reduces the blast radius of ARP/Layer 2 attacks.

#### **7. WLAN Defenses**
- 802.1X
- WPA3
- Protected management frames (802.11w)

---
### How This Connects to Everything Else You’ve Studied

| Topic                                         | Connection                                       |
| --------------------------------------------- | ------------------------------------------------ |
| **[[46-Wireless-Attacks\|Wireless attacks]]** | Evil twin, deauth → MITM setup                   |
| **[[45-DNS-Attacks\|DNS attacks]]**           | DNS spoofing is a classic on-path attack         |
| **[[43-Physical Attacks\|Physical attacks]]** | Rogue AP insertion / rogue devices often used    |
| **[[06-Zero-Trust\|Zero trust]]**             | Prevents trusting the network path               |
| **[[39-An-Overview-Of-Malware\|Malware]]**    | RATs and Trojans sometimes install MITM proxies  |
| **[[44-Denial-Of-Service\|DDoS]]**            | On-path attackers sometimes create DDoS as cover |
| **Replay attacks**                            | Often performed after MITM capture               |