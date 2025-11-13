# Malicious Updates
A **malicious update attack** occurs when an attacker **modifies or impersonates legitimate software updates** so that users or systems install **malware or backdoors** under the guise of normal patching.

> In short: the attacker _poisons the patch._

This is a **[[20-Common-Threat-Vectors#Supply Chain & Third-Party Threats|supply chain–type]] threat vector** that specifically targets the **update or patch distribution process**.

---
### **How the Attack Works**

1. **Compromise the vendor or update server**  
	- Attacker gains access to a developer environment, build pipeline, or update server.
2. **Insert malicious code or payload** into legitimate software packages or update files.
3. **[[16-Hashing-&-Digital-Signatures#What Is A Digital Signature?|Sign]] (or mimic) the update** so it appears authentic to end users.
4. **Victims install** the “trusted” update, granting the attacker code execution inside trusted environments.
5. **Persistence and exfiltration** occur using the update’s legitimate privileges.

_Core link:_  
This is a **[[02-The-CIA-Triad#Integrity|data integrity]]** attack on the **software supply chain** and a **[[20-Common-Threat-Vectors|threat vector]]** that relies on **trust exploitation** — like a digital version of a [[23-Watering-Hole-Attacks|watering hole]], but for update mechanisms.

---
### **Real-World Examples**

| Attack                      | Description                                                                                                                  |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| **SolarWinds Orion (2020)** | Attackers inserted backdoor code (“SUNBURST”) into legitimate Orion software updates, signed by SolarWinds’ own certificate. |
| **CCleaner (2017)**         | Legitimate installer replaced with malicious version distributed from the official server.                                   |
| **NotPetya (2017)**         | Fake update from Ukrainian accounting software “MeDoc” delivered destructive malware.                                        |

All show how attackers **exploit trust** in _authentic vendors or update channels._

---
### **What It Targets in the CIA Triad**

| CIA Component                                             | Impact                                           |
| --------------------------------------------------------- | ------------------------------------------------ |
| **[[02-The-CIA-Triad#Integrity\|Integrity]]**             | Code modified without detection.                 |
| **[[02-The-CIA-Triad#Confidentiality\|Confidentiality]]** | Malware exfiltrates sensitive data.              |
| **[[02-The-CIA-Triad#Availability\|Availability]]**       | May disable or corrupt systems (e.g., NotPetya). |

---
### **Attack Surface in the Update Process**

|Phase|Weak Point|Example Exploit|
|---|---|---|
|**Development**|Compromised source code repository|Attacker commits malicious code under false credentials|
|**Build/Compile**|Compromised build server|Payload inserted post-compile|
|**Signing/Distribution**|Stolen or misused signing certificate|Fake “trusted” update|
|**Client Update**|Unverified download or insecure channel|MITM replaces file in transit|

_Relates back to [[09-Change-Management|change management]] & version control:_ The update process should include **integrity validation** and **change approval** — the same principle you learned in **Technical Change Management**.

---
### **Mitigation Strategies**

| Level            | Control                                                                   | Description                                             |
| ---------------- | ------------------------------------------------------------------------- | ------------------------------------------------------- |
| **Development**  | Code review, CI/CD security, signed commits                               | Detect unauthorized code changes                        |
| **Distribution** | **Digital signatures**, **code signing**, **hash verification (SHA-256)** | Ensure [[03-Non-repudiation\|authenticity]] & integrity |
| **Network**      | TLS/HTTPS for update delivery                                             | Prevent tampering in transit                            |
| **Endpoint**     | Application whitelisting, EDR scanning updates                            | Block unknown binaries                                  |
| **Operational**  | Vendor vetting, supply-chain audits                                       | Reduce exposure to untrusted sources                    |
| **Policy**       | Verify updates only from trusted repositories                             | Administrative safeguard                                |

_Exam keywords:_ “Validate digital signatures,” “verify file hashes,” “[[06-Zero-Trust|signed updates only]].”

---
### **Related Concepts**

| Related Topic                                                                          | Relationship                                                |
| -------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| **Supply Chain Attack**                                                                | Broader category that includes malicious updates.           |
| **Code Signing Certificates**                                                          | Prevent tampering; should be securely stored.               |
| **[[16-Hashing-&-Digital-Signatures#What Is Hashing?\|Hashing]] / Integrity Checking** | Used to verify updates haven’t been modified.               |
| **[[06-Zero-Trust#Zero Trust (Architecture)\|Zero-Trust]] Architecture**               | Validates every connection and update regardless of source. |
| **Change Management**                                                                  | Ensures authorized updates follow proper approval paths.    |

---
### **Detection & Response**
- **File integrity monitoring (FIM):** Detect unexpected changes in binaries.
- **Log correlation:** Unusual outbound traffic after update installation.
- **Threat intelligence feeds:** Alert on known compromised update versions.
- **Revocation:** Vendor should revoke malicious certificates and issue new versions.
- **Forensics:** Compare hash of installed software to official vendor release.