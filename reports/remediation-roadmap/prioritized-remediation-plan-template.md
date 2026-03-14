# Prioritized Remediation Plan
**Client:** [Client Name]
**Date:** [Date]
**Version:** [1.0]
**Prepared by:** [Consultant Name / Firm Name]
**Classification:** CONFIDENTIAL

---

> **CONFIDENTIALITY NOTICE**
> This document contains sensitive security information about [Client Name]'s environment and remediation strategy. It is intended solely for authorized personnel. Distribution outside of the designated review team requires written approval from [Client Name]'s [CISO / IT Director / Designated Owner].

---

## Overview and How to Use This Document

This Prioritized Remediation Plan translates the findings from the **Technical Security Findings Report ([Report Date])** into a structured, actionable roadmap for [Client Name]'s IT and security team. It is designed to answer three questions clearly:

1. **What needs to be fixed?** — All identified findings, organized by CIS Control and priority.
2. **In what order?** — A prioritization framework that weighs severity, exploitability, business impact, and effort.
3. **By when?** — A phased 90-day roadmap with target dates and ownership.

**How to use this document:**

- **IT / Security Team:** Use the Master Remediation Table and CIS Control subsections to plan and execute remediation tasks. Update the Status column as items are completed.
- **IT Management:** Use the 90-Day Roadmap and Progress Tracking section to monitor progress and report upward.
- **Executive Leadership:** Refer to the companion **Executive Security Risk Report** for a business-level summary.

This document should be reviewed in weekly remediation status meetings and updated at minimum monthly. The consultant should be notified when findings are remediated so verification testing can be scheduled.

---

## Remediation Priority Framework

Each finding is assigned a **Priority Score** using the following formula, evaluated by the assessment team:

> **Priority Score = Severity Weight × Exploitability × Business Impact × (1 / Effort)**

### Scoring Dimensions

| Dimension | Scale | Description |
|---|---|---|
| **Severity Weight** | Critical=4, High=3, Medium=2, Low=1 | Based on CVSS v3.1 base score severity band |
| **Exploitability** | 1–3 | 1=Requires significant skill/access, 2=Moderate complexity, 3=Trivial/public exploit available |
| **Business Impact** | 1–3 | 1=Limited impact, 2=Significant disruption or data exposure, 3=Catastrophic (breach, ransomware, regulatory) |
| **Effort** | Low=1, Medium=2, High=3 | Relative effort to remediate — lower effort findings are prioritized higher when impact is equivalent |

Findings with the highest Priority Scores appear first in the Master Remediation Table. Where scores are equal, Critical severity findings are listed first, followed by items with the lowest effort estimate (quick wins).

---

## Risk Reduction Score

Each finding is also assigned a **Risk Reduction Score (1–10)**, representing the estimated reduction in overall organizational risk if the finding is remediated. This helps leadership understand which fixes deliver the greatest security return on investment.

| Score | Meaning |
|---|---|
| 9–10 | Remediating this finding significantly reduces the organization's most critical attack vectors. Highest possible impact on security posture. |
| 7–8 | High risk reduction — addresses a significant vulnerability or control gap with broad impact across systems or users. |
| 5–6 | Moderate risk reduction — closes an important gap, but impact is limited in scope or partially mitigated by other controls. |
| 3–4 | Low-moderate risk reduction — meaningful improvement, but finding is constrained in exploitability or business impact. |
| 1–2 | Minimal risk reduction — informational or low-severity finding; remediation improves hygiene but does not materially change risk posture. |

---

## Effort Estimate Legend

| Effort Level | Estimated Time | Description |
|---|---|---|
| **Low** | < 4 hours | Can be completed by a single administrator in a single session. Typically a configuration change, policy update, or single-system patch. |
| **Medium** | 4–40 hours | Requires planning, coordination, or work across multiple systems or teams. May require a maintenance window. |
| **High** | > 40 hours | Significant project effort. May require procurement, architectural changes, multi-team coordination, or phased rollout. |

---

## Master Remediation Table

*Organized by Priority Score (descending). Sort by CIS Control column to view grouped by control area.*

