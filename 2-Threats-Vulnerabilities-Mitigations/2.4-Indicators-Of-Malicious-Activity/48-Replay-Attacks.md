# Replay Attacks
A **Replay Attack** occurs when an attacker:
1. **Captures valid data** (usually authentication traffic),
2. **Re-sends (“replays”) that data later**,
3. Trick the system into thinking the attacker is the original sender.

This allows **unauthorized access** _without_ cracking passwords.
Replay attacks do **NOT** require modifying packets — just resending them.

---
### What Replay Attacks Target Most Often
#### ✔ [[04-Authentication-Authorization-&-Accounting#Authentication - Verifying Identity|Authentication]] Protocols
Old or weak authentication methods are extremely vulnerable:
- NTLMv1
- Kerberos (without proper anti-replay protections)
- HTTP cookies/session tokens
- Wireless authentication (WPA/WEP, old EAP)
- Legacy systems without timestamps

#### ✔ Access control systems
Attacker replays:
- RFID badge signals
- NFC tap info
- Garage door or car door signals
- Key fobs without rolling codes

This is why rolling codes were invented.

---
### Replay Attack Process (Simplified)
1. **Record** – attacker uses packet capture tools (Wireshark, aircrack-ng, etc.)
2. **Extract** meaningful authentication data
3. **Replay** the same data to bypass authentication
4. **Gain access** as the victim

No need for:
- password cracking
- brute force
- malware

Just captured traffic.

---
### Replay vs MITM (Critical Exam Difference)
Replay is **NOT** a MITM attack by default.

| Replay Attack                            | On-Path (MITM)                                               |
| ---------------------------------------- | ------------------------------------------------------------ |
| Replays previously captured messages     | Actively intercepts + possibly modifies traffic in real time |
| No need to modify packets                | Interception + modification possible                         |
| One-time or repeated replay              | Ongoing attack                                               |
| Doesn’t require altering connection flow | Must be in the middle of devices                             |

Security+ LOVES to test this subtle difference.

---
### Common Types of Replay Attacks

#### **1. Credential Replay (Login Replay)**
Attacker replays:
- authentication packets
- login tokens
- session cookies
- kerberos tickets
- API authentication headers

#### **2. Wireless Replay**
Used with:
- WEP
- WPA handshake capture attempts
- EAP replay abuse

Attackers replay captured frames to:
- reauthenticate
- force handshake
- bypass authentication

#### **3. RFID / NFC Replay**
Attacker captures RFID badge signal → replays it → opens door.

Exam trigger:
> “Attacker captured badge data and used it to gain access.”

#### **4. Replay for Token Reuse**
JWT, OAuth, SAML tokens reused after capture.

#### **5. Replay in ICS/SCADA**
Replayed control commands:
- open/close valves
- change settings
- start/stop machinery

Since old ICS uses no encryption → highly vulnerable.

---
### Examples That Appear on Security+

#### **Kerberos Replay**
An attacker captures a valid Kerberos ticket and reuses it.  
Mitigation: timestamps and ticket lifetimes.

#### **NTLM Relay Attack**
Capturing NTLM info and “relaying” it to another system.  
Not strictly replay but closely related.

#### **WEP Authentication Replay Attack**
Replaying authentication packets in WEP reveals key stream because WEP has no protection.

#### **HTTP Cookie Replay**
Attacker captures session cookie and reuses it to impersonate the user.

---
### Replay Attack Mitigations (Very Important)

#### ✔ **Timestamps and Nonces**
Most powerful defense.
- Each request has unique nonce
- Cannot be replayed
- Server rejects old messages
- Used in Kerberos, OAuth, API security

#### ✔ **Session Tokens with Expiration**
Short-lived session tokens stop long-term replay.

#### ✔ **TLS/HTTPS**
Encrypts authentication, preventing attackers from capturing it.

#### ✔ **Mutual Authentication**
Client + server both verify identity → replay harder.

#### ✔ **Digital Signatures**
Signing the content of messages makes replay invalid unless attacker can forge signature.

#### ✔ **802.11w (Protected Management Frames)**
Stops many wireless replay attacks.

#### ✔ **Rolling Codes**
Uses a new code each time:
- modern car key fobs
- garage doors
- NFC devices

#### ✔ **Strong Network Segmentation**
Limits exposure of broadcast authentication protocols.

---
### How This Connects to Previous Topics

| Topic                                                                          | Connection                                           |
| ------------------------------------------------------------------------------ | ---------------------------------------------------- |
| **[[47-On-path-Attacks\|On-path attacks]]**                                    | Replay often requires capturing data first           |
| **[[46-Wireless-Attacks\|Wireless attacks]]**                                  | Deauth → capture handshake → replay                  |
| **RFID/NFC attacks**                                                           | Badge replay is extremely common                     |
| **Session hijacking**                                                          | Replay = one type of session hijacking               |
| **[[38-Zero-day-Vulnerabilities\|Zero-day]]**                                  | Some replay vulnerabilities come from unknown flaws  |
| **[[04-Authentication-Authorization-&-Accounting\|Authentication protocols]]** | Replay attacks exploit weak auth (NTLMv1, WEP, etc.) |

Replay attacks bridge networking, authentication, wireless, and [[07-Physical-Security|physical security]].