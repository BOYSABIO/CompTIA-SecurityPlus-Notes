# Spyware & Bloatware
**Spyware** = malware designed to **monitor**, **collect**, or **exfiltrate** user data without consent.

It focuses on:
- **Surveillance**
- **Data theft**
- **Behavior tracking**
- **Credential harvesting**

Spyware can be:
- Part of a trojan
- Bundled with “free” software
- Installed via phishing
- Delivered through malicious ads
- Installed by insiders
- Installed via physical access

---
### Types of Spyware (Security+ Exam Focus)

#### **Keyloggers**
Record:
- keystrokes
- passwords
- chat messages
- credential forms

Exam trigger:
> “Passwords typed into a form were captured.”

#### **Screen Scrapers**
Take periodic screenshots or capture active windows.

#### **Browser Hijackers**
Modify:
- home page
- search engine
- browser settings
- redirect traffic
- inject ads

#### **Credential Stealers**
Focused on:
- password vaults
- cookies
- browser saved passwords
- session tokens

#### **Adware (borderline spyware)**
Displays ads but often **tracks** user behavior.  
Exam sometimes groups adware under spyware when it collects data.

#### **Stalkerware (high-risk, targeted spyware)**
Installed by:
- spouses
- employers
- insiders

Used to track:
- GPS
- messages
- calls
- photos
- microphone

Exam trigger:
> “Mobile device sending location and call data without user consent.”

#### **Mobile Spyware**
- SMS interceptors
- Fake “permissioned” apps
- Hidden background services
- Android/iOS enterprise profile abuse

Spyware LOVES mobile platforms due to excessive permissions.

---
### How Spyware Gets Installed
#### **Through user action:**
- Fake downloads
- Trojan installers (“free PDF converter”)
- Malicious browser extensions
- Bundled software
- Pop-up consent scams

#### **Through exploits:**
- Malvertising
- Drive-by downloads
- OS/application vulnerabilities
- Zero-days

#### **Through physical access / insiders:**
- Stalkerware
- Corporate monitoring tools abused
- Evil maid attacks

Exam trigger:
> “User installed a free program and suddenly has pop-ups, redirects, and system slowdown.”

---
### Spyware Behavior (Key Indicators)
Look for:
- Slow computer
- Excessive outbound network traffic
- New toolbars or browser extensions
- Modified browser homepage
- Unwanted ads
- Strange processes
- Webcam/microphone activation
- Unknown scheduled tasks
- C2 beaconing

CompTIA loves questions where “devices are slowing down and showing ads” → spyware/adware.

---
### How to Detect Spyware

#### **Host-based AV/EDR**
Behavior-based detection (keylogging, hooking APIs)

#### **Anti-spyware tools**
Specifically removes adware and tracking software

#### **Browser monitoring**
Detects unauthorized browser extensions

#### **Network analysis**
Detects:
- beaconing
- exfiltration
- command-and-control servers

#### **Mobile device management (MDM)**
Detects unauthorized apps or device profiles

---
### Spyware Mitigation
#### **Endpoint Security**
- EDR/AV
- Application whitelisting
- Disable unapproved browser extensions

#### **User Training**
- Avoid “freeware” traps
- Don’t install unknown apps
- Don’t sideload APKs

#### **Hardening**
- Patch OS & apps
- Harden browsers
- Limit admin rights

#### **Mobile Security**
- Require MDM
- Prevent sideloading
- Require app store-only installs
- Watch for unusual permissions

#### **Network Controls**
- DNS filtering
- Blocking known tracking domains
- SIEM alerting on abnormal outbound traffic

---
### What Bloatware Is (Exam Definition)
**Bloatware** is NOT malware.  
Security+ categorizes it as **unwanted, preinstalled, unnecessary software** that comes with devices (especially mobile and OEM laptops).

Examples:
- Trial antivirus
- Manufacturer apps
- Embedded games
- “Cleaner” apps
- Preloaded partner apps

#### Bloatware risks:
- Consumes resources
- Expands attack surface
- May include privacy-invasive adware
- Potentially includes hidden analytics/telemetry
- May require updates (supply chain risk)

**Exam trick:**  
Bloatware itself ≠ malicious  
But it _can_ include adware or tracking components → which _is_ malicious.

---
### Bloatware Mitigation
- Use enterprise images / gold images
- MDM to remove or block preinstalled apps
- Application allowlisting
- Device hardening
- Running debloat scripts (Windows, Android OEM)

---
### Spyware vs Bloatware (CompTIA Loves This Distinction)

| Feature      | Spyware               | Bloatware                 |
| ------------ | --------------------- | ------------------------- |
| Purpose      | Malicious             | Unwanted                  |
| Installs via | Exploit or user       | Vendor/OEM                |
| Behavior     | Steals data, monitors | Slows device, shows ads   |
| Detection    | AV/EDR                | Inventory, app management |
| Risk Level   | High                  | Low–medium                |

If scenario mentions:
- tracking
- keylogging
- redirects
- data exfiltration  
    → **Spyware**

If scenario mentions:
- preinstalled
- resource-heavy
- unnecessary  
    → **Bloatware**

---
# How This Connects to Previous Topics

| Previous Topic                                                   | Connection                                        |
| ---------------------------------------------------------------- | ------------------------------------------------- |
| **[[39-An-Overview-Of-Malware\|Malware overview]]**              | Spyware is a core malware family                  |
| **[[37-Mobile-Device-Vulnerabilities\|Mobile vulnerabilities]]** | Bloatware is common on mobile devices             |
| **[[36-Misconfiguration-Vulnerabilities\|Misconfigurations]]**   | Excessive permissions allow spyware to operate    |
| **[[24-Other-Social-Engineering-Attacks\|Social engineering]]**  | Spyware often disguised as legitimate apps        |
| **[[38-Zero-day-Vulnerabilities\|Zero-day]]**                    | Spyware sometimes delivered via zero-day exploits |
| **[[35-Supply-Chain-Vulnerabilities\|Supply chain]]**            | Bloatware sometimes comes from OEM vendors        |