| Priority | Finding ID | Title | CIS Control | Severity | CVSS | Effort | Risk Reduction Score | Owner | Target Date | Status | Notes |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | FIND-003 | Default Credentials on Network Devices | CIS 4 | Critical | 9.1 | Low | 10 | [Network Admin Name] | [Date + 7 days] | Open | Immediate action required — management interface exposure |
| 2 | FIND-001 | Unpatched Critical Vulnerabilities on Internet-Facing Servers | CIS 7 | Critical | 9.8 | Medium | 10 | [Systems Admin Name] | [Date + 15 days] | Open | Exploits publicly available — schedule emergency patching |
| 3 | FIND-002 | MFA Not Enforced for Remote Access | CIS 6 | High | 8.1 | Medium | 9 | [IT Manager / IAM Owner] | [Date + 30 days] | Open | May require licensing — begin procurement immediately |
| 4 | FIND-007 | No Asset Inventory Process in Place | CIS 1 | High | 7.2 | Medium | 8 | [IT Manager Name] | [Date + 30 days] | Open | Foundational — blocks other remediation tracking |
| 5 | FIND-004 | Sensitive Data Transmitted Over Unencrypted Channels | CIS 3 | High | 7.5 | Medium | 8 | [App / Network Owner] | [Date + 30 days] | Open | Assess TLS 1.2/1.3 enforcement across all services |
| 6 | FIND-008 | Unauthorized Software Detected on Production Systems | CIS 2 | Medium | 6.5 | Low | 7 | [Systems Admin Name] | [Date + 30 days] | Open | Review software allowlist; remove unauthorized installs |
| 7 | FIND-005 | Excessive Privileged Account Permissions | CIS 5 | Medium | 6.3 | Medium | 7 | [Active Directory Admin] | [Date + 45 days] | Open | Conduct access review; enforce least privilege |
| 8 | FIND-009 | Security Event Logging Not Enabled on Critical Systems | CIS 8 | Medium | 5.9 | Medium | 7 | [SOC / IT Admin Name] | [Date + 45 days] | Open | Deploy log forwarding to SIEM; define retention policy |
| 9 | FIND-006 | Insecure Default Configurations on Workstations | CIS 4 | Medium | 5.5 | High | 6 | [Endpoint Admin Name] | [Date + 60 days] | Open | Deploy CIS Benchmark GPO baseline — phased rollout |
| 10 | FIND-010 | No Formal Vulnerability Scanning Program | CIS 7 | Medium | 5.0 | Medium | 8 | [Security Program Owner] | [Date + 60 days] | Open | Establish recurring scan schedule and SLA policy |

---

## CIS Control Sections

*The following sections group findings by CIS Control, explain why the control matters, and provide recommended sequencing for remediation.*

---

### CIS Control 1 — Inventory and Control of Enterprise Assets

**Why this control matters:** You cannot protect what you do not know exists. An accurate, continuously maintained asset inventory is the foundation of every other security control — patching, monitoring, access control, and incident response all depend on knowing what assets are in your environment. Unknown assets are frequently targeted by attackers precisely because they fall outside monitoring and maintenance cycles.

**Findings under this control:**

| Finding ID | Title | Severity | Status |
|---|---|---|---|
| FIND-007 | No Asset Inventory Process in Place | High | Open |

**Recommended approach and sequencing:**

1. Conduct an immediate network discovery scan across all known IP ranges to establish a baseline asset inventory.
2. Document all identified assets in a centralized asset management tool (options include: [e.g., Lansweeper, Snipe-IT, ServiceNow CMDB, or a maintained spreadsheet as a starting point]).
3. Define asset classification categories (e.g., critical, standard, decommissioned) and assign owners to each asset class.
4. Establish an automated discovery scan on a recurring schedule (weekly recommended) to identify new or unauthorized assets.
5. Integrate asset inventory with the vulnerability scanning program (FIND-010) to ensure all assets are included in scan scope.

---

### CIS Control 2 — Inventory and Control of Software Assets

**Why this control matters:** Unauthorized or unmanaged software on production systems introduces significant risk — it may contain unpatched vulnerabilities, exfiltrate data, provide backdoor access, or simply consume resources and complicate incident investigation. A software allowlist ensures only approved applications run in the environment.

**Findings under this control:**

| Finding ID | Title | Severity | Status |
|---|---|---|---|
| FIND-008 | Unauthorized Software Detected on Production Systems | Medium | Open |

**Recommended approach and sequencing:**

1. Review the list of unauthorized software identified during the assessment (detailed in FIND-008) and immediately remove or quarantine high-risk items (e.g., remote access tools, peer-to-peer applications, unapproved cloud sync clients).
2. Establish a software allowlist policy defining which applications are approved for use on corporate systems.
3. Implement technical enforcement via [e.g., Windows AppLocker, Microsoft Intune, or endpoint management tooling] to block execution of non-approved software.
4. Conduct a quarterly software audit against the allowlist.

