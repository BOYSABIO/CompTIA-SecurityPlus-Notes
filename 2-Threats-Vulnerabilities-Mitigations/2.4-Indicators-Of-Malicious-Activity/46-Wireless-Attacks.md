# Wireless Attacks
Wireless networks introduce **unique attack surfaces** because they broadcast information over the air.  
Anyone nearby can attempt to intercept, jam, impersonate, or manipulate traffic.

This section covers the major Wi-Fi–focused attacks CompTIA expects you to know.

---
### **Evil Twin Attack**
An attacker creates a **fake access point** (AP) with the same SSID as a legitimate network.

Victims connect to it, thinking it’s real.

Used for:
- Credential theft
- Man-in-the-middle (MitM)
- Captive portal phishing pages
- Traffic inspection

**Exam triggers:**
- “Duplicate wireless network”
- “Similar SSID”
- “Fake access point”
- “Users connecting to wrong AP”

Mitigation:
- Wireless intrusion detection (WIDS)
- 802.1X authentication
- Avoid open Wi-Fi
- VPN

---
### **Rogue Access Point**
A **non-malicious** or **accidentally installed** AP connected inside your network without security controls.

This could be:
- A user installing their own cheap Wi-Fi router
- A contractor plugging in wireless hardware
- An attacker placing an AP physically inside the building

This creates a **backdoor wireless entry point**.

**Exam trigger:**
> “Unauthorized AP connected to the corporate network.”

Mitigation:
- WIDS/WIPS
- Network access control
- Physical inspections

---
### **Deauthentication (Deauth) Attacks**
An attacker sends spoofed deauth frames to a client, forcing it to disconnect.

Used for:
- Capturing WPA/WPA2 4-way handshakes
- Forcing clients to join an evil twin
- Denial of service

WPA3 protects against this, but WPA2 is still vulnerable.

Exam trigger:
> “Wireless clients are repeatedly disconnected.”  
> “Attack uses spoofed management frames.”

Mitigation:
- 802.11w (protected management frames)
- WPA3

---
### **WPS Attacks (Wi-Fi Protected Setup)**
WPS uses an insecure PIN-based method to connect devices.

Attackers can brute-force the PIN:
- Only 11,000 possibilities
- Vulnerability in protocol
- No rate-limiting on some routers

This allows access to WPA/WPA2 keys.

**Exam trigger:**
- “PIN-based setup exploited”
- “Router with WPS enabled compromised”

Mitigation:
- Disable WPS
- Use WPA2/WPA3-PSK with strong password

---
### **Disassociation Attacks**
Similar to deauth:
- Sends a disassociation frame
- Forces the client to disconnect
- Can be part of a MitM attack
- Or used to cause DoS

Exam trigger:
> “Wireless clients dropped due to spoofed frames.”

---
### **Jamming / Interference Attacks**
Attacker overwhelms wireless frequencies with noise or high-power signals.

Results:
- Dropped connections
- Slow speeds
- Inability to connect

Types:
- **Constant jamming**
- **Random noise**
- **Reactive jamming**
- **Targeted jamming** (only specific channels)

Exam trigger:
> “Strong RF signal preventing wireless communication.”  
> “Interference on the same frequency.”

Mitigation:
- Detect signal anomalies
- Move to 5 GHz or other channels
- Directional antennas
- Physical security

---
### **Bluejacking**
Sending **unsolicited messages** over Bluetooth to nearby devices.

It’s mostly annoyance, not data theft.

Exam triggers:
>“Sending messages to nearby phones via Bluetooth.”

---
### **Bluesnarfing**
Attacker exploits Bluetooth for **unauthorized data access**, such as:
- contacts
- text messages
- files
- device info

This is a real breach of [[02-The-CIA-Triad#Confidentiality|confidentiality]].

Exam trigger:
> “Attacker accessed data over Bluetooth without permission.”

---
### **Bluebugging**
Attacker gains full remote control over a Bluetooth device:
- make calls
- send SMS
- enable microphone
- access Internet

More severe than bluesnarfing.

---
### **RFID/NFC Attacks**
Wireless technologies outside Wi-Fi.

#### RFID / NFC risks:
- Eavesdropping
- Replay attacks
- Cloning
- Skimming

Exam trigger:
> “Attacker captured badge signal and cloned it.”

---
### **WEP Cracking**
WEP is fundamentally broken because:
- small IV (24-bit)
- IV reuse leads to key recovery
- RC4 implementation flawed
- Attacks require only passive traffic capture

Exam trigger:
> “Legacy wireless network using RC4”  
> “IV reuse leads to key cracking”

---
### **Wireless Replay Attacks**
Attacker captures Wi-Fi packets (management or authentication) and replays them to:
- bypass authentication
- impersonate a client

Mitigation:
- WPA2/WPA3 exchange protections
- Protected management frames
- Randomized nonces

---
### **Wifi Password Cracking / Handshake Attacks**
#### WPA/WPA2-PSK attacks involve capturing the **4-way handshake**.
Requirements:
- Deauth the victim
- Capture handshake
- Perform offline dictionary/brute-force attack

Exam trigger:
> “Attacker captured WPA2 handshake and is performing offline cracking.”

---
### **Karma Attack**
An access point impersonates **ANY** SSID a client has in its preferred network list.

Used heavily in:
- Evil twin attacks
- Device tracking
- Credential theft

---
### **Ad-hoc Network Attacks**
Unauthorized peer-to-peer wireless connections between devices.

Risks:
- No central control
- Rogue device joining
- Malware propagation

---
### How This Connects to Previous Topics

| Topic                                                           | Connection                          |
| --------------------------------------------------------------- | ----------------------------------- |
| **[[44-Denial-Of-Service\|DoS]]**                               | Jamming is RF-based DoS             |
| **[[45-DNS-Attacks\|DNS attacks]]**                             | Evil twin often uses DNS spoofing   |
| **MitM**                                                        | Evil twin is textbook wireless MitM |
| **Credential attacks**                                          | Captive portals, handshake capture  |
| **[[32-Hardware-Vulnerabilities\|Hardware attacks]]**           | Rogue APs inserted physically       |
| **[[24-Other-Social-Engineering-Attacks\|Social engineering]]** | Fake login portals on evil twins    |
| **[[12-Encrypting-Data\|Encryption weaknesses]]**               | WEP cracking relies on IV reuse     |
