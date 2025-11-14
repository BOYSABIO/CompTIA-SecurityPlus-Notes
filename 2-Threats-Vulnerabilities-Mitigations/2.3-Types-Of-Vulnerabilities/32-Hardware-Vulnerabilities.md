# Hardware Vulnerabilities
It refers to any security weakness that exists at the **physical layer** or **hardware/firmware level**, not in the OS or software.

Think:
- CPUs
- Chipsets
- Memory modules
- BIOS/UEFI firmware
- Hardware components (NICs, GPUs)
- Peripheral devices (USB drives, printers)
- Embedded devices / IoT
- Supply chain tampering

These vulnerabilities are dangerous because they sit **below the OS** — meaning they can bypass most security controls.

---
### Common Categories of Hardware Vulnerabilities

#### **Firmware Vulnerabilities**
Firmware runs before the OS.  
If compromised → full system compromise.

Examples:
- UEFI/BIOS vulnerabilities
- Outdated router firmware
- Bootloader tampering
- Unpatched embedded device firmware
- Baseboard Management Controller (BMC/IPMI) exploits

**Ties back:**  
This directly connects to _[[28-Malicious Updates|malicious updates]]_ — a poisoned firmware update is catastrophic.

#### **Side-Channel Attacks (VERY exam-relevant)**
These attacks extract secrets by measuring **hardware behavior**, not software logic.

Examples:
- **Spectre** and **Meltdown** → CPU speculative-execution flaws
- **Power analysis** → measure power usage to extract keys
- **Electromagnetic analysis** → read signals from chips
- **Timing attacks** → response time reveals secrets
- **Tempest attacks** (EM monitoring)

**CIA impact:**  
Mostly **[[02-The-CIA-Triad#Confidentiality|confidentiality]]** (secret data leakage).

#### **Physical Interface Attacks**
Exploitation via physical ports or access points:
- **JTAG / UART debug ports**
- **FireWire/Thunderbolt DMA** (Direct Memory Access attacks)
- **PCIe/Thunderbolt DMA injection**
- **Cold boot attacks** (extract encryption keys from RAM)

**These bypass OS protections because DMA = raw memory access.**

#### **Removable Media Vulnerabilities**
Hardware-based vectors such as:
- Malicious USB devices
- Rubber Ducky
- Bash Bunny
- USB Killer
- HID spoofing (keyboard emulation)

Attackers use these to inject payloads or keystrokes at hardware speed.
**Connects to:** earlier topic on **Baiting** (free USB sticks).

#### **Fault Injection Attacks**
Manipulating hardware with glitches to make it behave incorrectly.

Methods include:
- Voltage glitching
- Clock manipulation
- Laser fault injection
- Rowhammer (flipping bits in adjacent memory cells)

Example: **Rowhammer** →  
Repeatedly accessing DRAM rows causes bits to flip in adjacent rows → can corrupt page tables or data.

#### **Malicious Hardware / [[20-Common-Threat-Vectors#Supply Chain & Third-Party Threats|Supply Chain Attacks]]**
Attackers tamper with hardware **before it enters your environment**.

Examples:
- Hidden chips added to motherboards
- Modified NICs or implants
- Rogue components in network devices
- Fake hardware masquerading as genuine (counterfeits)

Same theme as **malicious updates**, but at hardware level.

#### **Hardware Backdoors**
Manufacturers (or attackers) embed secret access mechanisms:
- Debug modes
- Hidden credentials
- Hardcoded encryption keys
- Backdoor admin ports
- ISP/modem “remote management modes”

These are extremely hard to detect and patch.

---
### How Hardware Vulnerabilities Are Exploited

Attackers gain:
- **Privileged access** (kernel or hypervisor level)
- **Persistence** that survives OS reinstallations
- **Stealth** (AV/EDR won’t see BIOS-level malware)
- **Ability to disable security features**
- **Direct memory access** (bypassing software protections)

**This directly ties to [[25-Memory-Injections|memory injection]], [[26-Buffer-Overflows|buffer overflows]], and [[29-Operating-System-Vulnerabilities|OS vulnerabilities]]** — hardware-level compromises make those easier.

---
### Mitigation Strategies (Security+ keywords)

#### Firmware Hardening
- Keep UEFI/BIOS firmware updated
- Enable **Secure Boot**
- Enable **Measured Boot + TPM**
- Disable unused ports (USB, Thunderbolt, JTAG)

#### Supply Chain Security
- Procurement from trusted vendors
- Chain-of-custody
- Component validation
- Hardware attestation

#### Physical Security
- Locks, cages, tamper-evident seals
- Restrict access to server rooms
- Disable/lock external ports

#### Core Technological Controls
- **IOMMU** (blocks DMA attacks)
- **TPM** for key storage
- **Hardware root-of-trust**
- **Memory encryption** (AMD SME/ SEV, Intel TME)

#### Monitoring & Detection
- Firmware integrity checks (e.g., CHIPSEC, OS attestation)
- Behavior monitoring for side-channel anomalies
- Inventory management (detect counterfeit hardware)

---
# CompTIA Exam Triggers

If you see wording like:
- “Compromised firmware”
- “Modified BIOS/UEFI”
- “Side-channel timing leakage”
- “Spectre/Meltdown”
- “Unauthorized DMA access”
- “Malicious USB device”
- “Hardware implant”
- “Counterfeit network device”
- “Rowhammer attack”
- “Tampered motherboard”

→ The answer is **hardware vulnerability** (or specific variant).

Security+ wants you to know:
- **Firmware + boot chain vulnerabilities**
- **Side-channel concepts**
- **Supply chain hardware tampering**
- **DMA-based attacks**
- **USB-based malicious devices**

---
# How It Ties Back to Previous Topics

| Previous Topic                                  | Connection                                            |
| ----------------------------------------------- | ----------------------------------------------------- |
| **[[25-Memory-Injections\|Memory Injection]]**  | DMA attacks inject code directly into RAM             |
| **[[28-Malicious Updates\|Malicious Updates]]** | Applies to firmware updates too                       |
| **[[27-Race-Conditions\|Race Conditions]]**     | Hardware timing flaws enable side-channel attacks     |
| **[[26-Buffer-Overflows\|Buffer Overflows]]**   | Rowhammer causes bit flips that can simulate overflow |
| **[[01-Security-Controls\|Physical Controls]]** | Needed to stop hardware implants & port access        |
| **[[06-Zero-Trust\|Zero Trust]]**               | Hardware must be attested before trusted              |

Hardware compromise = **total loss of [[02-The-CIA-Triad#Integrity|integrity]]**.