---

### CIS Control 3 — Data Protection

**Why this control matters:** Protecting sensitive data — whether in transit or at rest — is both a core security obligation and a regulatory requirement under frameworks such as [HIPAA / PCI DSS / GDPR / applicable regulation]. Unencrypted data in transit is trivially intercepted on shared network segments and by any attacker who has gained a foothold in the environment.

**Findings under this control:**

| Finding ID | Title | Severity | Status |
|---|---|---|---|
| FIND-004 | Sensitive Data Transmitted Over Unencrypted Channels | High | Open |

**Recommended approach and sequencing:**

1. Identify all services and application interfaces transmitting data without encryption (list provided in FIND-004 evidence).
2. Enforce TLS 1.2 or TLS 1.3 for all web services, APIs, and database connections. Disable TLS 1.0 and 1.1.
3. Replace any use of unencrypted protocols (HTTP, FTP, Telnet, SNMPv1/v2) with encrypted equivalents (HTTPS, SFTP, SSH, SNMPv3).
4. Conduct a data classification exercise to identify where sensitive data resides and ensure encryption at rest is applied to data stores containing PII, financial data, or regulated information.
5. Implement certificate management processes to track TLS certificate expiry and prevent unplanned outages.

---

### CIS Control 4 — Secure Configuration of Enterprise Assets and Software

**Why this control matters:** Vendor default configurations are designed for ease of initial setup — not for security. Default credentials, enabled unnecessary services, and out-of-box settings are well known to attackers and are among the most frequently exploited issues in breach investigations. Establishing and enforcing a secure configuration baseline dramatically reduces the attack surface.

**Findings under this control:**

| Finding ID | Title | Severity | Status |
|---|---|---|---|
| FIND-003 | Default Credentials on Network Devices | Critical | Open |
| FIND-006 | Insecure Default Configurations on Workstations | Medium | Open |

**Recommended approach and sequencing:**

1. Immediately change all default credentials on network devices (FIND-003) — this is the single highest-priority item in this plan.
2. Restrict management interface access on all network devices to a dedicated management VLAN or jump host.
3. Develop a secure configuration baseline for workstations using the CIS Benchmark for [Windows 10 / Windows 11 / macOS] as a reference.
4. Deploy the configuration baseline via Group Policy (GPO) or endpoint management tooling in audit mode first, then enforce mode after validating no production impact.
5. Establish a configuration drift monitoring process to detect deviations from the approved baseline.

---

### CIS Control 5 — Account Management

**Why this control matters:** Improper account management — including excessive permissions, stale accounts, and shared credentials — is one of the most common factors enabling attackers to move laterally within an environment after initial compromise. Enforcing the principle of least privilege limits the blast radius of any single compromised account.

**Findings under this control:**

| Finding ID | Title | Severity | Status |
|---|---|---|---|
| FIND-005 | Excessive Privileged Account Permissions | Medium | Open |

**Recommended approach and sequencing:**

1. Conduct an immediate Active Directory access review to identify accounts with Domain Admin, Enterprise Admin, or equivalent privileges that do not require that level of access.
2. Remove or downgrade excess privileges. Implement tiered administration (Tier 0: Domain Controllers, Tier 1: Servers, Tier 2: Workstations).
3. Disable or remove stale accounts (accounts inactive for > 90 days) after confirming with account owners.
4. Implement a privileged access workstation (PAW) or jump host requirement for administrative tasks.
5. Establish a quarterly access review process where managers certify which accounts and permissions their staff require.

---

### CIS Control 6 — Access Control Management

**Why this control matters:** Access control determines who can reach what systems and data. Without strong access controls — particularly multi-factor authentication on remote access — a single stolen password is sufficient for an attacker to gain full access to the environment from anywhere in the world. MFA is the single most effective control for preventing unauthorized remote access.

**Findings under this control:**

| Finding ID | Title | Severity | Status |
|---|---|---|---|
| FIND-002 | MFA Not Enforced for Remote Access | High | Open |

**Recommended approach and sequencing:**

1. Procure and deploy an MFA solution compatible with the existing VPN and remote access infrastructure. Recommended options: [e.g., Cisco Duo, Microsoft Entra ID (Azure AD) MFA with Conditional Access, Okta].
2. Enforce MFA for all VPN connections first (highest risk exposure) within 30 days.
3. Extend MFA enforcement to RDP gateway access, cloud management consoles, and privileged admin portals.
4. Enforce MFA for all staff with access to sensitive systems or data.
5. Document MFA exceptions (if any) with a formal risk acceptance process and time-limited waivers.

