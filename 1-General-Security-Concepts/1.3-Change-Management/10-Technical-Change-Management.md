# Technical Change Management
**Technical Change Management** is the process of **applying, tracking, and validating changes to systems, software, and configurations** using technical tools and procedures.

It's the *implementation* side of the broader change management policy.

Change management = policy and approval

Technical change management = execution and verification

---

### Goals
- Maintain **stability** and `availability` while implementing updates
- Ensure **tracability** - you know *who* changed *what* and *when*
- Prevent **unauthorized or unintended changes**
- Allow **rollback** or **recovery** if something fails

---

### Core Elements of Technical Change Management
| Element | Description | Example | 
| --- | --- | --- | 
| Configuration Baselines | Known good, approved system configurations. Used as a reference point | Baseline windows 11 image with approved apps |
| Version Control | Tracks changes to configuration files or code | Git, Ansible, or network configuration backups | 
| Testing and Validation | Run changes in lab or sandbox before production | Try patch or firmware update on test VM |
| Implementation Plan | Step-by-step technical guide for deployment | List of commands, order of systems, verification steps |
| Rollback Plan | Technical steps to revert a change | Revert snapshot, restore config, reload previous firmware |
| Monitoring / Verification | Ensure change succeeded and didn't break anything | Log review, performance monitoring, automated tests |

---

### Examples of Technical Changes
- OS or firmware updates
- Firewall rule modifcations
- Network reconfigurations (VLANs, ACLs, routing changes)
- Database schema updates
- Software version upgrades
- Certificate renewals
- Cloud infrustructure updates (new instances, IAM policy changes)

Security+ expects you to recognize that these all require planning, documentation, and rollback capability - not just doing them live.

---

### Technical Tools Used In Change Management 
| Tool / System | Purpose |
| --- | --- |
| Configuration Management Tools | Automate and track system states. Examples: Ansible, Puppet, Chef, SaltStack |
| Version Control Systems | Track file or code changes with commits. Example: GitHub |
| Automated Deployment Tools | Apply tested updates consistently across environments. Example: CI/CD pipelines, SCCM, Intune, Jenkins |
| Ticketing / Workflow Systems | Manage approvals and documentation. Example: ServiceNow, Jira, Remedy. |
| Monitoring Tools | Verify changes and catch anomolies. Example: Nagios, Splunk, SolarWinds |

**Automation** and **Versioning** are KEY THEMES here - they minimize human error and create audit trails.

---

### Change Validation
After implementation, **Validation** ensures:
- The system behaves as expected
- There's no unintended side effect
- Logs and monitoring show normal operation

Common validation methods:
- Automated tests or scripts
- Log reviews
- Baseline comparison (before/after snapshots)
- User acceptance testing (UAT)

---

### Rollback & Recovery
A rollback plan ensures that if a change goes wrong, you can revert quickly to a known stable state.


| Rollback Type | Description | Example |
| --- | --- | --- | 
| Manual Rollback | Admin restores configuration or image manually | Copy old config file back to router | 
| Automated Rollback | System detects failure and reverts automatically | Cloud deployment pipeline reverts to last version | 
| Snapshot Reversion | VM or container snapshot restored | Revert to pre-patch snapshot |

*An update caused system instability. What should the admin do next?*: **Initiate the rollback plan**

---

### Documentation and Recordkeeping
Every technical change should record:
- Who made it
- When it occurred
- What was changed
- Why the change was made
- Verification results

This supports `accountability`, **auditing**, and **non-repudiation** - all key security goals

---

### Security & Risk Implications
Poorly managed technical changes can cause:
- **Outages** (`availability` impact)
- **Configuration Drift** (inconsistency across systems)
- **Security Gaps** (e.g. accidental ACL misconfigurations)
- **Data Integrity Issues** (e.g. DB updates gone wrong)

Proper technical change management **minimizes risk** by enforcing:
- Testing
- Version Control
- Rollback Capability
- Documentation

---

### Technical Change Management In Action
1. **Request**: Admin submits request to update firewall firmware
2. **Approval**: CAB reviews risk and approves
3. **Testing**: Test update in lab firewall
4. **Implementation**: Apply update in production during maintenance window
5. **Verification**: Monitor traffic logs and performance
6. **Rollback**: Revert to previous firmware if instability is detected 
7. **Documentation**: Record version, time, and results in change log

---

---

## Related Notes
- [[09-Change-Management]]
- [[28-Malicious Updates]]
- [[53-Mitigation-Techniques]]
