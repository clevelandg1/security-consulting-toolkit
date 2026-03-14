# Security Consulting Engagement — Discovery Questionnaire

**Client Name:** [Client Name]
**Prepared For:** [Primary Contact Name and Title]
**Classification:** Confidential
**Date Issued:** [Date Issued]
**Return To:** [Consultant Name] — [Consultant Email]
**Return By:** [Requested Return Date]

---

## Introduction

This questionnaire is the first step in establishing a shared understanding of your current security environment, your organization's priorities, and the context in which we will be working together. Your responses directly inform how we baseline your program, where we focus our initial assessment activities, and how we align our advisory recommendations to your business goals.

All information provided in this questionnaire is handled in strict confidence and is used solely for the purpose of scoping and executing this security engagement. Responses will not be shared outside the consulting team without your explicit written authorization.

There are no right or wrong answers. Please answer as accurately as your current knowledge allows — honest responses about gaps and challenges are far more useful than aspirational answers. Where you are uncertain, note that uncertainty; it helps us prioritize where to look first.

---

## Instructions for Completing This Questionnaire

- Complete all sections that apply to your organization. Mark questions as N/A where genuinely not applicable.
- Where a question asks for a list, provide as much detail as you have available. We can fill in gaps during the kickoff interview.
- For Yes/No questions, please circle or bold your answer, then add any relevant context in the space provided.
- You may distribute individual sections to the subject-matter experts best positioned to answer them (e.g., IT lead, security engineer, compliance manager).
- Return the completed questionnaire to the consultant listed above by the date indicated.
- If you have questions about any item, contact [Consultant Name] at [Consultant Email] before completing that section.

**Estimated Completion Time:** 60–90 minutes (may be distributed across multiple respondents)

---

## Section 1: Security Goals and Strategic Objectives

*This section helps us understand what matters most to your organization and ensures our engagement is aligned to your business priorities from day one.*

---

**1.1 What are your top 3 security priorities for the next 12 months?**

1. _______________________________________________

2. _______________________________________________

3. _______________________________________________

---

**1.2 What security outcomes would make this engagement a success from your perspective?**

_______________________________________________
_______________________________________________
_______________________________________________

---

**1.3 What is your single biggest security concern today?**

_______________________________________________
_______________________________________________
_______________________________________________

---

**1.4 Are there upcoming security initiatives, programs, or projects we should be aware of? (e.g., a new platform rollout, a planned cloud migration, an upcoming audit)**

_______________________________________________
_______________________________________________
_______________________________________________

---

**1.5 What compliance frameworks or regulations must your organization adhere to? (check all that apply)**

- [ ] PCI DSS — Payment Card Industry Data Security Standard
- [ ] HIPAA / HITECH — Health Insurance Portability and Accountability Act
- [ ] SOC 2 Type I or Type II
- [ ] ISO 27001
- [ ] NIST Cybersecurity Framework (CSF)
- [ ] CMMC — Cybersecurity Maturity Model Certification (DoD)
- [ ] GDPR — General Data Protection Regulation
- [ ] CCPA or other U.S. state privacy regulations
- [ ] NERC CIP (energy / utilities)
- [ ] FFIEC (financial institutions)
- [ ] Other state or industry regulations: _______________________________________________
- [ ] None currently required

---

**1.6 What are your upcoming audit or certification deadlines?**

| Framework / Audit | Deadline / Target Date | Internal or External Auditor | Current Status |
|------------------|------------------------|------------------------------|----------------|
| | | | |
| | | | |
| | | | |

---

## Section 2: Current Security Tools and Technology

*This section gives us visibility into your existing security technology stack so we know what we are working with, what integrations are possible, and where coverage gaps may exist.*

---

**2.1 What vulnerability scanning tools does your organization currently use? (check all that apply)**

- [ ] Qualys — modules in use: _______________________________________________
- [ ] Tenable / Nessus — version or product: _______________________________________________
- [ ] Rapid7 InsightVM / Nexpose
- [ ] CrowdStrike Falcon Spotlight
- [ ] Microsoft Defender Vulnerability Management
- [ ] OpenVAS / Greenbone
- [ ] Other: _______________________________________________
- [ ] None currently in use

If in use, describe the current scan frequency and coverage:

_______________________________________________
_______________________________________________

---

**2.2 Do you have a SIEM (Security Information and Event Management) platform?**

[ ] Yes [ ] No

If yes:

- SIEM Platform: _______________________________________________
- How long has it been deployed? _______________________________________________
- Who manages it (internal team / MSSP / vendor managed)? _______________________________________________
- Approximately how many log sources are currently connected? _______________________________________________
- Is it tuned and generating actionable alerts? [ ] Yes [ ] No [ ] Partially

---

**2.3 Do you have an EDR or XDR solution deployed?**

[ ] Yes [ ] No

