# Change Management
**Change management** is the formal process used to **plan, test, document, and approve** any changes to systems, networks, applications, or configurations.

"Don't make changes randomly - make them safely, predictably, and with accountability"

It ensures `availability`, `security`, and `stability` aren't accidentally compromised by well-intentioned updates.

Changes are one of the most common risks in enterprise. You can have thousands of applications all with different updates etc. Many organizations already have a policy with respect to change management making it easy but without one, it is very difficult to implement or make any changes.

---

### Why Change Management Matters
- Prevents **unplanned downtime**
- Avoids **configuration drift** (systems deviating from standard baselines)
- Creates `accountability` (who changed what, when, and why)
- Helps detect **unauthorized or malicious changes**
- Supports **auditability** and **compliance**

Many security incidents are caused not by attackers but by poorly managed internal changes (usually people).

---

### Core Steps In The Change Management Process
Main idea is to avoid downtime, confusion, and mistakes. 

You'll see some slight variations but the main stages are:

| Step | Description | Example | 
| --- | --- | --- | 
| Request / Initiation | Someone proposes a change (in the form of a form). The reason for the change | Admin requests firmware update for routers | 
| Impact Analysis / Risk Assessment | Determine what could go wrong or the scope of the change. Including a Scheduling process. Risk also is important. | Will this affect connectivity or users? | 
| Approval / Authorization | **The Change Advisory Board (CAB)** or management reviews and approves | **CAB** approves weekend maintenance window | 
| Testing / Validation | Test the change in a **sandbox** or **lab** first or users testing it. | Try update on test router before production | 
| Implementation | Apply the approved change during the scheduled window | Perform firmware update on all routers |
| Documentation / Review / Backout Plan | Record results and update documentation. Include a **rollback plan** just incase of failure | Document success; if failure - restore previous config |

This process usually starts with the owner of the application or data wanting to make a change to that application or data. These people don't generally control the change management process and are not usually making the actual change. Instead the owners are the one's managing the process. The change is made and then these owners are responsible for testing afterwards.

ALWAYS HAVE A BACKOUT / ROLLBACK PLAN. You can also test this in the sandbox so you can document everything on a duplicate system and know that the rollback would work too.

---

### Key Components of Change Management
| Component | Description |
| --- | --- | 
| Change Request | The formal record that starts the process. Includes description, reason, risk, and who's responsible |
| Change Advisory Board (CAB) | Group that reviews, prioritizes, and approves changes | 
| Maintenance Window | Pre-approved time slot for performing changes with minimal disruption (This is one of the hardest things to find time for or get approved) |
| Backout / Rollback Plan | Procedure for reverting to the previous state if the change fails | 
| Version Control | Tracks configuration and software versions to identify when a change occurred |
| Notification / Communication Plan | Alerts users and teams affected by the change before it happens | 

Stakeholders are also important. There are changes that can affect a large number of people in the organization. You need to research and identify who would be affected. One change can affect many appartments or functions because if there is downtime or a change in data, then it trickles down the whole line of value.

---

### Types Of Changes
| Type | Description | Example | 
| --- | --- | --- | 
| Standard Change | Pre-approved, low-risk, routine | Adding new user accounts, applying known updates | 
| Emergancy Change | Needs immediate action to fix a critical issue | Patching an actively exploited vulnerability | 
| Major Change | High-impact or complex, needs full CAB review | Migrating servers or replacing network core switches | 

Every change has a level of risk associated with it. Might be a risk value of low, medium or high. Risk could also be far-reaching. There is the risk that you don't actually fix anything or that it breaks something else, operating systems fail, data corruption.

It's also really important to highlight the risks of **NOT** making the change. 

Emergancy Changes still require documentation afterward - even if implemented quickly

--- 

### Best Practices And Security Implications
- **Segregation of Duties**: different people request, approve, and implement
- **Baseline Configurations**: compare post-change state to baseline to detect unauthorized changes
- **Change Tracking Tools**: use ticketing or configuration management systems (e.g., ServiceNow, Jira, Ansible, Git)
- **Notifications**: communicate to users before and after the change
- **Post-implementation review**: verify success and ensure no new vulnerabilities were introduced

---

### Change Management vs Configuration Management
| Aspect | Change Management | Configuration Management |
| --- | --- | --- |
| Focus | Managing the process of change | Maintaining consistency of system configurations |
| Scope | Procedural / organizational | Technical / system-level | 
| Example | Approving a server upgrade | Tracking version of OS and patch level |

They work together - configuration management records what changed; change management controls how it's changed.

---

### Connection To Security+
Change management supports:
- `Availability` - prevents outages
- `Integrity` - ensures approved, tested changes only
- `Accountability` - clear audit trails
- `Non-repudiation` - proof of who authorized / implemented a change

---

## Related Notes
- [[10-Technical-Change-Management]]
- [[05-Gap-Analysis]]
- [[36-Misconfiguration-Vulnerabilities]]
