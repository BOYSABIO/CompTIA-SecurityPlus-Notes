# Recovery Testing
Recovery testing falls under **Resiliency & Recovery** and focuses on:
- Verifying backup integrity
- Validating disaster recovery plans
- Ensuring business continuity
- Measuring recovery objectives (RTO / RPO)
	- **Recovery Time Objective (RTO):** This is the maximum amount of time it takes for the system or application to be restored after a failure or disaster.
	- **Recovery Point Objective (RPO):** This is the maximum amount of data that can be lost during a disaster or outage before the system or application needs to be restored from a backup.

This is about **confidence and validation**, not just documentation.

---
### Why Recovery Testing Exists
Many organizations:
- Create a DR plan (Disaster Recovery)
- Set RTO/RPO targets
- Configure backups
- Then… never test them

Security+ wants you to understand:
> An untested recovery plan is a failure waiting to happen.

Recovery testing ensures:
- Backups can actually be restored
- Recovery times meet business objectives
- Staff know their roles
- Processes are realistic

---
### Recovery Metrics (Must Be Solid Here)
You’ve seen these already — now they matter operationally.

| Metric                             | Meaning                      |
| ---------------------------------- | ---------------------------- |
| **RTO (Recovery Time Objective)**  | Maximum acceptable downtime  |
| **RPO (Recovery Point Objective)** | Maximum acceptable data loss |
| **MTTR**                           | Mean Time To Repair          |
| **MTBF**                           | Mean Time Between Failures   |

Recovery testing validates:
- Can we meet RTO?
- Can we meet RPO?

---
### Types of Recovery Testing (Very Testable Section)
Security+ expects you to recognize the **differences between test types**.
#### 3.1 Tabletop Exercise
- Discussion-based
- No systems touched
- Walk through the scenario

Purpose:
- Validate procedures
- Identify planning gaps

Low risk, low cost.

Exam clue:
> “Discussion-based review of DR plan” → Tabletop exercise

#### 3.2 Walkthrough / Simulation
- Simulated disaster scenario
- Some operational testing
- Still controlled

Purpose:
- Practice coordination
- Validate communication

#### 3.3 Parallel Test
- Systems fail over to backup
- Production system still running

Purpose:
- Validate backup systems
- No interruption to production

Exam clue:
> “Test backup systems without disrupting production” → Parallel test

#### 3.4 Full Interruption Test (Cutover Test)
- Production system is shut down
- Backup system takes over

Purpose:
- Real-world validation

Risk:
- Service disruption possible

Exam clue:
> “Completely shut down primary system for testing” → Full interruption

---
### Backup Testing (Closely Related)
Backups must be:
- Restorable
- Verified
- Complete
- Uncorrupted

Common failure:
- Backups exist but cannot be restored
- Keys lost
- Storage damaged
- Ransomware encrypted backup too

Security+ loves ransomware + backup scenarios.

---
### Recovery Testing in Cloud Environments
Cloud introduces:
- Cross-region failover
- Multi-AZ deployments
- Snapshot restoration
- Infrastructure as Code re-deployment

Testing may include:
- Simulating AZ failure
- Testing autoscaling during outage
- Validating replication

---
### Recovery vs Resiliency (Now Clearer)

| Resiliency        | Recovery          |
| ----------------- | ----------------- |
| Stay online       | Come back online  |
| Redundancy        | Restoration       |
| Failover          | Backup restore    |
| High availability | Disaster recovery |

Recovery testing validates:
- Disaster Recovery Plan (DRP)
- Business Continuity Plan (BCP)

---
### Recovery Testing & Compliance
Some regulations require:
- Annual DR testing
- Documented results
- Remediation tracking

Examples:
- Healthcare (HIPAA)
- Financial institutions
- Government contracts

---
### Common Exam Scenarios
Security+ might describe:
- Backup restores fail during a real incident
- RTO is not met during outage
- Secondary site fails under full load
- Staff unsure of recovery procedures

All point to:
> Insufficient recovery testing

---
### Risk Considerations
Testing must balance:
- Operational risk
- Business disruption
- Confidence in recovery

That’s why test types scale in risk:  
Tabletop → Parallel → Full interruption

---
### How Recovery Testing Connects to Previous Topics

| Previous Topic                                    | Connection                             |
| ------------------------------------------------- | -------------------------------------- |
| [[77-Resiliency\|Resiliency]]                     | Tests recovery after resiliency fails  |
| [[78-Capacity-Planning\|Capacity Planning]]       | Ensures backup systems can handle load |
| [[76-Protecting-Data\|Protecting Data]]           | Validates backups & encryption         |
| [[55-Cloud-Infrastructure\|Cloud Infrastructure]] | Tests cross-region failover            |
| Incident Response                                 | Recovery phase of IR lifecycle         |
| [[42-Other-Malware-Types\|Ransomware]]            | Offline backup validation critical     |

Recovery testing is the **proof phase** of your entire security architecture.