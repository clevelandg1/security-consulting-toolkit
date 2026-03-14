# Patch Management Policy

**Client:** [Client Name]
**Version:** 1.0
**Effective Date:** [Effective Date]
**Policy Owner:** [IT Director / CISO]
**Last Reviewed:** [Review Date]
**Next Review:** [Review Date + 1 Year]

---

## Table of Contents

1. [Purpose and Scope](#1-purpose-and-scope)
2. [Policy Statement](#2-policy-statement)
3. [Patch Classification](#3-patch-classification)
4. [Patch Management Process](#4-patch-management-process)
5. [Emergency Patch Process](#5-emergency-patch-process)
6. [Patch Coverage Requirements](#6-patch-coverage-requirements)
7. [Scope Inclusions](#7-scope-inclusions)
8. [Scope Exclusions and Special Handling](#8-scope-exclusions-and-special-handling)
9. [Exception Process](#9-exception-process)
10. [Reporting Requirements](#10-reporting-requirements)
11. [Roles and Responsibilities](#11-roles-and-responsibilities)
12. [Tool Requirements](#12-tool-requirements)
13. [Policy Review](#13-policy-review)
14. [Approval and Signatures](#14-approval-and-signatures)

---

## 1. Purpose and Scope

### 1.1 Purpose

This policy establishes [Client Name]'s requirements for the timely identification, testing, approval, deployment, and verification of security patches and updates across its technology environment. Effective patch management is a foundational security control that reduces the attack surface by eliminating known vulnerabilities in a structured and risk-informed manner.

This policy is aligned with:
- **CIS Controls v8** — Control 7 (Continuous Vulnerability Management), Control 2 (Inventory and Control of Software Assets), Control 4 (Secure Configuration of Enterprise Assets and Software)
- **NIST SP 800-40 Rev. 4** — Guide to Enterprise Patch Management Planning
- [Client Name] Vulnerability Remediation SLA Policy (Document ID: DOC-VSLA-001)

### 1.2 Scope

This policy applies to all technology assets owned, leased, or managed by [Client Name], including:

- All operating systems (Windows, Linux, macOS, server and endpoint)
- All commercial and open-source applications
- Firmware on servers, network devices, storage systems, and physical security systems
- Network infrastructure (firewalls, routers, switches, wireless access points, VPN concentrators)
- Cloud-hosted resources (virtual machines, containers, managed services, serverless functions)
- Mobile devices managed under [Client Name]'s Mobile Device Management (MDM) platform

This policy applies to all employees, contractors, managed service providers, and third parties who administer or manage [Client Name] systems.

### 1.3 Relationship to the Vulnerability Remediation SLA Policy

Patch deployment timelines in this policy are aligned with and subordinate to the [Client Name] Vulnerability Remediation SLA Policy (DOC-VSLA-001). Where a vulnerability is identified that requires patching, the SLA timelines in DOC-VSLA-001 govern the required remediation window. This policy governs the process by which patches are evaluated, tested, approved, and deployed.

---

## 2. Policy Statement

[Client Name] is committed to maintaining a proactive, risk-based patch management program that:

1. Identifies applicable patches through systematic monitoring of vendor advisories, vulnerability scan results, and threat intelligence sources
2. Evaluates each patch for applicability and prioritizes deployment based on vulnerability severity and environmental context
3. Tests patches in a controlled environment prior to production deployment to minimize service disruption
4. Deploys patches within defined timelines consistent with vulnerability severity tiers
5. Verifies successful patch deployment through automated scanning and manual confirmation
6. Documents all patching activities in a centralized system for audit, compliance, and reporting purposes
7. Maintains an exception process for cases where patching within the required timeline is not feasible

Failure to maintain patch currency within the defined timelines is a security risk that must be formally documented and accepted through the exception process. Unmanaged patch debt is not acceptable.

---

## 3. Patch Classification

All patches are classified into one of four tiers based on the severity of the vulnerability or vulnerabilities they address. Classification is consistent with the Vulnerability Remediation SLA Policy.

| Classification | CVSS Range | Description | Patch Deployment Timeline | Change Process |
|----------------|------------|-------------|---------------------------|----------------|
| **Critical** | 9.0 – 10.0 | Addresses remote code execution, authentication bypass, or other vulnerabilities enabling immediate system compromise with minimal attacker prerequisites. Zero-day patches always fall in this tier. | **24–48 hours** from patch availability | Emergency Change |
| **High** | 7.0 – 8.9 | Addresses vulnerabilities that significantly increase risk of compromise, privilege escalation, or lateral movement, typically requiring some access or interaction. | **7 calendar days** from patch availability | Emergency or Expedited Change |
| **Medium** | 4.0 – 6.9 | Addresses vulnerabilities presenting moderate risk, typically dependent on specific conditions or configurations. | **30 calendar days** from patch availability | Standard Change |
| **Low** | 0.1 – 3.9 | Addresses vulnerabilities with limited exploitability or low potential impact. Includes general maintenance and hardening patches. | **90 calendar days** from patch availability | Standard Change |

### 3.1 Patch Classification Override

As with vulnerability severity, patch classification may be upgraded based on contextual factors, including:

- Active exploitation of the underlying vulnerability (confirmed in CISA KEV or threat intelligence)
- Affected systems are internet-facing or store sensitive data
- Public proof-of-concept exploit code is available

Overrides are applied by the Security Team Lead and documented in the patch tracking record.

---

## 4. Patch Management Process

### Step 1: Discovery — Identifying Applicable Patches

Patches are identified through the following systematic sources:

| Source | Examples | Monitoring Frequency |
|--------|---------|----------------------|
| **Vendor Security Advisories** | Microsoft Security Update Guide, Red Hat Errata, Cisco PSIRT, Adobe Security Bulletins, VMware Security Advisories, Oracle Critical Patch Updates | Daily automated subscription |
| **Vulnerability Scanner Alerts** | [Vulnerability Scanner Platform] scheduled and ad hoc scan results | [Scanning frequency — e.g., Weekly for endpoints, Daily for internet-facing systems] |
| **Vulnerability Management Reports** | Security team findings, penetration test reports, third-party assessments | Per assessment schedule |
| **Threat Intelligence Feeds** | CISA Known Exploited Vulnerabilities catalog, [Threat Intel Platform] | Daily automated review |
| **Patch Management Platform** | [Patch Management Platform] automatic patch detection | Continuous / scheduled synchronization |
| **ISAC / Community Alerts** | [Relevant ISAC — e.g., MS-ISAC, FS-ISAC] | As received |

**Ownership:** Security Analyst and Patch Management Team maintain and monitor all discovery sources. Newly identified patches are logged in [Patch Management System] within 1 business day of identification.

---

### Step 2: Assessment — Evaluating Patch Applicability and Risk

Before any patch is tested or deployed, it must be assessed for:

**Applicability:**
- Does [Client Name]'s environment include the affected software/hardware/firmware?
- Which specific assets are affected (from asset inventory and recent scan results)?
- Is the affected software component in active use, or is it present but unused?

**Risk of not patching:**
- What is the severity tier (per Section 3)?
- Is the vulnerability being actively exploited in the wild?
- Are affected systems internet-facing, storing sensitive data, or critical to operations?

**Risk of patching:**
- Could applying the patch break application functionality or compatibility?
- Are there known vendor or community reports of post-patch issues?
- What is the rollback complexity if the patch causes problems?
- Is a maintenance window required, and when is the next available window?

**Assessment output:** Each patch is assigned:
1. A severity tier (Critical / High / Medium / Low)
2. An applicability determination (Applicable to X assets / Not Applicable — document reason)
3. A deployment timeline target
4. A risk note summarizing any known patching risks

Assessment is performed by the Patch Management Team with input from the Security Analyst. Documentation is completed in [Patch Management System].

---

### Step 3: Testing — Validating Patch Safety Before Production Deployment

All patches must be tested in a non-production environment before deployment to production, except in Critical/zero-day emergency scenarios (see Section 5).

**Test Environment Requirements:**
- Test environment must reasonably represent production (same OS version, same application stack where relevant)
- Test environment must be maintained and kept current — it is not acceptable to test on a significantly outdated test system
- Critical business applications must have a dedicated or representative test instance

**Minimum Test Duration by Severity:**

| Severity | Minimum Test Duration | Notes |
|----------|-----------------------|-------|
| Critical | 2–4 hours | Emergency scenarios may compress further — document rationale |
| High | 8–24 hours | Functional testing and stability review required |
| Medium | 2–5 business days | Standard UAT process |
| Low | 5 business days | Can be bundled with monthly or quarterly patch cycles |

**Testing Checklist:**
- [ ] Patch applied successfully to test system
- [ ] System rebooted (if required) and stable
- [ ] Core application functionality verified (smoke test)
- [ ] No unexpected errors in system or application logs post-patch
- [ ] Vulnerability re-scan confirms the target vulnerability is addressed by the patch
- [ ] Rollback tested (confirm ability to revert if needed)
- [ ] Test results documented in [Patch Management System] with tester name and date

**Rollback Planning:**
- All production systems must have a verified rollback path before patching begins
- Rollback options include: system snapshot (VM), backup restoration, or patch uninstall procedure
- Rollback procedure must be documented in the change request before approval is granted

---

### Step 4: Approval — Change Management Authorization

All patch deployments require formal change management approval:

| Severity | Approval Type | Approver(s) | Approval Timeline |
|----------|--------------|-------------|-------------------|
| Critical | Emergency Change | [CISO] for security changes; [IT Director / CTO] for infrastructure | Immediate — verbal approval acceptable if documented within 24 hours |
| High | Expedited Change | [IT Director] + [Security Team Lead] | Within 24 hours of request submission |
| Medium | Standard Change | [Change Advisory Board (CAB)] | Per standard CAB meeting cadence (e.g., weekly) |
| Low | Standard Change (may be pre-authorized) | [CAB] or pre-approved change template | Per standard CAB meeting cadence or pre-authorization |

**Change request must include:**
- Patch identifier (CVE, KB article, vendor advisory reference)
- List of affected assets to be patched
- Deployment date, time, and maintenance window
- Rollback plan
- Test results summary
- Requester and approver names

Pre-authorized (standard) change templates may be established for routine, recurring patch types (e.g., monthly OS patch cycles) to reduce CAB overhead for Low and Medium patches.

---

### Step 5: Deployment — Applying Patches to Production

**Maintenance Window Policy:**

| Severity | Maintenance Window Requirement |
|----------|-------------------------------|
| Critical | Deployed as soon as patch and emergency change approval are in place. May occur outside standard windows. Asset owner must be notified minimum 1 hour in advance (or immediately if not feasible). |
| High | Deployed within the next available maintenance window not exceeding 7 days from patch availability, or outside windows with expedited change approval. |
| Medium | Deployed during standard scheduled maintenance windows (see schedule below). |
| Low | Deployed during standard maintenance windows — may be batched with monthly or quarterly patch cycles. |

**Standard Maintenance Windows:** [e.g., Tuesdays and Thursdays, 10:00 PM – 2:00 AM local time / Saturdays 12:00 AM – 6:00 AM local time — adjust per client environment]

**Phased Rollout Approach (for High/Medium/Low patches affecting many systems):**

To minimize risk, patches affecting large numbers of systems should be deployed in phases:

| Phase | Scope | Purpose |
|-------|-------|---------|
| Phase 1 (Pilot) | 5–10% of affected assets (representative sample) | Detect unexpected issues before broad rollout |
| Phase 2 (Early Adopters) | 25–50% of affected assets | Confirm stability; monitor for 24 hours |
| Phase 3 (Broad Deployment) | Remaining affected assets | Full production rollout |

Phased rollout may be compressed or skipped for Critical patches requiring emergency deployment.

**Deployment Checklist:**
- [ ] Change request approved and documented
- [ ] Rollback procedure confirmed ready
- [ ] Asset owner notified of deployment window
- [ ] Pre-patch backup or snapshot taken
- [ ] Patch deployed per approved change
- [ ] Post-patch system stability confirmed
- [ ] Deployment logged in [Patch Management System] with timestamp and deploying engineer

---

### Step 6: Verification — Confirming Successful Patching

Patching is not considered complete until verified. Verification must occur within 24 hours of deployment for Critical/High patches, and within 7 days for Medium/Low:

- [ ] Re-scan affected asset(s) using [Vulnerability Scanner] — confirm vulnerability is no longer reported
- [ ] If scanner signatures are pending: manually confirm patch version installed (e.g., `wmic qfe`, `rpm -qa`, `dpkg -l`, or equivalent)
- [ ] Confirm all assets in scope for the patch cycle have been addressed — identify any missed systems
- [ ] Record verification results in [Patch Management System]: scan date, tool, result, verified by
- [ ] For Critical patches: Security Team Lead reviews and signs off on verification evidence

Failed or partial deployments must be documented and a new remediation timeline set within 24 hours.

---

### Step 7: Documentation — Recording Patch Activities

All patch activities must be recorded in [Patch Management System] and include:

| Field | Required Data |
|-------|--------------|
| Patch identifier | CVE number(s), vendor advisory reference, KB article / package name |
| Affected asset list | Hostname, IP, asset owner |
| Severity classification | Critical / High / Medium / Low |
| Deployment timeline target | Date required |
| Change request number | [Change Management System] reference |
| Test results | Summary and tester name |
| Deployment date and time | Actual deployment timestamp |
| Deployed by | Engineer name |
| Verification date | Re-scan or manual verification date |
| Verification result | Pass / Fail / Partial — with details |
| Exception status | None / Exception granted [reference] |
| Final status | Remediated / In Progress / Exception / Excluded |

Records must be retained for a minimum of [3 years / per data retention policy].

---

## 5. Emergency Patch Process

The Emergency Patch Process applies to:
- All Critical severity patches (CVSS 9.0–10.0)
- All zero-day vulnerabilities (automatic Critical treatment)
- Any patch where the Security Team Lead or CISO determines that the standard process timeline presents unacceptable risk

### Emergency Patch Process Steps

| Step | Action | Owner | Timeframe |
|------|--------|-------|-----------|
| 1 | Security team confirms patch applicability and affected assets | Security Analyst | Within 1 hour of patch identification |
| 2 | CISO and Security Team Lead are notified | Security Analyst | Immediately |
| 3 | Risk assessment — patch vs. compensating control decision | Security Team Lead + CISO | Within 2 hours |
| 4 | Compensating controls applied while patch is prepared (if needed) | IT Admin | Immediately |
| 5 | Patch obtained from vendor — integrity verified | Patch Management Team | Within 2–4 hours |
| 6 | Expedited testing in test environment (2–4 hours minimum) | IT Admin / Patch Team | Within 4–6 hours |
| 7 | Emergency change verbal approval obtained (CISO / IT Director) | Security Team Lead | Before deployment |
| 8 | Patch deployed to production — phased if feasible, direct if not | IT Admin | Within 24–48 hours of patch availability |
| 9 | Post-patch stability and functional validation | System Owner / IT Admin | Immediately post-deployment |
| 10 | Vulnerability re-scan — verify remediation | Security Analyst | Within 4 hours of deployment |
| 11 | Formal emergency change documentation submitted to [Change Management System] | Patch Management Team / Change Owner | Within 24 hours of deployment |
| 12 | After-action documentation complete in patch tracking system | Security Analyst | Within 24 hours |
| 13 | Post-incident review scheduled (for zero-day events) | Security Team Lead | Within 5 business days — see Zero-Day Playbook DOC-ZDR-001 |

### Emergency Patch Approval Authority

| Scenario | Approval Authority |
|----------|-------------------|
| Security-related emergency patch (OS, application) | CISO |
| Network infrastructure emergency patch | IT Director / CTO |
| Third-party managed system emergency patch | [MSSP / Managed Service Provider] notified — approval via CISO |

Verbal approvals given during emergency response must be followed by written documentation in [Change Management System] within 24 hours.

---

## 6. Patch Coverage Requirements

[Client Name] requires the following minimum patch coverage rates within each SLA window:

| Severity | Coverage Target | Measurement Period |
|----------|-----------------|--------------------|
| Critical | 100% of affected assets within 24–48 hours | Measured per event |
| High | ≥ 95% of affected assets within 7 days | Measured per patch cycle |
| Medium | ≥ 90% of affected assets within 30 days | Measured monthly |
| Low | ≥ 85% of affected assets within 90 days | Measured quarterly |

Systems not meeting coverage targets must be individually reviewed — each gap requires either an approved exception or documentation of why the asset was excluded from scope.

Coverage is measured as:

> **Coverage Rate = (Assets successfully patched within SLA / Total in-scope affected assets) × 100**

Coverage metrics are reported monthly to the CISO and IT Director per Section 10.

---

## 7. Scope Inclusions

The following asset categories are in scope for this policy:

| Category | Specific Inclusions |
|----------|---------------------|
| **Operating Systems** | Windows Server and Desktop (all supported versions), Linux distributions (RHEL, Ubuntu, CentOS, Debian, etc.), macOS (endpoints and servers) |
| **Server Applications** | Web servers (IIS, Apache, Nginx), database servers (MSSQL, MySQL, PostgreSQL, Oracle), email servers, directory services (Active Directory, LDAP) |
| **End-User Applications** | Browsers (Chrome, Edge, Firefox), productivity suites (Microsoft 365, Google Workspace), PDF readers, video conferencing clients, VPN clients |
| **Network Devices** | Firewalls, routers, switches, wireless access points, load balancers, VPN concentrators |
| **Security Tools** | Endpoint protection platforms, SIEM agents, vulnerability scanners, DLP agents |
| **Firmware** | Server firmware (BIOS/UEFI, iDRAC/iLO), network device firmware, storage array firmware |
| **Cloud Resources** | Cloud-hosted virtual machines (IaaS), container base images, managed cloud service configurations (where patching is client responsibility) |
| **Containers** | Container images and runtime environments — base image patching and image refresh cycles |
| **Mobile Devices** | Corporate-managed iOS and Android devices enrolled in [MDM Platform] |

---

## 8. Scope Exclusions and Special Handling

Some asset categories present unique patching constraints and require tailored handling rather than standard patch management procedures.

### 8.1 Operational Technology (OT) and Industrial Control Systems (ICS)

- **Exclusion from standard process:** OT/ICS environments (PLCs, SCADA systems, HMIs, RTUs) are excluded from this policy's standard patch process due to availability requirements, vendor support restrictions, and operational risk.
- **Special handling:** OT/ICS patching is governed by [OT Security Policy Reference] and requires coordination with operations leadership, system vendors, and scheduled production downtime windows.
- **Risk management:** Until patches can be safely applied, compensating controls (network segmentation, application whitelisting, enhanced monitoring) must be documented and maintained.

### 8.2 Medical Devices

- **Exclusion from standard process:** FDA-regulated medical devices are excluded from standard OS and application patching procedures.
- **Special handling:** Medical device patching is coordinated with the device manufacturer/vendor and is subject to FDA guidance. [Client Name]'s [Biomedical Engineering Team / Clinical Engineering] manages this process.
- **Risk management:** Compensating controls (network segmentation, restricted access) are maintained where vendor-authorized patching cannot occur within the standard SLA window.

### 8.3 Legacy Systems

Legacy systems are defined as systems running software or operating systems that are no longer supported by the vendor (end-of-life / end-of-support) and for which patches are no longer issued.

- **Elevated risk acknowledgment:** Legacy systems represent a material and ongoing security risk. Their continued operation must be formally justified and risk-accepted by the CISO.
- **Required compensating controls:** Network isolation or segmentation; application-layer access controls; enhanced monitoring and alerting; documented decommission or migration plan with a target completion date.
- **Annual review:** All legacy systems must be formally reviewed and re-approved annually by the CISO.

### 8.4 Vendor-Managed Third-Party Systems

- For systems fully managed by a third party (SaaS platforms, co-located vendor-managed hardware), [Client Name] relies on contractual SLA enforcement.
- Vendor patch management obligations must be defined in contracts and vendor agreements.
- [Client Name] Security team monitors vendor advisories and confirms vendor compliance with patching commitments.

---

## 9. Exception Process

### 9.1 When an Exception May Be Requested

A patch management exception may be requested when:
- A patch cannot be deployed within the required timeline due to compatibility, stability, or operational constraints
- No patch is currently available from the vendor (exception documents the pending state)
- The asset falls under a special handling category (Section 8) with documented constraints
- A critical business event (e.g., system freeze, production release) conflicts with the patch window

### 9.2 Exception Request Requirements

The system or application owner must submit an exception request through [GRC Platform / Patch Management System] including:

1. Asset(s) affected and their business function
2. Patch identifier and vulnerability reference
3. Reason patching cannot occur within the required timeline
4. Compensating controls currently in place or proposed
5. Proposed alternative patching date
6. Risk impact statement — what is the residual risk during the exception period?
7. Sign-off from the system/application owner

### 9.3 Exception Approval Requirements and Limits

| Severity | Approver | Maximum Exception Duration |
|----------|----------|---------------------------|
| Critical | CISO + IT Director | 30 calendar days |
| High | CISO | 30 calendar days |
| Medium | Security Team Lead | 60 calendar days |
| Low | Security Team Lead | 90 calendar days |

All exceptions are logged in [GRC Platform] and reviewed monthly at the patch compliance review.

### 9.4 Compensating Controls During Exceptions

All approved exceptions must include documented compensating controls commensurate with the vulnerability severity:

| Severity | Minimum Compensating Controls Required |
|----------|----------------------------------------|
| Critical | Network isolation or firewall ACL; WAF or IPS rule if applicable; enhanced SIEM monitoring with SOC alerting; written CISO risk acceptance |
| High | Firewall ACL or service restriction; IPS signature (if available); weekly Security team review of exception status |
| Medium | Access restriction (limit to authorized users); standard monitoring; monthly review |
| Low | Standard monitoring; quarterly review |

### 9.5 Maximum Total Exception Duration

Exceptions may not be renewed indefinitely. Total exception duration limits:

- **Critical:** 30 days total — beyond this requires board-level risk acceptance
- **High:** 60 days total
- **Medium:** 120 days total
- **Low:** 180 days total

Systems exceeding these limits must be escalated to the CISO and may require formal risk acceptance by executive leadership.

---

## 10. Reporting Requirements

### 10.1 Patch Compliance Dashboard

A real-time (or near-real-time) patch compliance dashboard must be maintained in [Patch Management / Vulnerability Management Platform], providing:

- Current patch compliance rate by severity tier and asset group
- Open unpatched vulnerabilities with days remaining in SLA
- Overdue patches (SLA breached) by asset and owner
- Active exceptions with expiration dates
- Trend line for compliance rates (last 90 days)

Access: Security Team Lead, IT Director, CISO, Patch Management Team, and relevant system owners.

### 10.2 Monthly Reporting

**Audience:** CISO, IT Director, Security Team Lead

**Contents:**
- Total patches identified, deployed, and verified in the reporting period
- Patch coverage rate by severity tier vs. target
- SLA compliance — on-time vs. late by severity
- Open exceptions and status
- Mean time to patch (MTTP) by severity tier
- Systems with no patch activity (potential coverage gaps)
- Patch failures and re-deployment status
- Month-over-month trend

### 10.3 Quarterly Executive Reporting

**Audience:** Executive Leadership

**Contents:**
- Patch program health summary
- Coverage trend quarter-over-quarter
- Significant exceptions or risk exposures
- Emergency patch events and outcomes
- Improvement initiatives and status

### 10.4 Exception Tracking

All open exceptions are tracked in [GRC Platform] with:
- Exception ID and reference
- Asset and vulnerability details
- Compensating controls in place
- Approval date and approver
- Expiration date
- Review status

Exception report is distributed monthly to Security Team Lead and CISO.

---

## 11. Roles and Responsibilities

| Role | Responsibilities |
|------|-----------------|
| **CISO** | Policy owner; approves Critical patch exceptions; receives escalations for SLA breaches; reviews monthly and quarterly patch reports; approves emergency patch strategy |
| **IT Director** | Ensures IT resources are available to support patch deployment timelines; co-approves infrastructure emergency changes; reviews monthly reporting; removes organizational blockers |
| **Security Team Lead** | Oversees daily patch management operations; approves Medium/Low exceptions; reviews weekly compliance status; escalates unresolved SLA breaches to CISO |
| **Security Analyst / Vulnerability Management Team** | Monitors patch sources and threat intelligence; classifies patches by severity; initiates patch tracking records; conducts verification scanning; generates compliance reports |
| **Patch Management Team / IT Operations** | Tests patches in test environment; deploys patches to production per approved change requests; documents all deployment activities; reports deployment status |
| **System / Application Owner** | Approves patching of assigned systems; participates in scheduling maintenance windows; requests exceptions when needed; accepts risk during exception periods |
| **Change Advisory Board (CAB)** | Reviews and approves standard and expedited change requests for patch deployments; maintains change records |
| **[MSSP / MDR Provider]** | Assists with threat intelligence monitoring; may participate in patch advisory and verification depending on contract scope |

---

## 12. Tool Requirements

The following tools are required to support this policy. Tool selection and procurement are the responsibility of [IT Director / CISO]:

| Tool Category | Purpose | Current Tool |
|---------------|---------|--------------|
| **Vulnerability Scanner** | Identifies unpatched vulnerabilities across all in-scope assets; verifies remediation | [e.g., Tenable.sc / Qualys / Rapid7 InsightVM] |
| **Patch Management Platform** | Automates patch discovery, deployment, and compliance reporting for endpoints and servers | [e.g., Microsoft SCCM / Endpoint Manager, Ivanti, Jamf (macOS/iOS), ManageEngine Patch Manager Plus] |
| **Asset Management / CMDB** | Authoritative inventory of all in-scope assets; used to confirm patch coverage | [e.g., ServiceNow CMDB, Lansweeper, custom CMDB] |
| **Change Management System** | Tracks change requests, approvals, and post-implementation reviews for all patch deployments | [e.g., ServiceNow, Jira Service Management, Freshservice] |
| **GRC Platform / Exception Tracking** | Manages exception requests, approvals, compensating control documentation, and compliance tracking | [e.g., ServiceNow GRC, Archer, custom tracker] |
| **Threat Intelligence Platform** | Provides early warning of newly disclosed vulnerabilities and active exploitation | [e.g., Recorded Future, Mandiant Advantage, CISA KEV catalog, AlienVault OTX] |
| **MDM Platform** | Manages patching of corporate mobile devices | [e.g., Microsoft Intune, Jamf Pro, VMware Workspace ONE] |

Tool configurations must ensure that:
- Scan coverage meets or exceeds 95% of in-scope assets per scan cycle
- Scan frequency aligns with SLA tier requirements (internet-facing systems scanned daily; endpoints weekly minimum)
- Patch compliance data is available for reporting within 24 hours of scan completion

---

## 13. Policy Review

This policy will be reviewed:

- **Annually** — by the CISO, IT Director, and Security Team Lead
- **Following a Critical patch event or security incident related to an unpatched vulnerability** — to assess policy adequacy
- **Following significant changes** to the technology environment (e.g., major new platform adoption, cloud migration, M&A activity)
- **Following any regulatory audit finding** related to patch management or vulnerability remediation
- **Following significant changes to applicable frameworks** (CIS Controls updates, NIST SP 800-40 revisions)

Proposed changes are submitted to [CISO / Policy Review Committee] and require approval per Section 14.

---

## 14. Approval and Signatures

| Role | Name | Signature | Date |
|------|------|-----------|------|
| CISO | [CISO Name] | _________________________ | [Date] |
| IT Director | [IT Director Name] | _________________________ | [Date] |
| CTO | [CTO Name] | _________________________ | [Date] |
| Executive Sponsor | [Executive Sponsor Name] | _________________________ | [Date] |
| Policy Author | [Author Name / Consulting Firm] | _________________________ | [Date] |

---

*This policy is confidential and intended for internal use by [Client Name] and authorized personnel only. Unauthorized distribution is prohibited.*

*Document ID: [DOC-PMP-001] | Classification: [Confidential / Internal] | Related Documents: DOC-VSLA-001, DOC-ZDR-001*