If yes:

- Platform: _______________________________________________
- What percentage of endpoints have the agent deployed? _______ %
- Who monitors and responds to EDR alerts? _______________________________________________

---

**2.4 Do you have a patch management tool in place?**

[ ] Yes [ ] No

If yes:

- Tool / Platform: _______________________________________________
- Does it cover servers, workstations, and laptops? _______________________________________________
- Are third-party application patches managed through it? [ ] Yes [ ] No

---

**2.5 What ticketing / IT service management (ITSM) system do you use?**

- [ ] ServiceNow
- [ ] Jira / Jira Service Management
- [ ] BMC Remedy
- [ ] Freshservice
- [ ] Zendesk
- [ ] Other: _______________________________________________
- [ ] No formal ticketing system

Are security vulnerabilities tracked as tickets in this system? [ ] Yes [ ] No [ ] Sometimes

---

**2.6 What firewall and network security tools are currently in place?**

| Tool / Platform | Vendor | Version / Generation | Managed By |
|----------------|--------|---------------------|------------|
| Perimeter Firewall | | | |
| Next-Gen Firewall (NGFW) | | | |
| Web Application Firewall (WAF) | | | |
| IDS / IPS | | | |
| DNS Security / Filtering | | | |
| Email Security Gateway | | | |
| VPN / Remote Access | | | |
| Other: | | | |

---

**2.7 Do you have a vulnerability management program today?**

[ ] Yes — formal, documented program
[ ] Partially — some elements exist but it is not formalized
[ ] No — ad hoc scanning only

Describe the current state of your vulnerability management program:

_______________________________________________
_______________________________________________
_______________________________________________

---

## Section 3: Vulnerability Tracking and Management

*This section establishes your current vulnerability management process baseline — where things stand today, not where you want them to be.*

---

**3.1 How are vulnerabilities currently tracked after they are identified? (check primary method)**

- [ ] Spreadsheet / manual tracking
- [ ] Ticketing system (specify above in 2.5)
- [ ] Within the vulnerability scanner platform only
- [ ] Dedicated VM platform with tracking capabilities
- [ ] Not formally tracked
- [ ] Other: _______________________________________________

---

**3.2 Do you have defined SLAs for vulnerability remediation?**

[ ] Yes [ ] No

If yes, list your current SLA definitions:

| Severity Level | Remediation SLA Target |
|---------------|------------------------|
| Critical | |
| High | |
| Medium | |
| Low | |
| Informational | |

Are SLAs currently being met? [ ] Yes [ ] No [ ] Unknown — we do not measure this

---

**3.3 How frequently do you conduct vulnerability scans? (check primary cadence)**

- [ ] Continuously (always-on scanning)
- [ ] Weekly
- [ ] Monthly
- [ ] Quarterly
- [ ] Ad hoc (on demand, no set schedule)
- [ ] Rarely / only when required for audits

Are scans conducted on a different schedule for different asset types? If so, describe:

_______________________________________________

---

**3.4 What percentage of your known assets are currently covered by vulnerability scans?**

Estimated scan coverage: _______ % of known assets

Are there asset categories you know are NOT being scanned (e.g., cloud, OT, remote laptops)?

_______________________________________________
_______________________________________________

---

**3.5 Who is responsible for remediating vulnerabilities? (check all that apply)**

- [ ] Internal IT / sysadmin team
- [ ] Internal development team (for application vulnerabilities)
- [ ] Managed service provider (outsourced)
- [ ] Business unit owners for specific systems
- [ ] No clearly defined owner — varies by asset
- [ ] Other: _______________________________________________

Is there a formal handoff process from the security team to the remediation team?

[ ] Yes [ ] No — describe current process: _______________________________________________

---

**3.6 What is your single biggest challenge with vulnerability remediation today?**

_______________________________________________
_______________________________________________
_______________________________________________

---

## Section 4: Asset Inventory and Criticality

*Knowing what you have, where it is, and how critical it is to the business is foundational. This section identifies the current state of your asset management capability.*

---

**4.1 Do you maintain a formal asset inventory?**

[ ] Yes [ ] No [ ] Partial / informal

If yes, what tool or system is used to maintain it?

_______________________________________________

How frequently is it updated? _______________________________________________

---

**4.2 How confident are you in the accuracy and completeness of your current asset inventory?**

Rating (circle one): 1 — 2 — 3 — 4 — 5 — 6 — 7 — 8 — 9 — 10

*(1 = Very low confidence; 10 = Complete and highly accurate)*

What factors limit your confidence in the current inventory?

_______________________________________________
_______________________________________________

---

**4.3 Do you have asset criticality ratings defined for your assets?**

[ ] Yes — formally defined and documented
[ ] Partially — some systems are tagged, but not systematically
[ ] No — no criticality classification in place

If yes, describe the criticality tiers or methodology used:

