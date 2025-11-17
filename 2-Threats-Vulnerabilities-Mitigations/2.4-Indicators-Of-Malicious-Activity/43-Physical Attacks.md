# Physical Attacks
Physical attacks are attacks that require **direct physical access** to a device, facility, or environment.  
They bypass digital security entirely and focus on _touching_ or _manipulating_ hardware or people.

They’re often:
- low tech
- high impact
- difficult to detect
- impossible to fix with software controls

---
### **Impersonation Attacks**
Attacker pretends to be:
- a technician
- a delivery person
- maintenance worker
- third-party vendor
- an employee

Goal:
- access restricted areas
- plug in malicious devices
- collect badges
- steal hardware
- install malware physically

**Exam trigger:**
> “Attacker wearing a uniform gained access to the server room.”

Mitigation:
- Access badges
- Security guards
- Visitor logs
- Mantraps
- Challenge procedures (“Who are you here to see?”)

---
### **Tailgating / Piggybacking**

#### **Tailgating**
Unauthorized person follows an authorized person through a secure door **without permission**.

#### **Piggybacking**
Authorized person _knowingly_ allows another to follow.

CompTIA simplifies it → both are physical social engineering.

**Exam trigger:**
> “Employee held the door open for someone without verifying identity.”

Mitigation:
- Turnstiles
- Mantraps
- Access control
- Awareness training

---
### **Dumpster Diving**
Searching trash for:
- passwords
- printed network diagrams
- employee badges
- hardware with data
- shipping labels
- invoices with sensitive info

**Exam trigger:**
> “Attacker recovered sensitive documents from outside containers.”

Mitigation:
- Shredders
- Locked dumpsters
- Secure document disposal

---
### **Skimming**
Used to clone credentials or payment info.

Examples:
- **RFID badge skimming** (building access)
- **NFC or proximity card cloning**
- **Magstripe skimmers**
- **ATM skimmers**
- **Gas pump skimmers**

Key idea: The attacker **captures the signal** and duplicates it.

Mitigation:
- RFID shield sleeves
- Disable unnecessary badge frequencies
- Tamper-evident seals

---
### **Card Cloning / Card Shimming**
A modern version of skimming:

#### **Shimming** — a tiny device inserted INTO a card slot (chip/EMV) to intercept chip communication.

Exam trigger:
> “Thin device inside card reader capturing chip card data.”

---
### **Eavesdropping / Shoulder Surfing**
Watching someone type:
- passwords
- PINs
- passphrases
- door codes

Or listening to:
- phone calls
- confidential conversations

Mitigation:
- Privacy screens
- Positioning screens away from public view
- Awareness
- Shielding keypad with hand

---
### **Replay Attacks (Physical Context)**
Occurs when attacker intercepts **RFID or wireless key signals**, then replays them to unlock:
- cars
- buildings
- restricted areas

This is _not_ crypto replay — it’s physical access replay.

Mitigation:
- Rolling codes
- RFID shielding
- NFC distance limitations

---
### **Evil Maid Attacks**
Attacker with _brief physical access_ installs:
- spyware
- keyloggers
- hardware implants
- malicious USB payloads
- bootloader tampering

This is named after “a maid entering a hotel room to attack a laptop.”

**Exam trigger:**
> “Laptop left unattended in a hotel room was modified.”

Mitigation:
- Disk encryption
- Secure boot
- TPM
- Locking devices
- Boot passwords

---
### **USB Drops / Baiting**
Attacker leaves:
- USB drives
- SD cards
- chargers (O.MG cables)
- malicious devices disguised as keyboards

Goal:
- curiosity leads users to plug them in
- malware executes
- system is compromised

**Exam trigger:**
> “Employee plugged a found USB drive into their computer.”

---
### **Hardware Implants**
Physical devices secretly inserted into:
- cables
- keyboards
- network taps
- USB hubs
- chargers
- servers
- routers

Examples:
- Keylogger dongles
- O.MG cable
- Raspberry Pi hidden in office
- Malicious NIC firmware

These allow:
- remote access
- monitoring
- backdoors
- interception

Mitigation:
- Supply chain security
- Physical inspections
- Tamper-evident seals

---
### **Sabotage / Destruction Attacks**
Targeting physical infrastructure:
- cutting network cables
- damaging servers
- destroying storage media
- power disruption
- arson (rare but exam mentions "fire or water damage")

Often insider or disgruntled employee.

---
### **Shoulder Surfing**
Simple but effective:
- Looking over someone’s shoulder
- Observing PIN entry
- Watching keyboard from reflection (window, glasses)

---
### **Social Engineering in Physical Context**
Physical attacks often use social engineering to:
- gain trust
- blend in
- bypass controls
- manipulate helpful employees

Physical + social engineering = very common attack path.

---
### How This Connects to Previous Topics

| Topic                                                                              | Connection                                                           |
| ---------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| **[[24-Other-Social-Engineering-Attacks\|Social engineering]]**                    | Many physical attacks start with [[22-Impersonation\|impersonation]] |
| **[[37-Mobile-Device-Vulnerabilities\|Mobile vulnerabilities]]**                   | RFID/NFC and physical access issues                                  |
| **[[35-Supply-Chain-Vulnerabilities\|Supply chain attacks]]**                      | Hardware implants inserted physically                                |
| **[[32-Hardware-Vulnerabilities\|Hardware vulnerabilities]]**                      | Evil maid attacks target firm/boot chain                             |
| **[[39-An-Overview-Of-Malware\|Malware]]**                                         | USB drops deliver Trojans, RATs, ransomware                          |
| **[[06-Zero-Trust\|Zero trust]]**                                                  | Prevents trusting physical presence alone                            |
| **[[01-Security-Controls#Control Types by Function\|Physical security controls]]** | Mitigate physical attacks                                            |
