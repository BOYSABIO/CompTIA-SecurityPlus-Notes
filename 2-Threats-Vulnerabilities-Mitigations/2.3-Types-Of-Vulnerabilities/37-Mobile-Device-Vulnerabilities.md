# Mobile Device Vulnerabilities
Mobile devices differ from desktops because they have:
- **Baseband radios** (cellular modems)
- **Multiple comms** (Wi-Fi, Bluetooth, NFC)
- **Highly privileged firmware**
- **App stores / mobile ecosystems**
- **Sensors** (GPS, camera, mic, accelerometer)
- **Always-on nature**
- **Cloud-connected identity** (Apple ID, Google account)

This creates attack surfaces that simply **don’t exist** on regular PCs.

---
### Major Categories of Mobile Vulnerabilities

#### **Outdated OS or Firmware**
Mobile devices (especially Android) often run:
- Unsupported versions
- OEM-customized builds
- Delayed security patches

Risks:
- Kernel vulnerabilities
- Privilege escalation
- RCE from malicious apps
- Bootloader exploits

**Exam trigger:**
> “Mobile device cannot be patched due to vendor restrictions.”

#### **Jailbreaking / Rooting**
Users remove OS restrictions.

Risks:
- Removes sandbox protections
- Allows untrusted apps to gain root access
- Breaks secure boot
- Allows sideloading unsigned code
- Reduces integrity of OS

**Exam trigger:**
> “User bypassed manufacturer restrictions for more control.”

#### **Malicious or Vulnerable Apps (App-Based Attacks)**
Examples:
- Apps requesting excessive permissions
- Sideloaded apps (APK files)
- Malicious apps from unofficial stores
- Supply chain apps hiding malware
- Insecure app coding (XSS, SQLi inside apps)

Mobile apps are often **over-permissioned**, making them ideal for stealing:
- contacts
- SMS messages
- GPS location
- microphone/camera data
- stored credentials

#### **Insecure Communications**
Mobile devices rely on radio technologies:
- Wi-Fi
- Bluetooth
- NFC
- Cellular (LTE/5G baseband)

Risks:
- Rogue access points
- Evil twin APs
- Bluetooth exploits
- NFC relay attacks
- Baseband vulnerabilities

**Exam trigger:**
> “Device automatically connected to rogue Wi-Fi.”

#### **SIM-Based & Cellular Attacks (Baseband Layer)**
The _baseband processor_ runs its own firmware. If compromised, it can:
- intercept calls
- read SMS
- perform MITM attacks
- track device location

Examples:
- SS7 vulnerabilities
- IMSI catchers / Stingrays
- SIM hijacking via carrier social engineering

#### **Mobile Device Theft / Physical Access Risks**
Mobile devices = small + portable = easily stolen.

Risks:
- Unencrypted storage
- Locked-out screens bypassable
- Token apps accessible
- Cloud accounts auto-logged in

Mitigations:
- Mobile Device Management (MDM)
- Remote lock and wipe
- Full disk encryption (FDE)
- Biometrics

#### **Weak or Missing MDM Controls**
Without MDM, organizations cannot enforce:
- passcode requirements
- encryption
- app restrictions
- remote wipe
- OS version compliance
- geofencing

This makes phones easily exploitable.

**Exam trigger:**
> “BYOD (bring your own device) device lacked enforced security policies.”

#### **Insecure App Permissions**
Mobile OS permissions include access to:
- Camera
- Microphone
- Contacts
- SMS
- GPS
- Clipboard
- Storage

Apps can abuse these permissions even if they’re not malicious.

Example: A flashlight app requesting GPS, camera, and contact permissions → suspicious.

#### **Mobile Malware**
Types include:
- Trojans
- Keyloggers
- Spyware
- Adware
- Stalkerware
- SMS interceptors
- Banking malware
- Mobile ransomware

Delivery:
- Malicious apps
- SMS phishing (smishing)
- Malicious QR codes
- Fake app stores
- Compromised websites

#### **Location Tracking & Sensor Exploits**
Sensors can leak information:
- GPS
- Accelerometer
- Gyroscope
- Magnetometer
- Camera / microphone

Attackers can:
- track movement
- infer keystrokes
- activate sensors silently (if permissions are abused)

#### **Mobile Browser Vulnerabilities**
Attack surface includes:
- XSS
- CSRF
- Malicious pop-ups
- Malicious profiles (iOS mobileconfig)
- Browser zero-days

#### **Unsecured Backups**
Cloud backups may store:
- messages
- call recordings
- app data
- credentials

If cloud accounts aren't protected (MFA, strong passwords) → major breach risk.

---
### Mobile Device Management (MDM) as a Defense
Security+ expects you to know what MDM can do.

**MDM Capabilities:**
- Enforce encryption
- Enforce passcodes
- Block jailbroken/rooted devices
- Restrict app installation
- Require VPN usage
- Enable secure containers (corporate sandbox)
- Remote lock/wipe
- Device geofencing
- Certificate deployment
- Email policy enforcement

MDM is **critical** for preventing mobile vulnerabilities.

---
### Mobile-Specific Attack Techniques (Exam Favorites)

| Attack                                                 | Description                                    |
| ------------------------------------------------------ | ---------------------------------------------- |
| **[[21-Phishing#Common Types Of Phishing\|Smishing]]** | SMS phishing                                   |
| **SIM swapping**                                       | Carrier social engineering to take over number |
| **QR code attacks**                                    | Malicious URLs or Wi-Fi configs                |
| **App wrapping**                                       | Secure container for corporate apps            |
| **Side-loading**                                       | Installing apps outside official store         |
| **NFC relay attacks**                                  | Payment or access badge cloning                |

---
### How This Connects to Previous Topics

| Previous Topic                                                            | Connection                                 |
| ------------------------------------------------------------------------- | ------------------------------------------ |
| **[[32-Hardware-Vulnerabilities\|Hardware vulnerabilities]]**             | Baseband, SIM, JTAG, sensors               |
| **[[33-Virtualization-Vulnerabilities\|Virtualization vulnerabilities]]** | Mobile sandboxing → app isolation issues   |
| **[[34-Cloud-specific-Vulnerabilities\|Cloud vulnerabilities]]**          | Mobile apps heavily tied to cloud APIs     |
| **[[36-Misconfiguration-Vulnerabilities\|Misconfigurations]]**            | App permissions, Wi-Fi trust levels        |
| **[[24-Other-Social-Engineering-Attacks\|Social engineering]]**           | Smishing, SIM hijacking                    |
| **[[35-Supply-Chain-Vulnerabilities\|Supply chain]]**                     | Malicious apps, compromised app stores     |
| **[[12-Encrypting-Data\|Cryptography]]**                                  | Mobile relies on FDE, secure enclaves, PKI |
