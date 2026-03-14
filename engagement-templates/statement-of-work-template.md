# Statement of Work

---

**SOW Number:** [SOW-YYYY-NNN]
**Effective Date:** [Effective Date]
**Expiration / End Date:** [End Date]

**Service Provider:**
[Firm Name]
[Address Line 1]
[City, State, ZIP]
[Contact Name] | [Email] | [Phone]

**Client:**
[Client Name]
[Address Line 1]
[City, State, ZIP]
[Primary Contact Name] | [Email] | [Phone]

**Master Services Agreement Reference:** [MSA Number, if applicable — otherwise "N/A"]

---

## Table of Contents

1. [Purpose and Background](#purpose-and-background)
2. [Service Definitions](#service-definitions)
3. [Scope Inclusions and Exclusions](#scope-inclusions-and-exclusions)
4. [Roles and Responsibilities](#roles-and-responsibilities)
5. [Engagement Timeline & Milestones](#engagement-timeline--milestones)
6. [Assumptions and Dependencies](#assumptions-and-dependencies)
7. [Change Management Process](#change-management-process)
8. [Fees and Payment Terms](#fees-and-payment-terms)
9. [Confidentiality and Data Handling](#confidentiality-and-data-handling)
10. [Acceptance Criteria](#acceptance-criteria)
11. [Signatures](#signatures)

---

## 1. Purpose and Background

### Purpose

This Statement of Work ("SOW") governs the delivery of security advisory services by [Firm Name] ("Service Provider") to [Client Name] ("Client"). It defines the specific services to be performed, the deliverables to be produced, the responsibilities of each party, and the terms under which work will be accepted and compensated.

This SOW is entered into in support of the proposal dated [Proposal Date] and incorporates the terms of the Master Services Agreement dated [MSA Date], if applicable.

### Background

[Client Name] is seeking ongoing security advisory support to improve its overall security posture, mature its vulnerability management and log management programs, align security operations with applicable compliance frameworks, and reduce organizational risk through structured, expert guidance.

[Firm Name] will provide these services using a structured advisory methodology grounded in continuous baseline assessment, discovery, gap remediation tracking, and quarterly executive reporting.

*Example background context: "Client recently completed a SOC 2 Type I audit and is preparing for Type II certification. The primary drivers for this engagement are improving vulnerability remediation SLAs, expanding SIEM log coverage, and documenting evidence of continuous security improvement."*

---

## 2. Service Definitions

The following table defines each service line included in this engagement. All services will be performed in accordance with the Customer Advisory Framework (CAF) methodology unless otherwise specified.

| Service Name | Description | Frequency | Primary Deliverable | Acceptance Criteria |
|--------------|-------------|-----------|---------------------|---------------------|
| **Vulnerability Management Advisory** | Review of vulnerability scanning program, backlog analysis, SLA tracking, and remediation prioritization guidance. Includes review of scanning coverage across endpoints, servers, network devices, and cloud assets. | Monthly review; continuous tracking | Monthly Vulnerability Metrics Report | Report delivered within 5 business days of month close; includes open count by severity, age distribution, SLA compliance %, and trend vs. prior month |
| **SIEM / Log Management Advisory** | Assessment and ongoing review of log sources, coverage gaps, detection rule efficacy, and alert triage processes. Includes recommendations for new log source onboarding. | Monthly review; gap report quarterly | Log Coverage Gap Report (quarterly); meeting notes (monthly) | Gap report delivered within 10 business days of quarter close; identifies all active log sources and documents gaps with risk ratings |
| **Security Posture Reviews** | Structured advisory meetings following the CAF meeting format: purpose review, posture overview, discovery, gap identification, improvement recommendations, and action items. | Monthly (standard); as-needed (ad-hoc) | Meeting Notes & Action Item Tracker update | Notes delivered within 5 business days of meeting; action items include owner and due date |
| **Quarterly Business Reviews (QBR)** | Executive-level review of security posture trends, metrics, remediation progress, gap analysis, and next-quarter planning. Aligned to CAF quarterly review cadence. | Quarterly | QBR Report / Presentation | Delivered at least 5 business days before scheduled QBR meeting; approved by Client primary contact |
| **Incident Response Support** | Advisory support during or following a security incident, including IR plan review, tabletop facilitation, post-incident review, and lessons-learned documentation. Not a managed response service. | As-needed (within scope hour allocation) | IR After-Action Report (when applicable) | After-Action Report delivered within 10 business days of incident close; reviewed and acknowledged by Client |
| **Reporting & Documentation** | Production and maintenance of all written deliverables, including baseline reports, gap analyses, metrics reports, roadmaps, and the action item tracker. | Continuous | All listed deliverables | Deliverables conform to agreed templates; delivered within timeframes specified in Section 5 |

---

## 3. Scope Inclusions and Exclusions

### 3.1 Scope Inclusions

The following activities and environments are explicitly in scope for this engagement:

**Advisory & Analysis**
- Vulnerability management program review and advisory
- SIEM / log management gap analysis and advisory
- Asset inventory review and criticality assessment advisory
- External attack surface review (advisory, not active testing)
- Cloud security advisory for [AWS / Azure / GCP — select applicable]
- Incident response plan review and advisory support
- Compliance framework alignment (applicable framework: [SOC 2 / NIST CSF / CIS Controls / PCI-DSS / HIPAA / ISO 27001])

**Environments**
- On-premises infrastructure (as documented in Client asset inventory)
- Cloud environments: [specify cloud providers in scope]
- SaaS applications: [specify if applicable, e.g., Microsoft 365, Salesforce]
- Remote/hybrid endpoint population

**Reporting**
- All deliverables described in Section 2
- Ad-hoc reporting within the monthly hour allocation

### 3.2 Scope Exclusions

The following items are explicitly excluded from this SOW. Any request to perform excluded activities will require a written Change Order (see Section 7):

- Hands-on remediation, patching, or configuration changes
- Penetration testing, red team exercises, or adversarial simulation
- Security tool procurement, licensing, deployment, or administration
- 24/7 managed security monitoring or SOC-as-a-service
- eDiscovery, forensic investigation, or legal proceedings support
- Regulatory certification, audit preparation services, or formal audit support
- Development of custom software or security tooling
- Physical security assessment
- [Any additional client-specific exclusions]

---

## 4. Roles and Responsibilities

### 4.1 Service Provider Responsibilities

| Responsibility | Detail |
|----------------|--------|
| Engagement delivery | Deliver all services described in Section 2 within agreed timelines |
| Meeting facilitation | Facilitate all advisory meetings and QBRs per the CAF meeting structure |
| Deliverable production | Produce all deliverables in the agreed formats and within the agreed timeframes |
| Action item tracking | Maintain and distribute the Action Item Tracker following each meeting |
| Discovery execution | Conduct and document all pre-engagement and ongoing discovery questions |
| Gap analysis | Identify, prioritize, and document security gaps with recommended remediation actions |
| Escalation | Escalate critical risk findings to Client primary contact within [1] business day of identification |
| Availability | Maintain availability for scheduled meetings and respond to Client inquiries within [2] business days |
| Confidentiality | Treat all Client information in accordance with Section 9 of this SOW |
| Staffing | Assign qualified personnel; notify Client of any key personnel changes with [10] business days notice |

### 4.2 Client Responsibilities

| Responsibility | Detail |
|----------------|--------|
| Stakeholder access | Provide access to relevant technical and operational staff for interviews and information gathering |
| Tool access | Grant read-only access to security tools, dashboards, and platforms necessary to perform advisory services |
| Timely responses | Respond to information requests and discovery questions within [5] business days |
| Action item ownership | Assign internal owners to all action items and track remediation progress |
| Meeting attendance | Ensure appropriate stakeholders attend scheduled advisory meetings and QBRs |
| Data accuracy | Provide accurate and up-to-date information about the environment, tools, and incidents |
| Change notification | Notify Service Provider of significant changes to the environment, tools, or business within [5] business days |
| Deliverable review | Review and provide feedback or acceptance on deliverables within [10] business days of receipt |
| Payment | Remit payment per the terms in Section 8 |

---

## 5. Engagement Timeline & Milestones

### 5.1 High-Level Phases

| Phase | Description | Target Start | Target Completion |
|-------|-------------|--------------|-------------------|
| Kickoff & Discovery | Kickoff meeting, pre-engagement questionnaire review, stakeholder interviews | [Start Date] | [+2 weeks] |
| Baseline Assessment | Tool/platform reviews, vulnerability and log coverage audit, baseline report | [+2 weeks] | [+4 weeks] |
| Ongoing Advisory | Monthly meetings, metrics reporting, action item tracking | [+1 month] | [Engagement End Date] |
| Quarterly Reviews | QBR #1, QBR #2, QBR #3, QBR #4 (annual) | [+3 months] | [Engagement End Date] |
| Renewal Planning | Value review, expansion discussion, renewal recommendation | [60 days before end] | [End Date] |

### 5.2 Milestone Schedule

| Milestone | Description | Expected Completion Date |
|-----------|-------------|--------------------------|
| M1 — Kickoff Meeting Completed | Initial meeting held; discovery questions distributed | [Date] |
| M2 — Access & Onboarding Complete | All tool and platform access granted and confirmed | [Date] |
| M3 — Baseline Report Delivered | Baseline Security Posture Report provided to Client | [Date] |
| M4 — Gap Remediation Roadmap Delivered | Prioritized roadmap with owners and timelines | [Date] |
| M5 — First Monthly Advisory Meeting | First recurring advisory meeting completed | [Date] |
| M6 — QBR #1 | First Quarterly Business Review completed | [Date] |
| M7 — QBR #2 | Second Quarterly Business Review completed | [Date] |
| M8 — QBR #3 | Third Quarterly Business Review completed | [Date] |
| M9 — QBR #4 / Annual Review | Final Quarterly Business Review; renewal discussion initiated | [Date] |
| M10 — Renewal Decision | Renewal or off-boarding plan confirmed | [60 days before end] |

---

## 6. Assumptions and Dependencies

The following assumptions underlie the scope and timeline of this engagement. If any assumption proves incorrect, scope or schedule adjustments may be required via a Change Order.

| # | Assumption / Dependency |
|---|-------------------------|
| 1 | Client will provide read-only access to all tools and platforms referenced in Section 3 within [10] business days of the Effective Date |
| 2 | Client has an existing vulnerability scanning tool in place. If not, tool selection and implementation are out of scope and may require a separate engagement |
| 3 | Client has an existing SIEM or log management platform. Advisory assumes the platform is operational; implementation support is out of scope |
| 4 | Client will designate a single primary point of contact (POC) responsible for coordinating access, information, and responses |
| 5 | Discovery questions submitted in advance of the kickoff meeting will be answered before the meeting to the extent practicable |
| 6 | Client will assign internal owners to all action items within [5] business days of each meeting |
| 7 | Monthly meeting scheduling will be confirmed at least [5] business days in advance |
| 8 | QBR scheduling will be confirmed at least [10] business days in advance |
| 9 | Service Provider is not responsible for delays caused by Client failure to fulfill responsibilities listed in Section 4.2 |
| 10 | Scope and pricing assume a stable environment. Major acquisitions, divestitures, or significant infrastructure changes may require scope revision |

---

## 7. Change Management Process

### 7.1 What Constitutes a Change

A change is any request that would:
- Add services, deliverables, or activities not described in this SOW
- Remove services or deliverables from scope
- Change agreed timelines or milestones by more than [10] business days
- Alter the assumptions or dependencies in Section 6 in a material way
- Require additional hours beyond the monthly allocation described in Section 8

### 7.2 Change Request Procedure

1. **Identification:** Either party may identify a potential change by submitting a written Change Request (CR) to the other party.
2. **Documentation:** The Service Provider will document the proposed change, including: description of the change, reason for the change, impact on scope, timeline, and cost, and any dependencies or risks.
3. **Review:** The Client has [5] business days to review and approve or reject the Change Request.
4. **Approval:** Changes are effective only upon written approval (email acceptable) by authorized representatives of both parties.
5. **Implementation:** Work on the changed scope begins after written approval. Service Provider will not begin out-of-scope work without an approved Change Order.

### 7.3 Emergency Changes

For urgent changes (e.g., active security incident support beyond scope), the Service Provider may begin work upon verbal approval from the Client's authorized representative, with written confirmation required within [2] business days.

---

## 8. Fees and Payment Terms

### 8.1 Fee Structure

| Item | Rate / Amount | Notes |
|------|---------------|-------|
| Monthly Retainer Fee | $[X,XXX] / month | Covers [X] advisory hours per month plus all standard deliverables |
| Quarterly Business Review (included) | Included in retainer | No additional charge |
| Overage Hours | $[XXX] / hour | Billed monthly in arrears; requires Client notification before incurring |
| Ad-Hoc Incident Response Support | $[XXX] / hour | Applies only to hours beyond the monthly retainer allocation |
| [Additional Line Item] | $[X,XXX] | [Description] |

### 8.2 Payment Terms

- Invoices will be issued on the [1st / 15th] of each month for the upcoming month's retainer (or prior month's actuals, as agreed).
- Payment is due within [Net 30] days of invoice date.
- Late payments are subject to a [1.5%] monthly interest charge on the outstanding balance.
- All fees are in [USD] and are exclusive of applicable taxes.

### 8.3 Expense Reimbursement

[Client / Service Provider] is responsible for travel and out-of-pocket expenses incurred in connection with this engagement. Expenses exceeding $[XXX] per occurrence require prior written Client approval. All expenses will be invoiced at cost with supporting receipts.

---

## 9. Confidentiality and Data Handling

### 9.1 Confidentiality

Both parties acknowledge that in the course of this engagement, each may receive or have access to confidential information belonging to the other party. Each party agrees to:

- Treat all confidential information as strictly confidential
- Use confidential information solely for the purposes of this engagement
- Not disclose confidential information to third parties without prior written consent, except as required by law
- Apply at least the same degree of care to protecting the other party's confidential information as it applies to its own confidential information, but in no event less than reasonable care

Confidential information includes, but is not limited to: security findings and reports, vulnerability data, network architecture, tool configurations, incident history, business strategy, and financial information.

### 9.2 Data Handling

- Service Provider will not store, copy, or retain Client data beyond what is strictly necessary to perform the services described in this SOW.
- All Client data will be handled in accordance with [applicable data protection regulation or Client data handling policy, e.g., GDPR, HIPAA, Client's Data Classification Policy].
- Upon engagement completion or termination, Service Provider will [destroy / return] all Client data within [30] days and provide written confirmation of destruction upon request.
- Service Provider will promptly notify Client of any suspected unauthorized access to or disclosure of Client data.

---

## 10. Acceptance Criteria

### 10.1 Deliverable Acceptance Process

1. Service Provider submits a completed deliverable to the Client's primary contact via [email / agreed delivery method].
2. Client has [10] business days to review the deliverable and either:
   - Provide written acceptance, or
   - Provide written feedback identifying specific deficiencies.
3. If deficiencies are identified, Service Provider will address them within [5] business days.
4. The revised deliverable is resubmitted and Client has [5] additional business days to provide final acceptance.
5. If no response is received within the review period, the deliverable is deemed accepted.

### 10.2 Acceptance Standards

| Deliverable | Acceptance Standard |
|-------------|---------------------|
| Baseline Security Posture Report | Covers all in-scope areas; findings are accurate and supported by evidence; gaps are risk-rated |
| Gap Remediation Roadmap | Gaps are prioritized by risk; each item has a recommended action, suggested owner, and target timeline |
| Monthly Advisory Meeting Notes | Distributed within 5 business days; accurately reflects discussion; includes all action items with owners and due dates |
| Vulnerability Metrics Report | Includes open count by severity, age distribution, SLA compliance %, and month-over-month trend |
| Quarterly Business Review Report | Covers all QBR sections; metrics are current; includes next-quarter objectives |
| Log Coverage Gap Report | Inventories all active log sources; identifies gaps with risk ratings and onboarding priority |

---

## Signatures

By signing below, the authorized representatives of both parties confirm their agreement to the terms of this Statement of Work.

---

**[Firm Name] — Service Provider**

Signature: ___________________________________

Printed Name: [Consultant Name]

Title: [Title]

Date: ___________________

---

**[Client Name] — Client**

Signature: ___________________________________

Printed Name: [Authorized Signatory Name]

Title: [Title]

Date: ___________________

---

*This Statement of Work is confidential. Unauthorized distribution is prohibited. SOW Number: [SOW-YYYY-NNN]*
