# Security Controls
*Security controls are the safeguards or countermeasures used to reduce risk to an acceptable level. They protect confidentiality, integrity, and availability (CIA) of data and systems.*
  
It's important to understand that it is the protection of both physical and virtual. It usually boils down to `data`, `physical property`, and `computer systems`.
  
**Prevent** security events, **Minimize the impact**, and **Limit** the damage.
  
The CIA Triad  
1. Confidentiality: Prevent unauthorized access (eg. encryption, access controls)
2. Integrity: Ensure data accuracy and trustworthiness (eg. hashing, digital signiture)
3. Availability: Ensure systems are up and running (eg. backups, redundancy)

---

### Control Types by Function
*There are three main functional categories of controls*

| Type | Purpose | Examples |
| --- | --- | --- |
| Preventive | Stop an attack before it happens. (Limit access to a certain resource) | Firewall role, strong passwords, training, locks |
| Detective | Identify or alert to an attack in progress or after. Warning and log information | IDS, audit logs, CCTV, file integrity monitoring |
| Corrective | Fix or mitigate issues after detection. Reverse the impact (sometimes) or operate with minimal downtime. | Patching, backup restoration, reimaging systems | 
| Deterrent | Something that aims to deter a possible attack | Application splash screen, front desk reception, posted warning signs | 
| Compensating | Security event occurred but you don't have the resources to reverse it. | Use other means (temporary basis). Firewall blocks of specific applications, seperation of duties, more guards. |
| Directive | Weak signal. You direct someone to do something more secure. | Require everyone to store sensitive info on protected encrypted folder. (Users have to decide which data is considered risk or not)

Also sometimes you'll see *Deterrent* (Discourage attacks) and *Compensating* (temporary or alternative control).

---

### Control Implementation Types (How they're applied)
*These describe how controls are implemented*

| Type | Description | Examples |
| --- | --- | --- | 
| Administrative (Managerial) | Policies, procedures, training (best way to manage computer, data or other) | Security policies, background checks, onboarding rules |
| Technical (Logical) | Technology-based controls. Using some type of technical system. | Firewalls, encryption, antivirus, access controls |
| Physical (Operational) | Protect the physical environment. Use people instead of systems to set controls. (Security guards or posters / awareness) | Fences, locks, guards, surveillance cameras | 

---

### Control Frameworks
You'll see references to frameworks that standardize controls, like:
- `NIST SP 800-53` - Federal control catalog
- `ISO/IEC 27001` - Global standard for information security management systems
- `CIS Controls` - Practical prioritized controls for enterprises

You don't need to memorize all, but know why they exist - to organize and implement controls systematically.

---

### Risk and Controls Relationship
- `Risk = Threat x Vulnerability x Impact`
- Security controls are applied to reduce vulnerabilities or minimize impact
- Controls can be proactive (preventive) or reactive (detective/corrective)

---

### Control Type Table
| Categories | Preventive | Deterrent | Detective | Corrective | Compensating | Directive |
| --- | --- | --- | --- | --- | --- | --- |
| Technical | Firewall | Splash Screen | System Logs | Backup Recovery | Block instead of Patch | File Storage Policies |
| Managerial | On-boarding Policy | Demotion Risk | Review Login Reports | Policies for Reporting Issues | Seperation of Duties | Compliance Policies |
| Operational (By Person) | Guard Shack | Reception Desk | Property Patrol | Contact Authorities | Require multiple Security Staff | Security Policy Training |
| Physical | Door Lock | Warning Signs | Motion Detectors | Fire Extinguisher | Power Generator | Sign: Authorized Personnel Only |
  
There are many categories of control and different security controls that fit into different categories.

---

## Related Notes
- [[02-The-CIA-Triad]]
- [[04-Authentication-Authorization-&-Accounting]]
- [[53-Mitigation-Techniques]]
- [[54-Hardening-Techniques]]
