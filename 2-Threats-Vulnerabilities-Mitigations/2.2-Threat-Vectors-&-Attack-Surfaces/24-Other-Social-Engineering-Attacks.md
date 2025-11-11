# Other Social Engineering Attacks
[[20-Common-Threat-Vectors#Email and Social Engineering|Social Engineering]] is a **psychological manipulation** used by attackers to trick people into giving access, information, or performing actions that compromise security

*Instead of hacking systems, they hack **human trust and behavior***

This topic expands beyond fishing and impersonation into tactics, psychological levers, and real-world scenarios that exploit human nature - curiosity, fear, urgency, or helpfulness

---
### How It Connects Back
- [[20-Common-Threat-Vectors#Common Threat Vectors|Threat vector]] - Human interaction (vs. technical exploitation)
- [[01-Security-Controls#Control Types by Function|Control Type]] - Administrative (training, verification) and technical (MFA policy enforcement)
- [[02-The-CIA-Triad#The CIA Triad|CIA Focus]] - Mainly **confidentiality** (stealing secrets) and **integrity** (tricking procedures)
- **Foundation tie-in** - Supports your understanding of control types (human vs technical) and risk management (social risks are harder to quantify)
---
### Key Social Engineering Techniques
| Technique                 | Description                                                                         | Example                                                |
| ------------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------------------ |
| Pretexting                | Creating a believable story (pretext) to justify a request                          | Pretending to be a security auditor needing log files  |
| Tailgating / Piggybacking | Physically following someone into a secure area without authorization               | Attacker follows employee through a locked door        |
| Shoulder Surfing          | Observing someone's screen or keyboard to capture credentials                       | Watching someone type a password or PIN                |
| Dumpster Diving           | Retrieving sensitive information from discarded materials                           | Searching trash for printouts or notes with passwords  |
| Eliciting Information     | Subtly manipulating someone to disclose information through conversation            | Oh, what's your Wi-Fi SSID again?                      |
| Hoaxes                    | False information designed to create panic or manipulate behaviour                  | Security alert: you must install this urgent patch     |
| Baiting                   | Offering something enticing to trick the victim                                     | Free USB drive labeled "Employee Salaries 2025"        |
| Quid Pro Quo              | Exchange of something (real or fake) for information or access                      | "IT support" offers help in exchange for login details |
| Influence Campaigns       | Coordinated misinformation using social media to manipulate perception or decisions | Fake news campaigns, bot networks, deepfakes           |
[[21-Phishing|Phishing]] is the delivery method, but these are the psychological or procedural tactics used to exploit people.

---
### Deeper Dive On Common Ones
#### Pretexting
- The attacker builds a **false scenario** to justify interaction or request
- Often paired with **impersonation** ("I'm from corporate IT, we're updating systems)
- Can be **in-person, over phone or online**

Breaks [[04-Authentication-Authorization-&-Accounting#Authentication - Verifying Identity|authentication]] by convincing a person to override identity checks
Relates to [[01-Security-Controls#Control Implementation Types (How they're applied)|administrative controls]] - verify requests, require callback numbers

#### Tailgating / Piggybacking
- **Tailgating**: Attacker slips in behind someone without their consent
- **Piggybacking**: Authorized user knowingly holds the door open 

Physical - mitigated by mantraps, badge readers, guards
Supports [[02-The-CIA-Triad#Availability|availability]] by maintaining facility integrity

#### Shoulder Surfing
- Observing screens, keyboards, or printed materials
- Can be done directly, or remotely via cameras / binoculars

Privacy filters, workstation positioning, awareness training can all help to prevent

#### Dumpster Diving
- Collecting discarded info from trash (paper or media)
- Common finds: passwords, phone lists, old drives, printed logs

Physical control - shredders, locked disposal bins, data destruction policies

#### Eliciting Information
- Subtle conversational extraction - asking leading questions without arousing suspicion
- Common in [[23-Watering-Hole-Attacks#The Attack Chain|reconnaissance]] or [[21-Phishing#Common Types Of Phishing|spear phishing]] setups

Awareness training + principle of least information disclosure

#### Hoaxes
- False warnings or fake alerts that manipulate users to take harmful actions
- Often lead to installing malware or deleting critical files

Targets **availability** (e.g., trick users into disabling systems) and **integrity** (fake data or updates)

#### Baiting
- Uses curiosity or greed to lure users
- Example: infected USB drives, fake movie downloads, or "free" tools

[[20-Common-Threat-Vectors#Removable Media|Removable media threat vector]] (physical + social engineering hybrid)
Mitigate with auto-run, disabled, user awareness, and policy enforcement

#### Quid Pro Quo (Something for Something)
- Attackers promise a benefit or reward in exchange for sensitive info
- Common variant: Fake IT support offering "help" to fix an issue

Similar to phishing, but interaction-based attacker offers value not fear

#### Influence Campaigns
- Large scale social engineering targeting populations, not individuals
- Goal: manipulate beliefs, behavior, or decisions (often political or financial)
- Tools: Fake accounts, misinformation, deepfakes, botnets

---

### Psychological Principles Behind Social Engineering
This appears in many CompTIA questions - you'll see them in the phrasing ("the attacker used urgency and authority...")

| Principle                | Description                                    | Example                                           |
| ------------------------ | ---------------------------------------------- | ------------------------------------------------- |
| Authority                | Pretending to be someone in power              | This is the CEO - do it now                       |
| Intimidation             | Threatening consequences for non-compliance    | If you don't reset this password, you'll be fired |
| Consensus / Social Proof | Everyone else has done this                    | All employees must revalidate their credentials   |
| Scarcity                 | Creates FOMO or limited time offers            | Last chance to secure your account                |
| Urgancy                  | Forces quick, emotional reactions              | You have 30 min to act                            |
| Familiarity / Liking     | Building rapport or shared interests           | Oh, you went to stanford too                      |
| Trust                    | Implicit faith in brand, colleague, or process | Using company logos or real names                 |
Human behavior risk = administrative control, training, and procedural enforcement

---
### Mitigation & Prevention
| Control Type      | Example                                              | Goal                                |
| ----------------- | ---------------------------------------------------- | ----------------------------------- |
| Technical         | Spam filters, link protection, disable USB autorun   | Reduce exposure                     |
| Administrative    | Security awareness training, verification procedures | Reduce human error                  |
| Physical          | Mantraps, cameras, badge policies                    | Stop tailgating and dumpster diving |
| Incident response | Reporting suspected social engineering attempts      | Early detection                     |
Defense against social engineering primarily relies on **people and processes**, not just technology.