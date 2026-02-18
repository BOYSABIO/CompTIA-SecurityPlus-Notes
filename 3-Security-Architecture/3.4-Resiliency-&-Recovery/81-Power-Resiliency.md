# Power Resiliency
This topic is about ensuring systems remain operational despite **power disruptions**.  
It directly ties to:
- CIA triad → [[02-The-CIA-Triad#Availability|Availability]]
- Infrastructure considerations
- Resiliency
- Disaster recovery
- Capacity planning

---
### Why Power Resiliency Is a Security Topic
Power loss causes:
- System crashes
- Data corruption
- Service outages
- Hardware damage
- Lost transactions

Security+ treats availability failures as security failures.

Power resiliency ensures:
> Systems continue running or shut down safely during power disruptions.

---
### Types of Power Issues (Know These)
Security+ may describe a problem rather than naming it.
#### Brownout
- Temporary drop in voltage
- Systems may malfunction but not fully shut down

#### Blackout
- Complete power loss

#### Surge
- Sudden voltage spike
- Can damage equipment

#### Spike
- Very short, sharp voltage increase

#### Sag
- Short drop in voltage

Exam pattern:  
If hardware damage occurs → likely surge/spike  
If system instability → brownout/sag  
If complete shutdown → blackout

---
### Core Power Resiliency Controls
#### 3.1 UPS (Uninterruptible Power Supply)
Provides:
- Short-term battery power
- Clean, conditioned power
- Protection from surges and brownouts

Purpose:
- Graceful shutdown
- Maintain uptime until generator activates

Exam trigger:
> “Provide temporary power during outage” → UPS

#### 3.2 Backup Generators
Provide:
- Long-term power during outages
- Used in data centers

Often paired with:
- Automatic transfer switches (ATS)

Exam trigger:
> “Maintain operations during extended outage” → Generator

#### 3.3 Dual Power Supplies
Servers may have:
- Two independent power supplies
- Connected to separate circuits

Purpose:
- Eliminate single point of failure

Exam trigger:
> “Redundant power source within server” → Dual power supply

#### 3.4 Power Distribution Units (PDUs)
- Distribute electrical power within racks
- Can include monitoring

Not a backup power source — just distribution.

---
###  Clean Power & Conditioning
UPS devices also provide:
- Voltage regulation
- Surge suppression
- Noise filtering

This protects:
- Sensitive hardware
- Network appliances
- Storage systems

---
### Power Resiliency in Data Centers
Enterprise environments use layered protection:
1. Utility power
2. UPS
3. Generator
4. Redundant circuits
5. Dual power supplies

This aligns with:
> Defense in depth — but for power systems.
---
### Cloud Power Resiliency
Cloud providers:
- Use multiple power grids
- Redundant UPS systems
- Multiple generators
- Separate Availability Zones

Security+ expects you to understand:
> Multi-AZ deployments protect against facility-level power loss.
---
### Power Resiliency vs Backup Strategy
Important distinction:

| Control       | Purpose               |
| ------------- | --------------------- |
| UPS           | Short-term continuity |
| Generator     | Long-term continuity  |
| Backups       | Data restoration      |
| Failover site | Service continuity    |

Power resiliency prevents downtime.  
Backups restore after downtime.

---
### Common Exam Scenarios
Security+ may describe:
- Systems abruptly shutting down → no UPS
- Data corruption after outage → no graceful shutdown
- Server remains online during short outage → UPS functioning
- Data center operational during city-wide outage → generator

---
### Power Resiliency & Availability (CIA)
This topic reinforces:
Availability depends on:
- Redundant hardware
- Redundant power
- Environmental controls
- Capacity planning

Power resiliency is foundational infrastructure security.

---
### How This Connects to Previous Topics

| Topic                                                               | Connection                             |
| ------------------------------------------------------------------- | -------------------------------------- |
| [[77-Resiliency\|Resiliency]]                                       | Eliminates single point of failure     |
| [[78-Capacity-Planning\|Capacity Planning]]                         | Power infrastructure must support load |
| [[80-Backups\|Backups]]                                             | Prevent corruption during outage       |
| [[58-Infrastructure-Considerations\|Infrastructure Considerations]] | HVAC + power tied together             |
| [[59-Secure-Infrastructure\|Secure Infrastructure]]                 | Physical layer support                 |
| Disaster Recovery                                                   | Power outages trigger DR events        |

Power resiliency supports everything above it.