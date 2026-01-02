Solution Architecture case study for a greenfield manufacturing IT infrastructure (IT, OT, CCTV)
# 🏭 Greenfield IT Infrastructure Architecture – Manufacturing Plant  
**Portfolio | Solution Architecture Case Study**

**Author:** Khalid Zamil  
**Role:** Solution Architect *(End-to-End Ownership)*  
**Project Type:** Greenfield Manufacturing Infrastructure  
**Confidentiality:** High-level design shared for portfolio purposes only

---

## 1. Business Context & Problem Statement
IDVB Recycling required a **secure, scalable, and audit-ready IT foundation** to enable go-live of a new manufacturing plant in Odisha.

### Key Challenges
- Zero existing IT/OT/CCTV infrastructure (Greenfield environment)
- Critical dependency on OT and CCTV for plant operations
- Mandatory **segregation between IT, OT & CCTV networks**
- Secure **physical access control for critical rooms and plant entry**
- Enterprise-grade collaboration & communication required
- **Fixed capital budget** with a strict plant go-live deadline

### Business Impact of Failure
- Delay in plant commissioning
- OT/CCTV operational disruption
- Increased cyber & physical security risk
- Audit non-compliance exposure

---

## 2. Architectural Principles Enforced
| Principle | Implementation Approach |
|---|---|
| Network segregation over convergence | 3 isolated networks (IT / OT / CCTV) routed only via firewalls |
| Defense-in-depth | Firewalls, MFA, MDR, VMDR + physical access governance |
| High availability | Redundant ISP, Firewall HA, Core switching, Virtualization hosts |
| Operational simplicity | Traditional virtualization selected over HCI |
| On-prem + cloud augmentation | Local workloads with immutable cloud backup copy |

---

## 3. Project Constraints & Their Impact
| Constraint | Impact |
|---|---|
| Budget cap ~USD 3.94M | Cost-optimized design mandatory |
| Greenfield site | Dependent on passive infra readiness |
| Hardware supply delays | Go-live schedule risk |
| OT security sensitivity | Zero IT/OT convergence allowed |
| Limited local IT skillset | Design had to be operable, not exotic |
| Compliance & audit | Mandatory logical + physical controls |

---

## 4. Architecture Options Evaluated
### ❌ Option A – HCI (Hyper-Converged)
**Rejected due to:**
- Higher capital cost
- Vendor lock-in risk
- Skill dependency
- Over-complex for workload size

### ❌ Option B – Cloud-First
**Rejected due to:**
- OT & CCTV latency sensitivity
- WAN dependency risk for plant operations
- Local data governance considerations

### ✅ Option C – Traditional Virtualization + External Storage  
**Selected for:**
- Predictable cost
- Compute–storage separation
- Easier troubleshooting & scaling
- Vendor flexibility

**Accepted Trade-off:** Higher operational effort for lower CapEx and long-term control.

---

## 5. Final Architecture Overview
### 5.1 Network Segmentation
- **IT Network:** Enterprise apps, users, identity, security, VC, telephony
- **OT Network:** SCADA, PLC, OT user workstations
- **CCTV Network:** IP cameras, NVRs, surveillance workloads

**No network convergence.**  
Inter-network access permitted only through **firewall policy governance.**

---

## 6. IT Infrastructure Stack
### Core & Perimeter
- 2× **ISPs (Redundant)**
- 2× **Palo Alto Firewalls (HA)**
- 2× **Core Switches**
- Access switching + Wireless for ~400 users

### Compute & Virtualization
- 2× **HPE ProLiant DL380 Gen10**
- **Hyper-V on Windows Server Datacenter**
- 12 Virtual Machines (6 Infra + 6 Production)

### Identity & Cybersecurity
- On-Prem: **Active Directory, DNS**
- Hybrid Identity via **IPSec VPN to Entra ID**
- **RADIUS authentication** for network access
- **Cisco Duo MFA**
- **Sophos MDR** (Endpoints)
- **Qualys VMDR** (Vulnerability & risk posture)

---

## 7. Storage & Backup Design
- **HPE MSA 2060 iSCSI Storage** *(9 TB usable)*
- Storage segmented into performance-aligned pools
- **Commvault Backup Architecture**
  - 1× CommServe
  - 1× Media Agent (On-Prem)
  - 14-day Local backup retention
  - 28-day **immutable cloud copy**
  - **Air-gap protection enabled**

---

## 8. Recovery Objectives (Aligned to Business Tolerance)
| Workload Tier | RPO | RTO |
|---|---|---|
| Infrastructure (AD, DNS, Auth, Mgmt) | ≤ 24 hrs | ≤ 4 hrs |
| Production IT Apps | ≤ 24 hrs | ≤ 8 hrs |
| Collaboration & Telephony | ≤ 24 hrs | ≤ 4 hrs |
| OT Systems | Not backed up | Site-level DR only |
| CCTV | Recording continuity | Manual restore accepted |

*Balanced to meet resilience goals without over-engineering.*

---

## 9. Risk Register & Mitigation
| Risk | Impact | Mitigation |
|---|---|---|
| Hardware delivery delays | Go-live risk | Distributor switch & escalation |
| Passive infra dependency | Schedule risk | Joint execution planning |
| Vendor skill gaps | Quality risk | Internal SME governance |
| Documentation gaps | Audit exposure | Architect-led HLD/LLD ownership |
| Cyber threats | Business outage | MFA, MDR, immutable backups |

---

## 10. Financial Governance & Variance Control
- **Approved Budget:** ~USD 3.94M  
- **Final Spend:** ~USD 4.03M  
- **Variance:** **2.3% (controlled & justified)**

---

## 11. Business Outcomes Delivered
- On-time manufacturing IT go-live
- Zero IT/OT/CCTV blast-radius risk
- Audit-ready infrastructure from Day 1
- Strong cyber + physical security posture
- Scalable for future plant expansion
- Improved leadership collaboration & vendor coordination

---

## 12. Future Improvements (If Constraints Changed)
### If Budget Increased by 30%
- Dedicated DR site
- Additional Hyper-V node
- Faster storage tiering
- Advanced SIEM integration

### If Budget Reduced by 30%
- Reduced backup retention
- Phased VC rollout
- Higher RTO acceptance

---

## 🧠 Architect’s Summary
This case study demonstrates **end-to-end solution architecture ownership** across:

- Business risk alignment  
- Secure network segregation  
- Virtualization + SAN design  
- Cyber + physical security governance  
- Recovery planning  
- Vendor and financial accountability  

*Designed within constraints, governed through risk-aware decision making, delivered with ownership.*

---

## Scope Clarification
- This is a **High-Level Design (HLD) view only**
- **LLD configurations and credentials are excluded intentionally**
- Vendor names are mentioned only where relevant to architectural decision traceability

---

## Author Note
This portfolio reflects **real-world architectural decision-making and ownership**, intended to demonstrate **Solution Architecture capability**, not provide implementation-level guidance.

---

⭐ *If you found this useful, explore the full portfolio repository for additional case studies and architecture diagrams.*
