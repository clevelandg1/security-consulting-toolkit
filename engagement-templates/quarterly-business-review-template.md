# Quarterly Business Review

---

**Client Name:** [Client Name]
**Review Period:** Q[X] [Year] — [Month DD, YYYY] through [Month DD, YYYY]
**QBR Date:** [Date of Meeting]
**Prepared By:** [Consultant Name] | [Firm Name]
**Client Attendees:** [List names and titles]
**Consultant Attendees:** [List names and titles]
**Document Version:** [1.0]

---

## Table of Contents

1. [Executive Summary](#section-1-executive-summary)
2. [Security Posture Metrics](#section-2-security-posture-metrics)
3. [Measurable Security Improvements](#section-3-measurable-security-improvements)
4. [CIS Controls Progress](#section-4-cis-controls-progress)
5. [Gap Analysis](#section-5-gap-analysis)
6. [Expansion Opportunities](#section-6-expansion-opportunities)
7. [Next Quarter Planning](#section-7-next-quarter-planning)
8. [Action Items](#section-8-action-items)

---

## Section 1: Executive Summary

*Provide a one-paragraph snapshot of the quarter. Cover: the overall arc of progress, the most significant accomplishments, the most important risks still open, and a forward-looking statement about the next quarter. This section should be readable by a non-technical executive in 60 seconds.*

> **[Draft — customize for the Client]**
>
> During Q[X] [Year], [Client Name] made measurable progress in [primary focus area, e.g., vulnerability remediation and SIEM log coverage expansion]. Critical vulnerability count decreased from [X] to [Y], representing a [Z%] reduction over the quarter, and mean time to remediate critical findings improved from [X days] to [Y days]. [N] new log sources were onboarded, significantly improving detection coverage across [cloud / endpoint / identity]. Key accomplishments included [specific win 1] and [specific win 2]. Open risks include [primary remaining gap] and [secondary remaining gap], both of which are prioritized in next quarter's plan. Q[X+1] will focus on [primary objective], [secondary objective], and [tertiary objective], with the goal of [overarching outcome, e.g., achieving full SLA compliance and completing the NIST CSF gap remediation roadmap].

---

## Section 2: Security Posture Metrics

This table tracks key security metrics quarter over quarter. All figures should be sourced from the vulnerability management platform, SIEM, and asset inventory tooling. Include citations where data sources differ.

| Metric | Previous Quarter (Q[X-1]) | This Quarter (Q[X]) | Trend | Target |
|--------|:-------------------------:|:-------------------:|:-----:|:------:|
| Total vulnerabilities open | [#] | [#] | [↑ ↓ →] | [#] |
| Critical vulnerabilities open | [#] | [#] | [↑ ↓ →] | [#] |
| High vulnerabilities open | [#] | [#] | [↑ ↓ →] | [#] |
| Medium vulnerabilities open | [#] | [#] | [↑ ↓ →] | [#] |
| Mean time to remediate — Critical (days) | [# days] | [# days] | [↑ ↓ →] | [# days] |
| Mean time to remediate — High (days) | [# days] | [# days] | [↑ ↓ →] | [# days] |
| SLA compliance % — Critical | [%] | [%] | [↑ ↓ →] | [%] |
| SLA compliance % — High | [%] | [%] | [↑ ↓ →] | [%] |
| Assets in scope / scanned (coverage %) | [%] | [%] | [↑ ↓ →] | [%] |
| Log sources active in SIEM | [#] | [#] | [↑ ↓ →] | [#] |
| Open action items (from prior quarter) | [#] | [# completed / # remaining] | [↑ ↓ →] | 100% complete |
| [Custom metric] | [#] | [#] | [↑ ↓ →] | [target] |

**Trend Key:** ↑ = Improving &nbsp;&nbsp; ↓ = Declining &nbsp;&nbsp; → = Stable

**Metric Notes / Data Sources:**

> [Document where each metric was sourced from and any caveats — e.g., "Total vuln count pulled from Tenable as of [date]. Excludes [X] assets that were offline during the scan window."]

---

## Section 3: Measurable Security Improvements

Document 3–5 concrete accomplishments from this quarter with before/after data. Use business-impact language alongside technical detail. These should be directly shareable with executive leadership.

**Improvement 1:**

| | Detail |
|---|--------|
| **What improved** | [e.g., Vulnerability remediation SLA compliance for Critical severity] |
| **Before** | [e.g., 42% of Critical vulnerabilities remediated within the 15-day SLA window at the start of Q3] |
| **After** | [e.g., 81% of Critical vulnerabilities remediated within SLA by end of Q3] |
| **How it happened** | [e.g., Implemented weekly remediation status meetings between security and IT; created automated Jira tickets for Critical findings] |
| **Business impact** | *[e.g., "The window of exploitability for your highest-severity vulnerabilities has been cut nearly in half — materially reducing the risk of a breach during the period between discovery and patching."]*  |

---

**Improvement 2:**

| | Detail |
|---|--------|
| **What improved** | [e.g., SIEM log source coverage] |
| **Before** | [e.g., 8 log sources active; no cloud coverage; no identity provider logs] |
| **After** | [e.g., 13 log sources active; AWS CloudTrail and GuardDuty onboarded; Azure AD sign-in logs onboarded] |
| **How it happened** | [e.g., Prioritized log sources using risk-based gap analysis delivered in Q2; Client SIEM admin executed onboarding with advisory guidance] |
| **Business impact** | *[e.g., "Your security team now has visibility into cloud and identity events that represent the most common initial access vectors in modern attacks — events you were previously unable to detect."]*  |

---

**Improvement 3:**

| | Detail |
|---|--------|
| **What improved** | [e.g., Incident Response plan completeness and readiness] |
| **Before** | [e.g., IR plan existed but was 3 years out of date; had never been tested] |
| **After** | [e.g., IR plan updated and reviewed by stakeholders; tabletop exercise completed with security team and IT leadership] |
| **How it happened** | [e.g., IR plan review completed in Month [X]; tabletop exercise facilitated by [Consultant] on [date]] |
| **Business impact** | *[e.g., "Your team now has a practiced, tested response process. In the event of an incident, you can expect faster containment, better coordination, and reduced overall impact."]*  |

---

**Improvement 4:**

| | Detail |
|---|--------|
| **What improved** | [e.g., Asset inventory completeness] |
| **Before** | [e.g., ~60% of assets documented; no criticality classification] |
| **After** | [e.g., ~90% of assets documented; criticality classification applied to all Tier 1 and Tier 2 assets] |
| **How it happened** | [e.g., Asset discovery scan supplemented by review of Active Directory, CMDB, and cloud console exports] |
| **Business impact** | *[e.g., "Remediation teams can now reliably prioritize patching based on business criticality — ensuring that the systems that matter most are always protected first."]*  |

---

**Improvement 5:**

| | Detail |
|---|--------|
| **What improved** | [Description] |
| **Before** | [Baseline state] |
| **After** | [Current state] |
| **How it happened** | [Process / activity] |
| **Business impact** | *[Business-impact statement]* |

---

## Section 4: CIS Controls Progress

Track progress against CIS Controls (or the applicable framework) that were in scope this quarter. Focus on controls where meaningful progress was made or where current status changed.

*Note: Adjust the framework column to match the applicable standard for this Client (NIST CSF, ISO 27001, SOC 2 TSC, PCI-DSS, etc.).*

| CIS Control | Control Name | Status — Start of Quarter | Status — End of Quarter | Progress Made This Quarter |
|:-----------:|--------------|:-------------------------:|:-----------------------:|---------------------------|
| CIS 1 | Inventory and Control of Enterprise Assets | Partial | Implemented | Asset inventory expanded to 90% coverage; criticality classifications applied |
| CIS 2 | Inventory and Control of Software Assets | Not Started | Partial | Software inventory initiated; review of authorized vs. unauthorized software ongoing |
| CIS 3 | Data Protection | Partial | Partial | Data classification policy reviewed; gaps in encryption-at-rest identified |
| CIS 4 | Secure Configuration of Enterprise Assets | Not Started | Partial | Configuration baselines defined for Windows servers; remediation backlog identified |
| CIS 5 | Account Management | Partial | Implemented | Privileged account audit completed; stale accounts removed; MFA enforced for admin accounts |
| CIS 6 | Access Control Management | Not Started | Not Started | Scheduled for Q[X+1] |
| CIS 7 | Continuous Vulnerability Management | Partial | Implemented | SLAs defined; scanning frequency increased; backlog tracking implemented |
| CIS 8 | Audit Log Management | Partial | Partial | 5 new log sources onboarded; gaps in cloud and email logging remain |
| CIS 9 | Email and Web Browser Protections | Not Started | Not Started | Scheduled for Q[X+1] |
| CIS 10 | Malware Defenses | Implemented | Implemented | No changes; EDR coverage at 98% of endpoints |
| CIS 11 | Data Recovery | Partial | Partial | Backup review completed; restoration testing not yet performed |
| CIS 12 | Network Infrastructure Management | Not Started | Partial | Network device inventory completed; configuration review scheduled |
| CIS 13 | Network Monitoring and Defense | Not Started | Partial | IDS/IPS log sources added to SIEM; detection rules in development |
| [Additional control] | | | | |

**Status Key:**
- **Not Started** — Work has not yet begun
- **Partial** — Some implementation in place but gaps remain
- **Implemented** — Control fully implemented for this environment
- **N/A** — Not applicable to this Client's environment

**Framework Notes:**

> [Any notes on framework interpretation, scoping decisions, or evidence collected this quarter]

---

## Section 5: Gap Analysis

This section documents open security gaps as of the end of this quarter, ranked by risk. For each gap, provide context on why it matters and a recommended remediation action.

| # | Gap | Affected Area | Risk Rating | Risk Rationale | Recommended Remediation Action | Estimated Effort | Priority |
|---|-----|---------------|:-----------:|----------------|-------------------------------|:----------------:|:--------:|
| 1 | [e.g., Cloud workload visibility — GCP not monitored] | Cloud Security / Detection | Critical | Unmonitored environment represents a complete blind spot for threat detection | Onboard GCP Cloud Audit Logs and Security Command Center findings to SIEM | Medium | Q[X+1] |
| 2 | [e.g., High vulnerability backlog — [X] highs open >60 days] | Vulnerability Management | High | Extended exposure window for exploitable vulnerabilities increases breach likelihood | Implement remediation workflow automation; increase patching cadence for high-severity findings | High | Q[X+1] |
| 3 | [e.g., Application security — no testing performed on customer portal] | Application Security | High | Web-facing application represents a common initial access vector; no current testing program | Perform DAST scan of customer-facing applications; review results with development team | Medium | Q[X+1] |
| 4 | [e.g., External attack surface — no formal EASM process] | External Exposure | Medium | Internet-exposed assets may have undetected vulnerabilities not covered by internal scanning | Implement external vulnerability scanning or EASM tooling; review findings quarterly | Low | Q[X+2] |
| 5 | [e.g., Restoration testing — backups not tested] | Business Continuity | Medium | Untested backups cannot be relied upon for recovery; risk of extended downtime during incident | Schedule and perform backup restoration test for Tier 1 systems | Low | Q[X+1] |
| 6 | [e.g., Detection rule coverage — limited custom rules in SIEM] | Threat Detection | Medium | Default SIEM rules provide limited detection for environment-specific attack patterns | Develop and tune custom detection rules for [priority use cases] | Medium | Q[X+2] |
| 7 | [Additional gap] | | | | | | |

**Risk Rating Key:** Critical | High | Medium | Low

**Gap Analysis Notes:**

> [Space for additional context — e.g., client-specific factors that affect gap prioritization, dependencies, or risk acceptance decisions]

---

## Section 6: Expansion Opportunities

This section identifies opportunities to expand the engagement scope or enhance the Client's security program with additional services. Each item is mapped to the Customer Advisory Framework (CAF) upsell paths.

---

### 6a. Additional Log Sources

**Description:** Onboard additional log sources into the SIEM to close current detection coverage gaps. High-priority candidates based on this Client's environment:
- [e.g., Email security platform (Proofpoint / Defender for Office 365)]
- [e.g., VPN / remote access platform]
- [e.g., Cloud storage access logs (S3, Blob Storage)]
- [e.g., Database activity monitoring]

**Business Case:** *[e.g., "Each new log source closes a specific detection gap. Email logs would enable detection of phishing-based initial access — one of the most common attack entry points. VPN logs would provide visibility into remote access anomalies, which are frequently associated with credential-based attacks."]*

**Recommended Next Step:** [e.g., Prioritize top 3 missing log sources; schedule onboarding sprint for Q[X+1]]

---

### 6b. Cloud Workload Visibility

**Description:** Extend security visibility into cloud environments not currently covered.

| Cloud Provider | Current Coverage | Proposed Addition | Key Benefit |
|----------------|:----------------:|-------------------|-------------|
| AWS | [Full / Partial / None] | [e.g., CloudTrail, GuardDuty, VPC Flow Logs] | Cloud API activity, threat detection, network visibility |
| Azure | [Full / Partial / None] | [e.g., Azure Activity Logs, Defender for Cloud, Entra ID Sign-In Logs] | Hybrid identity visibility, cloud resource monitoring |
| GCP | [Full / Partial / None] | [e.g., Cloud Audit Logs, Security Command Center] | GCP workload and admin activity monitoring |

**Business Case:** *[e.g., "Cloud environments now host [X]% of your critical workloads. Without log coverage in [GCP / Azure], your security team has no ability to detect threats targeting those systems."]*

**Recommended Next Step:** [e.g., Prioritize GCP coverage; scope onboarding project and include in Q[X+1] plan]

---

### 6c. Application Security Testing

**Description:** Introduce structured security testing for web-facing and internal applications, covering areas such as OWASP Top 10, authentication flaws, injection vulnerabilities, and API security.

**Business Case:** *[e.g., "Your customer portal and [internal application] are publicly accessible and represent attack surfaces not covered by your current vulnerability management program. Application-layer testing identifies vulnerabilities that network scanning cannot detect."]*

**Recommended Next Step:** [e.g., Identify top 3 highest-risk applications; scope a DAST engagement or advisory review of existing application security practices]

---

### 6d. Threat Detection & Response

**Description:** Build out detection capabilities beyond log collection — including custom detection rule development, alert triage playbooks, and use-case-based tuning of the SIEM.

**Business Case:** *[e.g., "Your SIEM is currently collecting logs but running primarily on vendor-default rules. Custom detection rules tuned to your environment and threat profile will significantly improve alert fidelity and reduce noise — enabling faster, more accurate detection of real threats."]*

**Recommended Next Step:** [e.g., Prioritize top 5 detection use cases (e.g., credential stuffing, lateral movement, data exfiltration); begin developing and testing custom rules in Q[X+1]]

---

### 6e. Reporting Automation

**Description:** Automate the production of security metrics and executive reporting, reducing manual effort and providing leadership with on-demand visibility into security posture.

**Business Case:** *[e.g., "Currently, producing the monthly vulnerability metrics report and QBR deck requires [X hours] of manual effort. Automating this through your existing tooling (e.g., SIEM dashboards, vulnerability platform reports, BI tool integration) would save time and provide leadership with real-time visibility."]*

**Recommended Next Step:** [e.g., Define required metrics and reporting cadence; evaluate automation capabilities within current tool stack; design dashboard prototype]

---

### 6f. Remediation Workflow & Ticketing Integration

**Description:** Connect the vulnerability management platform directly to the Client's ticketing system (ServiceNow, Jira, or similar) to automate remediation ticket creation, tracking, and SLA enforcement.

**Business Case:** *[e.g., "Today, remediation tickets are created manually after each scan — a process that introduces delay and creates tracking gaps. A direct integration between [Tenable / Qualys / Rapid7] and [Jira / ServiceNow] would automate ticket creation, assign owners based on asset criticality, and enforce SLA alerts automatically."]*

**Recommended Next Step:** [e.g., Review integration capabilities between [vuln management tool] and [ticketing platform]; define field mapping and workflow requirements; pilot with Critical and High severity findings]

---

## Section 7: Next Quarter Planning

### 7a. Q[X+1] Objectives

| # | Objective | Success Metric | Priority |
|---|-----------|---------------|:--------:|
| 1 | [e.g., Achieve 90%+ SLA compliance for Critical vulnerability remediation] | [e.g., SLA compliance % = 90% by end of Q[X+1]] | High |
| 2 | [e.g., Onboard GCP log sources into SIEM] | [e.g., GCP Cloud Audit Logs and SCC findings active in SIEM] | High |
| 3 | [e.g., Complete CIS Controls 6 and 9 implementation] | [e.g., Status = "Implemented" for both controls by quarter end] | Medium |
| 4 | [e.g., Perform backup restoration test for Tier 1 systems] | [e.g., Test completed; results documented] | Medium |
| 5 | [e.g., Develop 5 custom detection rules for priority use cases] | [e.g., Rules created, tuned, and in active monitoring] | Medium |
| 6 | [Additional objective] | | |

### 7b. Key Milestones

| Milestone | Description | Target Completion Date | Owner |
|-----------|-------------|:----------------------:|-------|
| [e.g., GCP onboarding kickoff] | [Confirm scope and begin log source configuration] | [Date] | [Client IT / Consultant] |
| [e.g., Remediation SLA review] | [Mid-quarter check on SLA compliance trajectory] | [Date] | [Consultant] |
| [e.g., CIS Controls 6 & 9 review] | [Assess current state and develop implementation plan] | [Date] | [Consultant] |
| [e.g., Backup restoration test] | [Schedule and perform test; document results] | [Date] | [Client IT] |
| [e.g., Q[X+1] monthly meetings] | [Three advisory meetings: [Month], [Month], [Month]] | [Dates] | [Both] |
| [e.g., QBR #[N] preparation] | [Draft QBR report and share with Client for review] | [5 days before QBR] | [Consultant] |

### 7c. Dependencies

| Dependency | Description | Risk if Not Resolved |
|------------|-------------|----------------------|
| [e.g., GCP service account access] | [Client must create and share service account credentials for log forwarding] | [GCP onboarding delayed] |
| [e.g., IT team bandwidth] | [Remediation cadence for Q[X+1] objectives dependent on IT patching capacity] | [SLA compliance targets may not be achievable] |
| [e.g., Ticketing system integration] | [Jira API access required for remediation workflow integration] | [Manual process continues; delays and tracking gaps persist] |
| [Additional dependency] | | |

---

## Section 8: Action Items

Review this table at the end of the QBR meeting and confirm owners and due dates before closing.

| # | Action Item | Owner | Due Date | Priority | Status |
|---|-------------|-------|----------|:--------:|:------:|
| 1 | Send QBR notes and this action item list to all attendees | [Consultant] | [+3 business days] | High | Open |
| 2 | [e.g., Initiate GCP log source onboarding — provide service account access] | [Client Cloud Team] | [Date] | High | Open |
| 3 | [e.g., Schedule remediation sprint for top [X] high-severity vulnerabilities] | [Client IT / Security] | [Date] | High | Open |
| 4 | [e.g., Begin CIS Controls 6 assessment] | [Consultant] | [Date] | Medium | Open |
| 5 | [e.g., Schedule backup restoration test] | [Client IT] | [Date] | Medium | Open |
| 6 | [e.g., Evaluate Jira integration capabilities with vulnerability management platform] | [Consultant + Client IT] | [Date] | Medium | Open |
| 7 | [e.g., Schedule three monthly advisory meetings for Q[X+1]] | [Consultant] | [Date] | High | Open |
| 8 | [e.g., Confirm Q[X+1] QBR date] | [Both] | [Date] | High | Open |
| 9 | [Additional action item] | [Owner] | [Date] | | Open |
| 10 | [Additional action item] | [Owner] | [Date] | | Open |

---

*Quarterly Business Review | [Client Name] | Q[X] [Year] | Prepared by [Consultant Name] — [Firm Name]*
*Document Version [1.0] | Distribution: [Client Name] Security Leadership and [Firm Name] Engagement Team*