---

### CIS Control 7 — Continuous Vulnerability Management

**Why this control matters:** The threat landscape changes daily as new vulnerabilities are discovered and exploit code is published. Without a continuous vulnerability management program — including regular scanning and a defined remediation SLA — the organization will inevitably fall behind, allowing attackers to exploit publicly known vulnerabilities that have been patched by vendors but not yet applied. Regular scanning and timely patching is the most scalable defense against commodity attacks.

**Findings under this control:**

| Finding ID | Title | Severity | Status |
|---|---|---|---|
| FIND-001 | Unpatched Critical Vulnerabilities on Internet-Facing Servers | Critical | Open |
| FIND-010 | No Formal Vulnerability Scanning Program | Medium | Open |

**Recommended approach and sequencing:**

1. Apply all critical patches to internet-facing servers immediately (FIND-001). Prioritize CVEs with CVSS ≥ 9.0 and treat these as emergency patching events.
2. Establish a monthly patching cadence for all systems, with emergency patching procedures for critical CVEs released outside the regular cycle.
3. Procure or configure a recurring vulnerability scanning solution. [Nessus Essentials (free for up to 16 IPs), Nessus Professional, or Tenable.io are recommended depending on environment size.]
4. Define remediation SLAs: Critical ≤ 15 days, High ≤ 30 days, Medium ≤ 90 days, Low ≤ 180 days.
5. Establish a monthly vulnerability management review meeting to track SLA compliance and escalate exceptions.

---

## 90-Day Roadmap

*This phased plan sequences remediation activities for maximum risk reduction within the first 90 days. Items within each phase are ordered by Priority Score.*

---

### Phase 1 — Days 1–30: Critical and High — Immediate Action and Quick Wins

**Goal:** Eliminate the highest-risk vulnerabilities and address the findings most likely to result in a breach if left unresolved.

| Priority | Finding ID | Title | Effort | Owner | Target Date |
|---|---|---|---|---|---|
| 1 | FIND-003 | Change default credentials on network devices | Low | [Network Admin] | Day 7 |
| 2 | FIND-001 | Apply critical patches to internet-facing servers | Medium | [Systems Admin] | Day 15 |
| 3 | FIND-002 | Begin MFA deployment — VPN first | Medium | [IT Manager] | Day 30 |
| 4 | FIND-007 | Conduct network discovery — baseline asset inventory | Medium | [IT Manager] | Day 30 |
| 5 | FIND-004 | Enforce TLS on all internet-facing services | Medium | [App / Network Owner] | Day 30 |
| 6 | FIND-008 | Remove unauthorized software from production systems | Low | [Systems Admin] | Day 14 |

**Phase 1 Milestones:**
- [ ] Default credentials changed on all network devices — verified by rescan
- [ ] Critical patches applied to internet-facing servers — verified by Nessus rescan
- [ ] MFA enabled for VPN — tested and confirmed
- [ ] Asset inventory baseline document completed
- [ ] Unauthorized software removed — configuration confirmed

---

### Phase 2 — Days 31–60: High and Medium — Systematic Remediation

**Goal:** Address systemic control gaps that require more planning and coordination. Begin building durable security processes.

| Priority | Finding ID | Title | Effort | Owner | Target Date |
|---|---|---|---|---|---|
| 3 | FIND-002 | Complete MFA rollout — RDP, admin portals, privileged users | Medium | [IT Manager] | Day 45 |
| 7 | FIND-005 | Conduct AD access review — remove excess privileges | Medium | [AD Admin] | Day 45 |
| 9 | FIND-009 | Enable security event logging on critical systems | Medium | [SOC / IT Admin] | Day 55 |
| — | FIND-001 | Apply High-severity patches across all systems (patching cycle) | Medium | [Systems Admin] | Day 60 |
| — | FIND-004 | Extend TLS enforcement to internal services and APIs | Medium | [App Owner] | Day 60 |

**Phase 2 Milestones:**
- [ ] MFA fully deployed across all remote access pathways — confirmed
- [ ] Access review completed — excess privileges removed, documented
- [ ] Critical systems logging to SIEM or central log repository
- [ ] High-severity patch cycle completed across all in-scope systems
- [ ] Internal service encryption enforcement verified