_______________________________________________
_______________________________________________

---

**4.4 What are your most critical business systems? (list the systems whose loss would cause the greatest operational, financial, or reputational impact)**

| System / Application Name | Type | Why It Is Critical |
|--------------------------|------|--------------------|
| | | |
| | | |
| | | |
| | | |
| | | |

---

**4.5 Does your asset inventory include the following? (check all that apply)**

- [ ] On-premises servers (Windows and Linux)
- [ ] End-user workstations and laptops
- [ ] Network devices (switches, routers, firewalls)
- [ ] Cloud VMs and cloud-hosted infrastructure (AWS, Azure, GCP)
- [ ] Containers and Kubernetes clusters
- [ ] SaaS applications in use by the organization
- [ ] Mobile devices (corporate-managed)
- [ ] OT / ICS / operational technology systems
- [ ] IoT devices
- [ ] None of the above — no formal inventory

---

## Section 5: External Asset Visibility

*Your external attack surface is what threat actors see when they look at your organization from the internet. This section helps us understand your awareness of that exposure.*

---

**5.1 Do you know all of your organization's external and internet-facing assets?**

[ ] Yes, we have a complete and current picture
[ ] Mostly — we believe we know the primary assets but may have gaps
[ ] No — we do not have a complete view of our external exposure

How confident are you in your external asset visibility? (1 = Not at all; 10 = Fully confident)

Confidence rating: _______

---

**5.2 Do you use an Attack Surface Management (ASM) tool?**

[ ] Yes [ ] No

If yes, which tool? _______________________________________________

What does it cover (subdomains, IPs, cloud assets, certificates, etc.)? _______________________________________________

---

**5.3 When was the last external vulnerability scan or external penetration test conducted?**

External vulnerability scan: _______________________________________________

External penetration test: _______________________________________________

Was a report produced? [ ] Yes [ ] No — do you have a copy available? [ ] Yes [ ] No

---

**5.4 Have you experienced any incidents or concerns related to shadow IT or unknown external exposure in the past 12 months?**

[ ] Yes [ ] No

If yes, please describe:

_______________________________________________
_______________________________________________

---

## Section 6: Log Collection and SIEM Coverage

*Log coverage is the foundation of detection capability. This section identifies what is being collected, what is not, and where detection gaps may exist.*

---

**6.1 What log sources are currently feeding your SIEM or log management platform? (check all that apply)**

- [ ] Perimeter / next-generation firewall
- [ ] Active Directory (Windows Security Event Log)
- [ ] Azure Active Directory / Entra ID
- [ ] Endpoint / EDR (workstations and servers)
- [ ] VPN / remote access gateway
- [ ] Email security gateway (inbound/outbound mail logs)
- [ ] DNS logs
- [ ] DHCP logs
- [ ] Web proxy / secure web gateway
- [ ] Cloud platform logs (AWS CloudTrail, Azure Activity Log, GCP Audit Logs)
- [ ] Cloud workload logs (EC2, Azure VMs, GCP VMs)
- [ ] SaaS application logs (M365, Salesforce, etc.)
- [ ] Database activity logs
- [ ] Application logs (custom or business applications)
- [ ] Network flow logs (NetFlow, sFlow, VPC Flow Logs)
- [ ] Identity provider / SSO (Okta, Ping, etc.)
- [ ] IDS / IPS
- [ ] Other: _______________________________________________
- [ ] No SIEM in place

---

**6.2 What percentage of your environment generates logs that are actively collected?**

Estimated log collection coverage: _______ % of environment

---

**6.3 Are log sources normalized and parsed correctly in your SIEM?**

[ ] Yes — fully normalized and parsed
[ ] Partially — most sources are, but some are raw / unparsed
[ ] No — minimal normalization in place
[ ] Unknown

---

**6.4 Who reviews and responds to SIEM alerts?**

- [ ] Internal security operations team (SOC)
- [ ] IT team (non-dedicated security role)
- [ ] Managed SIEM / MDR provider — provider name: _______________________________________________
- [ ] Alerts are not actively reviewed
- [ ] Other: _______________________________________________

Estimated average time to review / respond to a high-priority SIEM alert: _______________________________________________

---

**6.5 What is your log retention period?**

Hot / searchable retention (online): _______________________________________________
Cold / archive retention (offline or compressed): _______________________________________________

Is the retention period sufficient for your regulatory requirements? [ ] Yes [ ] No [ ] Unknown

---

**6.6 Are there log sources you know you are missing or not yet collecting?**

[ ] Yes [ ] No

If yes, list known gaps:

_______________________________________________
_______________________________________________

---

## Section 7: Incident Response and SLAs

*This section establishes the state of your incident response readiness and the service level commitments that govern your security operations.*

---

**7.1 Do you have a documented incident response plan?**

