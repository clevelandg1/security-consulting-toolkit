# Zero-Day Response Playbook

**Client:** [Client Name]
**Version:** 1.0
**Effective Date:** [Effective Date]
**Playbook Owner:** [Security Team Lead / CISO]
**Last Reviewed:** [Review Date]
**Next Review:** [Review Date + 1 Year]

---

## Table of Contents

1. [Overview and Purpose](#1-overview-and-purpose)
2. [Definitions](#2-definitions)
3. [Severity Override Rule](#3-severity-override-rule)
4. [Phase 1: Discovery and Identification](#4-phase-1-discovery-and-identification)
5. [Phase 2: Initial Triage](#5-phase-2-initial-triage-within-2-hours)
6. [Phase 3: Containment](#6-phase-3-containment-within-4-24-hours)
7. [Phase 4: Remediation Planning](#7-phase-4-remediation-planning)
8. [Phase 5: Deployment and Verification](#8-phase-5-deployment-and-verification)
9. [Phase 6: Post-Incident Review](#9-phase-6-post-incident-review-within-5-business-days)
10. [Communication Templates](#10-communication-templates)
11. [RACI Matrix](#11-raci-matrix)
12. [Escalation Contacts](#12-escalation-contacts)

---

## 1. Overview and Purpose

### 1.1 Purpose

This playbook defines the structured, step-by-step response procedure that [Client Name]'s security team follows when a zero-day vulnerability is discovered or publicly disclosed that may affect systems within [Client Name]'s environment.

Zero-day vulnerabilities represent an elevated threat due to the absence of a vendor patch at the time of disclosure and, frequently, active exploitation by threat actors. The speed, coordination, and documentation of the response are critical to minimizing exposure and business impact.

This playbook is aligned with:
- **CIS Controls v8** — Control 7 (Continuous Vulnerability Management), Control 12 (Network Infrastructure Management), Control 17 (Incident Response Management)
- **NIST SP 800-61 Rev. 2** — Computer Security Incident Handling Guide
- [Client Name] Vulnerability Remediation SLA Policy (Document ID: DOC-VSLA-001)

### 1.2 Scope

This playbook applies to all zero-day vulnerabilities that:
- Affect software, hardware, or firmware used anywhere in [Client Name]'s environment
- Are publicly disclosed (including limited disclosure to vendors or researchers)
- Are discovered internally by [Client Name]'s security team or a third-party assessor

All personnel in Security Operations, IT, and relevant system owners are expected to be familiar with this playbook and their assigned responsibilities.

---

## 2. Definitions

| Term | Definition |
|------|-----------|
| **Zero-Day Vulnerability** | A vulnerability in software, hardware, or firmware that is unknown to the vendor or for which no patch exists at the time of public knowledge. The term "zero-day" refers to the fact that developers have had zero days to create and release a fix. |
| **N-Day Vulnerability** | A vulnerability for which a patch or advisory has been released by the vendor, but for which the organization has not yet applied the remediation. N-Day vulnerabilities follow the standard Vulnerability Remediation SLA Policy. |
| **Proof-of-Concept (PoC) Exploit** | Functional code or a demonstration that proves a vulnerability is exploitable. The existence of a PoC dramatically increases the urgency of response. |
| **Active Exploitation** | Confirmed or credibly reported exploitation of a vulnerability in the wild by threat actors against real-world targets. |
| **Threat Intelligence Feed** | Automated or curated data streams providing information about current threat actor activity, newly disclosed vulnerabilities, and indicators of compromise (IOCs). Examples: CISA KEV catalog, vendor security bulletins, ISAC feeds. |
| **Compensating Control** | A temporary security measure that reduces exploitability of the vulnerability while a patch is unavailable or being prepared. |
| **Exposure Window** | The period of time between when the vulnerability was first exploitable in the environment and when it was confirmed remediated or an effective compensating control was in place. |

---

## 3. Severity Override Rule

> **All zero-day vulnerabilities are automatically treated as Critical severity, regardless of their CVSS base score.**

### Rationale

CVSS base scores do not fully account for:
- The absence of a vendor-supplied patch (elevated risk)
- Active exploitation occurring in the wild
- Attacker first-mover advantage during the zero-day window
- The compressed decision timeline available to defenders

Even a zero-day with a CVSS score in the Medium range (e.g., 5.5) may present immediate, material risk to the organization due to these factors.

### Practical Effect of the Override

- Response initiates under Critical SLA timelines (24–48 hour remediation target)
- Immediate notification is required regardless of CVSS score
- CISO and CTO are notified within 4 hours of identification
- Emergency change procedures apply to any required configuration changes
- All phases of this playbook are activated in full

### Override Removal

The Critical override may be downgraded only if:
- The security team confirms with high confidence that [Client Name]'s environment is not affected by the vulnerability (no affected assets found), AND
- This conclusion is documented and approved by the Security Team Lead

If any uncertainty exists about asset exposure, the Critical override remains in effect.

---

## 4. Phase 1: Discovery and Identification

**Target Completion:** Immediately upon awareness — initiate within 30 minutes of receiving information

### 4.1 How Zero-Days Are Surfaced

The Security team monitors the following sources for zero-day disclosures:

| Source | Examples | Monitoring Frequency |
|--------|---------|----------------------|
| **Vendor Security Advisories** | Microsoft Patch Tuesday (off-cycle), Cisco PSIRT, Adobe Security Bulletins, VMware Security Advisories | Daily automated subscription |
| **Government and Industry Feeds** | CISA Known Exploited Vulnerabilities (KEV) catalog, US-CERT Alerts, ISAC alerts | Daily automated subscription |
| **Threat Intelligence Platforms** | [Threat Intel Platform — e.g., Recorded Future, Mandiant Advantage, AlienVault OTX] | Continuous automated monitoring |
| **Security Research and Media** | Project Zero disclosures, major security conference publications (DEF CON, Black Hat), reputable security news outlets | Daily manual review |
| **Internal Discovery** | Penetration test findings, red team exercises, security researcher reports via [Responsible Disclosure Program] | Ad hoc — immediate escalation |
| **Partner and MSSP Alerts** | [MSSP / MDR Provider Name] alerts | Continuous monitoring |

### 4.2 Verification Steps

Before activating the full zero-day response, the Security Analyst must verify:

- [ ] Confirm the disclosure is legitimate (vendor or credible researcher source)
- [ ] Confirm the affected software/hardware/firmware — name and version range
- [ ] Check whether a patch is currently available from the vendor
- [ ] Check CISA KEV catalog to determine if actively exploited
- [ ] Check threat intelligence feeds for IOCs and active exploit campaigns
- [ ] Determine the severity — apply Critical override per Section 3
- [ ] Confirm which CVE(s) are assigned (if any; some zero-days are pre-CVE)

### 4.3 Initial Documentation Checklist

A zero-day tracking record must be opened immediately in [Incident Management System / Vulnerability Tracking System] with the following fields populated:

- [ ] **Zero-Day Identifier:** CVE number (if assigned) or internal tracking ID
- [ ] **Date and time discovered/disclosed**
- [ ] **Affected software/hardware:** Name, vendor, affected versions
- [ ] **Patch availability:** Yes / No / Partial — with details
- [ ] **CVSS score (if available):** Base score and vector string
- [ ] **Active exploitation status:** Confirmed / Suspected / Unknown
- [ ] **Public PoC available:** Yes / No
- [ ] **Source of discovery:** [Vendor advisory URL / threat intel feed / internal discovery]
- [ ] **Initial asset impact assessment:** Pending (to be completed in Phase 2)
- [ ] **Record creator:** [Analyst Name]
- [ ] **Record creation timestamp**

### 4.4 Immediate Notifications Required

| Recipient | Notification Method | Timeframe |
|-----------|--------------------|-----------|
| Security Team Lead | Direct call + [Slack/Teams] message | Within 30 minutes of identification |
| CISO | Direct call + email | Within 1 hour of identification (4 hours if identified after hours) |
| CTO | Direct call + email (via CISO) | Within 4 hours of identification |
| [MSSP / MDR Provider] | Ticketing system + direct contact | Within 1 hour of identification |
| On-call IT Systems Administrator | Direct call | Within 1 hour if affected assets confirmed |

---

## 5. Phase 2: Initial Triage (Within 2 Hours)

**Owner:** Security Analyst + Security Team Lead
**Target Completion:** Within 2 hours of Phase 1 initiation

### 5.1 Asset Inventory Check — Are We Affected?

Immediately query the asset inventory and vulnerability management platform to determine exposure:

- [ ] Query [Asset Management System / CMDB] for assets running affected software/hardware
- [ ] Run targeted scan using [Vulnerability Scanner — e.g., Tenable.sc, Qualys, Rapid7] if signatures are available
- [ ] Manually query software inventory records (endpoint management platform, cloud asset inventory)
- [ ] Contact system owners for systems not covered by automated scanning
- [ ] Document all confirmed and suspected affected assets with hostname, IP, business function, and owner

**If no affected assets are found:** Document finding, have Security Team Lead review and approve the conclusion, maintain monitoring posture, and close the zero-day tracking record with status "Not Affected — Monitored."

### 5.2 Exposure Assessment

For each confirmed affected asset, assess the following:

| Assessment Dimension | Questions to Answer |
|---------------------|---------------------|
| **Network Exposure** | Is the asset internet-facing? Accessible from untrusted networks? DMZ-hosted? |
| **Internal Exploitability** | Can the vulnerability be exploited by an internal user without elevated privileges? |
| **Data Sensitivity** | Does the asset store, process, or transmit PII, PHI, PCI data, or intellectual property? |
| **Business Criticality** | What is the business impact if this asset is compromised or taken offline? |
| **Authentication Required** | Does exploitation require prior authentication? If so, is authentication strong? |
| **Exploit Complexity** | Is exploitation straightforward (low complexity) or requires significant effort (high complexity)? |

### 5.3 Threat Intelligence Check

- [ ] Query threat intelligence platform for IOCs related to this vulnerability
- [ ] Check CISA KEV catalog — is this CVE listed?
- [ ] Search [SIEM / EDR Platform] for any IOCs associated with known exploit activity
- [ ] Query firewall and proxy logs for suspicious traffic patterns targeting affected service/port
- [ ] Document threat intelligence findings — exploitation is: **Confirmed / Suspected / No Evidence Found**

### 5.4 Triage Decision Matrix

Based on the findings from Sections 5.1–5.3, assign one of the following triage outcomes:

| Scenario | Condition | Immediate Action |
|----------|-----------|-----------------|
| **Scenario A: Affected + Actively Exploited** | Confirmed affected assets AND confirmed or strongly suspected active exploitation | Activate Phase 3 (Containment) IMMEDIATELY. Notify CISO and CTO immediately. Treat as active incident — activate Incident Response Plan [IR Plan Reference]. |
| **Scenario B: Affected + Not Currently Exploited** | Confirmed affected assets AND no evidence of active exploitation against our environment | Activate Phase 3 (Containment) within 4 hours. Notify CISO within 1 hour. Treat as urgent — this can become Scenario A quickly. |
| **Scenario C: Possibly Affected — Uncertain** | Asset inventory is incomplete, scanning is inconclusive, or affected version range is unclear | Assume affected. Treat as Scenario B until proven otherwise. Accelerate asset inventory work. |
| **Scenario D: Not Affected** | Confirmed no affected assets in scope | Document conclusion (Security Team Lead approval required). Close active response. Maintain monitoring. |

---

## 6. Phase 3: Containment (Within 4–24 Hours)

**Owner:** Security Team Lead + IT Systems Administrator / Remediation Owner
**Target Completion:** Within 4 hours for Scenario A; within 24 hours for Scenario B

### 6.1 Immediate Containment Options by Scenario

Select the most appropriate containment action(s) for the specific vulnerability and affected assets. Multiple controls may be layered:

| Containment Option | Applicable Scenarios | Implementation Owner | Notes |
|-------------------|---------------------|---------------------|-------|
| **Network Isolation** | Scenario A — internet-facing or actively exploited asset | Network Engineer / IT Admin | Isolate affected system from the network. Use only as a last resort if business impact is acceptable — confirm with asset owner before proceeding. |
| **Firewall ACL / Rule** | Scenario A and B — restrict access to vulnerable port/service | Network Engineer | Block or restrict inbound/outbound traffic to the vulnerable service. Document rule with expiry. |
| **WAF Rule Deployment** | Scenario A and B — web application vulnerabilities | [WAF Platform Admin / Security Engineer] | Deploy virtual patch or block rule in [WAF Platform]. Confirm rule is in blocking mode, not detection-only. |
| **Disable Vulnerable Service or Feature** | Scenario A and B — service is not business-critical or can be disabled without impact | System Administrator | Disable the vulnerable service or application component. Confirm with asset owner that business impact is acceptable. |
| **IPS/IDS Signature Deployment** | Scenario A and B — supplemental detection/prevention | Security Engineer | Deploy known exploit signatures to IPS. Note: IPS is not a substitute for isolation or remediation but provides an additional layer. |
| **Enforce Authentication Controls** | Scenario B — if exploitation requires unauthenticated access | IT Admin / Identity Team | Enable authentication requirements, MFA, or restrict access to authorized users only. |
| **Enhanced Monitoring** | All scenarios as a baseline | Security Analyst (SOC) | Increase logging verbosity, create specific SIEM alerts for exploit patterns, assign SOC analyst to monitor continuously. |

### 6.2 Compensating Control Documentation

For every containment measure applied, document immediately in the zero-day tracking record:

- [ ] Control type and description
- [ ] Date and time implemented
- [ ] Implemented by (name and role)
- [ ] Validation evidence (screenshot, configuration export, scan result)
- [ ] Estimated effectiveness — does this prevent exploitation or only reduce likelihood?
- [ ] Risk acceptance sign-off from asset owner and Security Team Lead

### 6.3 Communication to Stakeholders

**At containment initiation:**
- Security Team Lead notifies CISO and CTO of containment actions being taken
- Asset Owner is notified of containment measures and any expected service impact
- [MSSP / MDR Provider] is updated with containment status

**At containment completion:**
- CISO receives written summary: affected assets, containment measures in place, residual risk, next steps
- IT Director is notified of any systems affected by containment actions
- If business operations are impacted: business unit leadership is notified via [Communication Channel]

See Section 10 for communication templates.

---

## 7. Phase 4: Remediation Planning

**Owner:** Security Team Lead + Remediation Owner
**Target Initiation:** Concurrent with or immediately following Phase 3

### 7.1 Check Vendor Patch Availability

- [ ] Check vendor security portal, advisory page, and release notes for patch availability
- [ ] Confirm patch version number and applicability to the specific affected versions in our environment
- [ ] Note vendor's recommended action (patch, configuration change, workaround, or mitigation)
- [ ] Assess vendor patch reliability — check vendor and community reports for known patch issues
- [ ] Document patch availability status and expected release date if not yet available

### 7.2 If Patch Is Available

| Step | Action | Owner |
|------|--------|-------|
| 1 | Obtain patch from official vendor source. Verify integrity (checksum/signature). | Security Analyst |
| 2 | Deploy to isolated test environment representing affected production system. | IT Admin / DevOps |
| 3 | Conduct functional testing — confirm system operates as expected post-patch. | System Owner / QA |
| 4 | Confirm vulnerability is remediated in test environment via re-scan or manual validation. | Security Analyst |
| 5 | Document test results. If testing passes, submit emergency change request. | Remediation Owner |
| 6 | Emergency change approved (see Section 7.4). | Change Advisory Board / CISO |
| 7 | Deploy to production per Phase 5. | IT Admin / DevOps |

**Minimum test duration by severity:**
- Critical zero-day: 4 hours (may compress further if Scenario A — active exploitation)
- High severity (N-Day follow-up): 24 hours

### 7.3 If No Patch Is Available

- [ ] Confirm and maintain compensating controls from Phase 3
- [ ] Enhance monitoring posture — create specific detections for known exploit behavior
- [ ] Set up automated watch on vendor advisory page for patch release notification
- [ ] Schedule daily check-in until patch is available
- [ ] If compensating controls are insufficient, evaluate whether affected systems must be taken offline
- [ ] Document compensating control strategy with explicit re-evaluation date (no longer than 7 days out)
- [ ] CISO approves and signs off on "no patch available" interim strategy

### 7.4 Change Management Integration

Zero-day responses use the **Emergency Change** process:

- Emergency change requests bypass standard CAB approval cycle
- Approval authority: [CISO] for systems changes; [CTO / IT Director] for infrastructure changes
- Post-implementation review is required within 5 business days (rolled into Phase 6)
- All emergency changes must be documented in [Change Management System] within 24 hours of implementation, even if approval was verbal during the incident

---

## 8. Phase 5: Deployment and Verification

**Owner:** IT Admin / DevOps + Security Analyst
**Target Completion:** Within 24–48 hours of confirmed patch availability (Critical SLA applies)

### 8.1 Patch Deployment Checklist

- [ ] Emergency change request is approved and documented in [Change Management System]
- [ ] Rollback plan is documented (restore from backup or known good state)
- [ ] Asset owner and business stakeholders are notified of planned maintenance window
- [ ] Patch obtained from verified official source; integrity verified (hash match confirmed)
- [ ] Pre-patch snapshot or backup taken for affected systems
- [ ] Patch deployed to production — log deployment start and end time
- [ ] Post-patch functional testing performed — confirm business services are operating normally
- [ ] Deployment documented in [Patch Management System / Change Ticket]

### 8.2 Verification Testing Steps

After deployment, the Security Analyst must confirm remediation:

- [ ] Re-scan affected asset(s) using [Vulnerability Scanner] — confirm the vulnerability is no longer detected
- [ ] If scanner signatures are not yet updated: perform manual validation using vendor-provided verification steps or a controlled test
- [ ] Review system logs for any anomalies post-patch
- [ ] Confirm that all previously identified affected assets have been patched (no missed assets)
- [ ] Document verification method, tool used, scan date, and result in tracking record

### 8.3 Removal of Compensating Controls

Once the patch is deployed and remediation is verified:

- [ ] Review all compensating controls implemented in Phase 3
- [ ] Confirm each compensating control is no longer needed (patch provides the fix)
- [ ] Remove or roll back each compensating control in a controlled manner (document removal)
- [ ] Confirm removal does not reintroduce risk — perform final validation scan
- [ ] Update tracking record: compensating controls removed, replaced by patch, date confirmed

**Note:** Compensating controls should not remain in place longer than necessary after successful patching. Orphaned compensating controls (e.g., permanent firewall rules) can create technical debt and unexpected behavior.

### 8.4 Sign-Off Requirements

Full closure of the zero-day event requires sign-off from:

| Role | Sign-Off Confirms |
|------|------------------|
| Security Analyst | Vulnerability confirmed remediated via scan/validation |
| Remediation Owner / System Admin | Patch deployed and system is functioning normally |
| Security Team Lead | All affected assets remediated, compensating controls removed, tracking record complete |
| CISO | Final closure approved; event is formally closed |

---

## 9. Phase 6: Post-Incident Review (Within 5 Business Days)

**Owner:** Security Team Lead
**Attendees:** Security Analyst(s), Remediation Owner(s), IT Director, CISO (and CTO if appropriate)

### 9.1 Review Objectives

The post-incident review (also called "lessons learned") is a structured meeting and written report intended to:
- Establish a complete factual timeline of the event
- Measure the effectiveness of the response
- Identify gaps in process, tooling, or communication
- Drive continuous improvement — not assign blame

### 9.2 Required Review Content

**What happened — Timeline reconstruction:**
- When was the vulnerability disclosed (public disclosure date/time)?
- When did [Client Name]'s security team first become aware?
- What was the detection method?
- How long was the exposure window (disclosure to containment? disclosure to remediation?)?
- Were any exploitation attempts detected against our environment?

**How it was detected:**
- Which monitoring source surfaced the vulnerability?
- Was detection timely? If not, why?
- Were existing monitoring tools sufficient?

**Response assessment — What worked:**
- Which phases went smoothly?
- Which tools or processes performed well?
- Were SLA timelines met? (Containment, remediation targets)

**Response assessment — What didn't work:**
- Were there delays? At what phase and why?
- Were there communication gaps?
- Were any compensating controls insufficient?
- Were any affected assets initially missed?

**Exposure window summary:**

| Asset | First Exposure Date | Containment Date | Remediation Date | Exposure Window (Days) |
|-------|--------------------|-----------------|-----------------|-----------------------|
| [Hostname / Asset Name] | [Date] | [Date] | [Date] | [Calculated] |

### 9.3 Lessons Learned

Document at minimum three actionable lessons learned in the categories below (not all categories need to apply):

| Category | Lesson Learned | Action Item | Owner | Due Date |
|----------|----------------|-------------|-------|----------|
| Detection | [e.g., "Threat intel feed did not alert until 6 hours after public disclosure"] | [e.g., "Add CISA KEV catalog to automated daily ingestion"] | [Security Analyst] | [Date] |
| Asset Inventory | [e.g., "Two affected servers were not in CMDB"] | [e.g., "Conduct quarterly CMDB reconciliation against active network scan"] | [IT Admin] | [Date] |
| Communication | [e.g., "Executive notification was delayed by 3 hours"] | [e.g., "Update escalation procedure with 1-hour hard deadline for CISO notification"] | [Security Team Lead] | [Date] |
| Containment | [e.g., "WAF rule took 2 hours to deploy due to approval bottleneck"] | [e.g., "Pre-authorize Security Team Lead to deploy emergency WAF rules without CAB approval"] | [CISO] | [Date] |
| Tooling | [e.g., "Scanner did not have a signature for the vulnerability until day 3"] | [e.g., "Evaluate additional scanner or manual validation procedures for pre-signature zero-days"] | [Security Team Lead] | [Date] |

### 9.4 Post-Review Report

A written Post-Incident Review report must be completed within 5 business days and distributed to:
- CISO
- CTO / IT Director
- Security Team Lead
- [Executive Sponsor] (for Critical events)

The report is retained in [Document Management System] for a minimum of [3 years / per retention policy].

---

## 10. Communication Templates

### 10.1 Internal Notification — Security Team and IT Staff

> **SUBJECT: [URGENT] Zero-Day Vulnerability Identified — [CVE Number / Vulnerability Name]**
>
> **Severity:** Critical (Zero-Day Override Applied)
> **Date/Time:** [Timestamp]
> **Issued By:** [Security Team Lead Name]
>
> **Summary:**
> A zero-day vulnerability has been identified that may affect [Client Name] systems. This message initiates our Zero-Day Response Playbook.
>
> **Vulnerability:** [CVE Number] — [Brief description, e.g., "Remote code execution vulnerability in Apache Log4j affecting versions 2.0-beta9 through 2.14.1"]
>
> **Patch Available:** [Yes / No — If yes: Version X.X.X released by vendor]
>
> **Affected Assets (Initial Assessment):** [List known or suspected affected systems, or "Asset inventory check in progress"]
>
> **Active Exploitation:** [Confirmed in the wild / Not confirmed / Under investigation]
>
> **Current Status:** [Phase 1 — Identification / Phase 2 — Triage / Phase 3 — Containment]
>
> **Immediate Actions Required:**
> - [IT Admin Team]: Please confirm whether [Software/System] is deployed on systems not covered by automated scanning. Report to [Security Analyst Name] by [Time].
> - [System Owners]: Please review your systems and respond to any direct requests from the Security team immediately.
>
> **Next Update:** [Time / "Updates will be provided every 2 hours until containment is achieved"]
>
> **Contact:** [Security Team Lead Name] — [Contact Method]

---

### 10.2 Executive Notification

> **SUBJECT: [EXECUTIVE ALERT] Critical Zero-Day Vulnerability — [CVE / Vulnerability Name] — Action in Progress**
>
> **To:** [CISO, CTO, Executive Sponsor]
> **Date/Time:** [Timestamp]
> **Issued By:** [CISO / Security Team Lead]
>
> **Situation:**
> A critical zero-day vulnerability ([CVE Number]) affecting [Affected Software/System] was [disclosed / discovered] on [Date/Time]. [Client Name]'s Security team activated the Zero-Day Response Playbook at [Time].
>
> **Business Impact:**
> [e.g., "Approximately [X] servers in our environment are running affected versions. Systems include [general description — e.g., web-facing application servers]. If exploited, an attacker could [brief, plain-language impact — e.g., execute arbitrary code remotely without authentication]."]
>
> **Current Status:**
> - Containment measures: [In place / In progress — e.g., "Firewall rules restricting external access to affected services have been applied as of [Time]"]
> - Patch availability: [Available — deployment in progress / Not yet available — compensating controls in place]
> - Evidence of exploitation: [None detected / Under investigation]
>
> **Action Required from Leadership:**
> [None at this time — Security team is managing response] OR [Approval of emergency change request #[Number] required — [CISO] will contact you directly]
>
> **Next Steps:**
> - [Planned action 1] — ETA [Time]
> - [Planned action 2] — ETA [Time]
>
> **Next Executive Update:** [Time]
>
> **Primary Contact:** [CISO Name] — [Direct Line]

---

### 10.3 Vendor Escalation Communication

> **SUBJECT: [URGENT] Security Vulnerability Escalation — [CVE Number / Product Name] — [Client Name]**
>
> **To:** [Vendor Security / PSIRT Contact]
> **From:** [CISO / Security Team Lead Name], [Client Name]
> **Date:** [Date]
>
> **Vendor:** [Vendor Name]
> **Product:** [Product Name]
> **Version(s) Affected:** [Version Range]
> **CVE:** [CVE Number] (or "Pre-CVE — no identifier assigned yet")
>
> **Issue:**
> [Client Name] has identified that [Vulnerability Description] affects our production deployment of [Product Name] version [X.X]. We have confirmed [X] systems in our environment are running affected versions.
>
> **Current Exposure:**
> [Brief description of our exposure — e.g., "Three internet-facing servers are running the affected version. We have implemented firewall restrictions as a temporary compensating control."]
>
> **Specific Requests:**
> 1. **Patch availability:** What is the expected release date for a security patch addressing this vulnerability?
> 2. **Vendor-recommended mitigations:** Please confirm any vendor-recommended configuration changes or workarounds that can reduce risk in the interim.
> 3. **IOCs:** Please provide any known indicators of compromise that would help us detect exploitation attempts.
> 4. **Escalation:** Please escalate this request to your PSIRT / Security Response team if not already engaged.
>
> **Urgency:** This is a critical priority for [Client Name]. We request a response within **4 business hours**.
>
> **Primary Contact:** [Name] — [Email] — [Direct Phone]

---

## 11. RACI Matrix

**R = Responsible | A = Accountable | C = Consulted | I = Informed**

| Activity | Security Analyst | Security Team Lead | CISO | CTO / IT Director | IT Admin / System Owner | [MSSP / MDR] |
|----------|:---:|:---:|:---:|:---:|:---:|:---:|
| **Phase 1: Monitor threat intel feeds** | R | A | I | I | | C |
| **Phase 1: Verify vulnerability validity** | R | A | I | | | C |
| **Phase 1: Create tracking record** | R | A | I | | | |
| **Phase 1: Initial notifications** | R | A | I | I | I | I |
| **Phase 2: Asset inventory check** | R | A | I | C | C | C |
| **Phase 2: Exposure assessment** | R | A | C | I | C | |
| **Phase 2: Threat intelligence check** | R | A | C | | | R |
| **Phase 2: Triage decision** | C | R | A | I | I | C |
| **Phase 3: Containment implementation** | C | A | C | C | R | |
| **Phase 3: Compensating control documentation** | R | A | C | | R | |
| **Phase 3: Stakeholder communication** | | R | A | I | I | I |
| **Phase 4: Vendor patch check** | R | A | I | | | |
| **Phase 4: Remediation planning** | C | R | A | C | C | |
| **Phase 4: Emergency change submission** | | R | A | C | C | |
| **Phase 5: Patch testing** | C | A | | | R | |
| **Phase 5: Patch deployment** | | A | | C | R | |
| **Phase 5: Verification scanning** | R | A | I | | | |
| **Phase 5: Compensating control removal** | | A | C | | R | |
| **Phase 5: Final sign-off** | C | R | A | C | C | |
| **Phase 6: Post-incident review facilitation** | C | R | A | C | C | |
| **Phase 6: Lessons learned documentation** | R | A | C | I | C | |
| **Phase 6: Post-review report distribution** | | R | A | I | I | |

---

## 12. Escalation Contacts

| Role | Name | Primary Contact | After-Hours / On-Call |
|------|------|-----------------|-----------------------|
| Security Team Lead (On-Call) | [Security Team Lead Name] | [email@clientdomain.com] | [Mobile Number] / [PagerDuty Handle] |
| CISO | [CISO Name] | [ciso@clientdomain.com] | [Mobile Number] |
| CTO | [CTO Name] | [cto@clientdomain.com] | [Mobile Number] |
| IT Director | [IT Director Name] | [itdirector@clientdomain.com] | [Mobile Number] |
| Network Engineer (On-Call) | [Network Engineer Name] | [neteng@clientdomain.com] | [Mobile Number] / [PagerDuty Handle] |
| [MSSP / MDR Provider] SOC | [Provider Name] | [SOC Email] | [24x7 SOC Phone Number] |
| Executive Sponsor | [Executive Sponsor Name] | [execsponsor@clientdomain.com] | [Mobile Number] |
| Legal Counsel (if breach notification required) | [Legal Counsel Name] | [legal@clientdomain.com] | [Mobile Number] |

---

*This playbook is confidential and intended for internal use by [Client Name] and authorized personnel only. Unauthorized distribution is prohibited.*

*Document ID: [DOC-ZDR-001] | Classification: [Confidential / Internal] | Related Documents: DOC-VSLA-001, [IR Plan Reference]*