---

### Phase 3 — Days 61–90: Medium and Low — Hardening and Process Establishment

**Goal:** Remediate remaining medium and low findings, implement foundational security processes, and establish ongoing program cadence to sustain improvements beyond day 90.

| Priority | Finding ID | Title | Effort | Owner | Target Date |
|---|---|---|---|---|---|
| 9 | FIND-006 | Deploy CIS Benchmark workstation configuration baseline | High | [Endpoint Admin] | Day 85 |
| 10 | FIND-010 | Establish recurring vulnerability scanning program and SLA | Medium | [Security Program Owner] | Day 75 |
| — | FIND-008 | Implement software allowlist enforcement | Medium | [Systems Admin] | Day 90 |
| — | [FIND-XXX] | [Remaining medium findings] | [Varies] | [Owner] | Day 90 |
| — | [FIND-XXX] | [Low-severity findings] | [Varies] | [Owner] | Day 90 |

**Phase 3 Milestones:**
- [ ] Workstation configuration baseline deployed in enforce mode
- [ ] Vulnerability scanning program operational — first recurring scan completed
- [ ] Software allowlist enforcement active
- [ ] All medium findings remediated or formally risk-accepted with documented owner
- [ ] 90-day progress report prepared for leadership

---

## Progress Tracking

### How to Update This Document

1. **Weekly:** The assigned owner for each finding updates the **Status** column in the Master Remediation Table. Valid status values:

   | Status | Meaning |
   |---|---|
   | Open | Not yet started |
   | In Progress | Work has begun — include a brief note |
   | Pending Verification | Remediation applied — awaiting consultant verification scan |
   | Resolved | Verified resolved by consultant rescan |
   | Risk Accepted | Leadership has formally accepted the risk — document approver and date in Notes |
   | Deferred | Remediation postponed — document new target date and reason |

2. **Monthly:** The document owner (see below) reviews all status updates, updates the 90-day roadmap completion checkboxes, and prepares a one-page summary for management.

3. **Quarterly:** A full document review is conducted in conjunction with the quarterly Executive Security Risk Report. Resolved findings are archived, and new findings from subsequent assessments are added.

### Document Ownership

| Role | Name | Responsibility |
|---|---|---|
| Document Owner | [Name — typically IT Manager or CISO] | Maintains document, tracks overall progress, escalates blockers |
| Technical Lead | [Name] | Ensures technical accuracy of status updates, coordinates verification |
| Executive Sponsor | [Name] | Reviews monthly summary, approves risk acceptances |
| Consulting Contact | [Consultant Name — Firm Name] | Available for questions; conducts verification rescans |

### Review Cadence

| Activity | Frequency | Participants |
|---|---|---|
| Remediation status standup | Weekly | IT/Security team, Document Owner |
| Management progress review | Monthly | Document Owner, Executive Sponsor |
| Consultant verification scan | After each phase completion | Consulting team + Document Owner |
| Full document review and reset | Quarterly | All stakeholders |

### Escalation Process

If a remediation item is blocked by resource constraints, technical complexity, or organizational dependencies:

1. The assigned owner documents the blocker in the **Notes** column.
2. The Document Owner escalates to the Executive Sponsor.
3. If remediation cannot proceed within the SLA, a formal **Risk Acceptance** is documented (see Risk Acceptance section below).

### Risk Acceptance Process

Findings that cannot be remediated within the target timeframe must be formally risk-accepted:

1. Owner documents the reason for non-remediation and any compensating controls in place.
2. Executive Sponsor reviews and approves in writing (email approval is acceptable).
3. Risk acceptance is recorded in the **Notes** column with the approver name and acceptance date.
4. Risk acceptances are reviewed at each quarterly review — they do not grant indefinite deferral.

---

## Sign-off and Approval

*This document represents [Client Name]'s formal remediation commitment for the findings identified in the Technical Security Findings Report dated [Report Date]. By signing below, the authorized representatives confirm they have reviewed this plan and commit to the remediation timeline outlined herein.*

| Role | Name | Signature | Date |
|---|---|---|---|
| [CISO / IT Director / Authorized Owner] | [Name] | | [Date] |
| [Executive Sponsor] | [Name] | | [Date] |
| [Consulting Lead — Firm Name] | [Name] | | [Date] |

---

*Document Version: [1.0] | Last Updated: [Date] | Classification: CONFIDENTIAL | Owner: [Document Owner Name]*