[ ] Yes — formal, documented, and approved
[ ] Partially — informal guidance or runbooks exist
[ ] No

If yes, when was it last reviewed or updated? _______________________________________________

When was it last tested (tabletop exercise or actual incident)? _______________________________________________

---

**7.2 Have you experienced a security incident in the past 12 months?**

[ ] Yes [ ] No [ ] Prefer not to say

If yes, briefly describe the nature of the incident (no sensitive details required):

_______________________________________________
_______________________________________________

What was the approximate business impact and recovery time?

_______________________________________________

---

**7.3 What is your current process when a critical vulnerability is discovered (e.g., a CVSS 9.0+ or actively exploited CVE)?**

_______________________________________________
_______________________________________________
_______________________________________________

---

**7.4 Do you have formal escalation paths for security events?**

[ ] Yes — documented and tested [ ] Yes — documented but not tested [ ] No

Who is the first point of contact for a security event outside business hours?

_______________________________________________

---

**7.5 What are your current remediation SLAs, if any? (repeat or confirm from Section 3.2 if already provided)**

| Severity | SLA Target | Measured? | Met Consistently? |
|----------|-----------|-----------|-------------------|
| Critical | | [ ] Yes [ ] No | [ ] Yes [ ] No [ ] Unknown |
| High | | [ ] Yes [ ] No | [ ] Yes [ ] No [ ] Unknown |
| Medium | | [ ] Yes [ ] No | [ ] Yes [ ] No [ ] Unknown |
| Low | | [ ] Yes [ ] No | [ ] Yes [ ] No [ ] Unknown |

---

**7.6 Who would you contact first in a security emergency (e.g., active ransomware, confirmed breach)?**

| Role | Name | Contact Method |
|------|------|----------------|
| First call — internal | | |
| Second call — internal | | |
| Legal counsel | | |
| External IR firm (if retained) | | |
| Cyber insurance carrier | | |
| Law enforcement (if applicable) | | |

---

## Section 8: Business and Organizational Context

*Understanding the people, structure, and culture around security helps us tailor our engagement to work effectively within your organization.*

---

**8.1 How large is your IT team? Your security team specifically?**

Total IT staff (approximate): _______________

Dedicated security staff (approximate): _______________

Are any security functions outsourced? [ ] Yes [ ] No

If yes, describe what is outsourced and to whom:

_______________________________________________

---

**8.2 Do you have a dedicated security team, or is security handled by IT generalists?**

- [ ] Dedicated security team with defined security roles
- [ ] Security responsibilities shared among IT generalists
- [ ] Hybrid — a security lead or manager with generalist IT support
- [ ] Security is primarily outsourced to an MSSP
- [ ] Other: _______________________________________________

---

**8.3 Who is your executive security sponsor?**

| Role | Name | Title |
|------|------|-------|
| Executive Sponsor | | [ ] CISO [ ] CTO [ ] CIO [ ] VP IT [ ] Other: ___ |
| Reports to | | |

Does your security team have direct access to executive leadership for escalations? [ ] Yes [ ] No

---

**8.4 How is your security budget structured?**

- [ ] Dedicated security budget (separate from IT)
- [ ] Security budget is part of the overall IT budget
- [ ] No formal security budget — funded on a project / request basis
- [ ] Unknown / handled outside my visibility

Is there budget available for remediation activities identified during this engagement?

[ ] Yes [ ] No [ ] Subject to approval

---

**8.5 Have you had any security audits, assessments, or penetration tests in the past 24 months?**

[ ] Yes [ ] No

If yes:

| Assessment Type | Date | Conducted By | Key Findings / Themes |
|----------------|------|--------------|----------------------|
| | | | |
| | | | |
| | | | |

Have prior findings been remediated? [ ] Yes — fully [ ] Partially [ ] No [ ] Unknown

Are prior reports available for our review? [ ] Yes [ ] No

---

## Questionnaire Completion

Thank you for taking the time to complete this questionnaire. Your responses are essential to a productive kickoff and an effective baseline assessment.

---

**Completed By:**

Name: _______________________________________________
Title: _______________________________________________
Department: _______________________________________________
Date Completed: _______________________________________________

**If multiple people contributed to this response, list all contributors:**

| Name | Title | Sections Completed |
|------|-------|-------------------|
| | | |
| | | |
| | | |

---

**Best way to follow up on these responses:**

- [ ] Email — address: _______________________________________________
- [ ] Phone call — number: _______________________________________________
- [ ] Scheduled meeting — preferred days/times: _______________________________________________

---

**Is there anything else we should know before our kickoff meeting?**

_______________________________________________
_______________________________________________
_______________________________________________
_______________________________________________

---

*Return this completed questionnaire to [Consultant Name] at [Consultant Email] by [Return Date]. All information is handled as Confidential and used solely for the purpose of this security engagement.*
