# Security Consulting Toolkit

A professional, end-to-end security consulting resource library for vulnerability management, SIEM services, client engagement, and risk reporting. Built around the **Customer Advisory Framework** — discovery first, value-focused conversations, measurable outcomes, and continuous engagement.

---

## Table of Contents

1. [How to Use This Toolkit](#how-to-use-this-toolkit)
2. [Customer Advisory Framework](#customer-advisory-framework)
3. [Repository Structure](#repository-structure)
   - [engagement-templates/](#engagement-templates)
   - [sla-standards/](#sla-standards)
   - [reports/](#reports)
   - [assessment-checklists/](#assessment-checklists)
   - [client-resources/](#client-resources)
   - [siem-services/](#siem-services)
4. [Frameworks and Platforms Covered](#frameworks-and-platforms-covered)
5. [Client Engagement Model](#client-engagement-model)
6. [Consultant Bio](#consultant-bio)

---

## How to Use This Toolkit

This toolkit is designed to support security consultants at every stage of the client lifecycle — from first contact through renewal. Every template, checklist, and guide is ready to be handed directly to a client or used as internal reference with minimal customization.

**For new engagements:**
Start with `assessment-checklists/discovery-questionnaire.md` and `assessment-checklists/scope-definition-worksheet.md` to baseline the client. Then use `engagement-templates/proposal-template.md` and `engagement-templates/statement-of-work-template.md` to formalize the engagement.

**For active engagements:**
Use `engagement-templates/client-meeting-agenda-template.md` for every advisory session. Deliver findings using the `reports/technical/` template and roll up to leadership with `reports/executive/`. Track remediation progress with `reports/remediation-roadmap/`.

**For renewals and expansion:**
Use `engagement-templates/renewal-conversation-template.md` to structure renewal conversations around value delivered, not just license extension. Use `engagement-templates/quarterly-business-review-template.md` for QBR delivery. Point expansion conversations to `client-resources/expansion-upsell-guide.md`.

**For SIEM deployments:**
Begin with `siem-services/siem-comparison/siem-platform-guide.md` to select the right platform. Follow the onboarding sequence in `siem-services/onboarding/`. Use `siem-services/log-sources/universal-log-source-checklist.md` to identify and configure log sources. Deploy baseline detection coverage using `siem-services/detection-rules/detection-use-case-library.md`.

---

## Customer Advisory Framework

All templates in this repository reflect the following consulting methodology:

### 1. Customer Discovery and Baselining
Every engagement begins with structured discovery covering: security goals and risk tolerance, compliance requirements, current tool inventory, vulnerability tracking processes, SLA adherence, asset criticality mapping, external attack surface visibility, log collection maturity, and incident response readiness. Discovery questions are embedded in proposals, kickoff checklists, and onboarding templates throughout this toolkit.

### 2. Renewal Conversation Strategy
Renewals are positioned as continued risk reduction — not license extensions. Each renewal conversation reviews value delivered, highlights measurable posture improvements, identifies remaining gaps, discusses upcoming initiatives, and confirms platform expectations for the next year. The renewal template structures these conversations to be forward-looking and outcome-focused.

### 3. Expansion and Upsell Paths
Growth conversations are grounded in the client's specific gap analysis, not generic product pitches. Expansion paths include: additional log sources, cloud workload visibility (AWS / Azure / GCP), application security testing, threat detection and response, reporting automation, remediation workflows, and ticketing integrations (ServiceNow, Jira). The expansion guide is written from the client's perspective to make value tangible.

### 4. Meeting Structure
Every advisory meeting follows a consistent structure: state the purpose of the meeting, review current security posture, ask targeted discovery questions, review progress against prior action items, identify gaps and introduce improvements, and confirm action items with owners and due dates before closing.

### 5. Customer Engagement Model
- **Month 1:** Baseline assessment — establish current state, critical gaps, and 90-day priorities
- **Ongoing:** Regular advisory meetings using the standard meeting agenda
- **Quarterly:** QBR delivery with measurable improvements, gap analysis, and expansion alignment
- **Annually:** Renewal conversation with full-year value summary and next-year planning

---

## Repository Structure

### `engagement-templates/`
Client-facing and internal templates for the full engagement lifecycle.

| File | Purpose |
|------|---------|
| `proposal-template.md` | Formal proposal covering scope, objectives, methodology, deliverables, timeline, and three-tier pricing. Includes pre-engagement discovery questions. |
| `statement-of-work-template.md` | Formal SOW with service definitions, deliverable specifications, and acceptance criteria. |
| `engagement-kickoff-checklist.md` | Structured kickoff meeting checklist following the framework meeting script. Ensures baseline is captured at day one. |
| `renewal-conversation-template.md` | Renewal meeting guide with value delivered summary, posture improvement highlights, gap identification, and next-year planning sections. |
| `quarterly-business-review-template.md` | QBR template with measurable security improvements, gap analysis, and expansion opportunity sections mapped to upsell paths. |
| `client-meeting-agenda-template.md` | Standard advisory meeting agenda following the framework meeting structure. |

---

### `sla-standards/`
Policy templates for vulnerability response, patch management, and emergency response.

| File | Purpose |
|------|---------|
| `vulnerability-remediation-sla-policy.md` | SLA policy with timelines: Critical (24–48 hrs), High (7 days), Medium (30 days), Low (90 days). Includes exception handling and escalation procedures. |
| `zero-day-response-playbook.md` | Step-by-step zero-day response from initial discovery through remediation verification and post-incident review. |
| `patch-management-policy.md` | Comprehensive patch management policy covering scope, roles, patch cycles, testing, rollback, and compliance reporting. |

---

### `reports/`

#### `reports/executive/`
| File | Purpose |
|------|---------|
| `executive-risk-report-template.md` | Executive risk report written for non-technical stakeholders. Risk ratings, business impact language, trend chart placeholders, and QBR cadence alignment. |

#### `reports/technical/`
| File | Purpose |
|------|---------|
| `technical-findings-report-template.md` | Detailed technical findings report with vulnerability details, CVSS scores, affected asset inventory, reproduction steps, and proof of concept sections. |

#### `reports/remediation-roadmap/`
| File | Purpose |
|------|---------|
| `prioritized-remediation-plan-template.md` | Prioritized remediation plan organized by CIS Control with effort estimates, risk reduction scores, and owner assignment. |

---

### `assessment-checklists/`
Structured checklists and worksheets for baseline assessments and ongoing program evaluation.

| File | Purpose |
|------|---------|
| `cis-controls-assessment-checklist.md` | Full CIS Controls v8 assessment covering all 18 controls with pass/fail/partial status fields and scoring. |
| `vulnerability-management-maturity-checklist.md` | VM program maturity assessment covering discovery, prioritization, remediation, verification, and reporting dimensions. |
| `client-onboarding-checklist.md` | Client onboarding checklist incorporating the baseline assessment approach — technical setup, stakeholder alignment, and documentation. |
| `scope-definition-worksheet.md` | Scope definition document including asset criticality classification and external asset visibility mapping. |
| `discovery-questionnaire.md` | Client intake document built directly from the Customer Discovery and Baselining framework. Formatted as a fillable questionnaire. |

---

### `client-resources/`
Plain-English resources written for non-technical client stakeholders.

| File | Purpose |
|------|---------|
| `vulnerability-management-guide.md` | Plain-English guide explaining what vulnerability management is, why it matters, and what to expect from the program. |
| `risk-rating-explanation.md` | Business-language explanation of Critical / High / Medium / Low risk ratings with real-world business impact context. |
| `client-faq.md` | Answers to the most common client questions about security programs, findings, timelines, and the consulting relationship. |
| `expansion-upsell-guide.md` | Client-facing guide explaining the business value of additional log sources, cloud visibility, application testing, and ITSM integrations. |

---

### `siem-services/`
End-to-end SIEM deployment and operations resources organized into four areas.

#### `siem-services/log-sources/`
| File | Purpose |
|------|---------|
| `universal-log-source-checklist.md` | Comprehensive log source reference covering every major category: Firewall, VPN, Active Directory, Endpoint, Email, AV/EDR, Cloud (AWS/Azure/GCP/M365), DNS, DHCP, Web Proxy, and NetFlow. Each source includes what it is, what logs it generates, what security events to look for, and SIEM onboarding guidance. |

#### `siem-services/siem-comparison/`
| File | Purpose |
|------|---------|
| `siem-platform-guide.md` | Platform comparison for Splunk, Microsoft Sentinel, IBM QRadar, Elastic SIEM, and Rapid7 IDR. Covers deployment models, pricing, best-fit client size, strengths, weaknesses, and CIS alignment. Includes client-facing positioning guidance and expansion conversation maps. |

#### `siem-services/onboarding/`
| File | Purpose |
|------|---------|
| `siem-onboarding-project-plan.md` | Phased SIEM onboarding project plan: Discovery → Log Source Identification → Connector Setup → Alert Rule Configuration → Tuning → Handoff. |
| `log-source-priority-matrix.md` | Ranked matrix of log sources by risk and detection value. Guides the order of onboarding to maximize early detection coverage. |
| `siem-health-check-checklist.md` | Operational health check covering log ingestion rates, parser accuracy, alert firing, retention policies, and backup/redundancy. |

#### `siem-services/detection-rules/`
| File | Purpose |
|------|---------|
| `detection-use-case-library.md` | Top 20 must-have detection rules for every client regardless of SIEM platform. Each rule includes: rule name, description, required log sources, plain-English detection logic, MITRE ATT&CK mapping, CIS Control alignment, severity, and recommended response actions. |

---

## Frameworks and Platforms Covered

**Compliance Frameworks**
- CIS Controls v8 (primary framework throughout all templates)
- MITRE ATT&CK v14 (detection rules and threat mapping)
- NIST Cybersecurity Framework (referenced in risk reporting)
- SOC 2, ISO 27001, HIPAA, PCI-DSS (referenced in proposal and SOW templates)

**SIEM Platforms**
- Splunk Enterprise / Splunk Cloud
- Microsoft Sentinel
- IBM QRadar
- Elastic SIEM (Elastic Security)
- Rapid7 InsightIDR

**Cloud Platforms**
- Amazon Web Services (AWS) — CloudTrail, GuardDuty, Security Hub
- Microsoft Azure — Sentinel, Defender for Cloud, Azure AD
- Google Cloud Platform (GCP) — Chronicle, Cloud Audit Logs
- Microsoft 365 — Defender, Purview, Unified Audit Log

**Ticketing and ITSM Integrations**
- ServiceNow
- Jira
- PagerDuty (referenced in onboarding and SLA templates)

**Identity Platforms**
- Microsoft Active Directory / Azure AD
- Okta
- Ping Identity

---

## Client Engagement Model

```
Month 1 — Baseline Assessment
├── Discovery questionnaire completion
├── Scope definition and asset inventory
├── CIS Controls gap assessment
├── Initial risk report delivery
└── 90-day remediation roadmap

Ongoing — Regular Advisory Meetings
├── Monthly check-in using meeting agenda template
├── Remediation progress tracking
├── New vulnerability triage and SLA tracking
└── Threat intelligence briefings

Quarterly — Business Reviews (QBR)
├── Measurable posture improvement metrics
├── Gap analysis update
├── Expansion opportunity review
└── Executive risk report delivery

Annual — Renewal Planning
├── Full-year value delivered summary
├── Year-over-year posture comparison
├── Next-year initiative planning
└── Renewal positioned as risk reduction continuation
```

---

## Consultant Bio

**Senior Security Advisor | Vulnerability Management | Application Security | Threat Detection**
*Northstar Cyber Advisory*

Cybersecurity advisor specializing in vulnerability management, application security, and threat detection. Experienced in helping organizations strengthen their security posture through effective vulnerability remediation strategies, improved log visibility, and security platform optimization using solutions such as Rapid7 InsightVM and InsightIDR. Focused on aligning security operations with business risk reduction while improving detection capabilities and security program maturity.

**Contact:** [your email]
**LinkedIn:** [linkedin.com/in/yourprofile]
**Certifications:** Microsoft SC-200 | Security+ | CEH (in progress) | CISSP (in progress)

---

*Security Consulting Toolkit v1.0*
*Built on the Customer Advisory Framework | CIS Controls v8 | MITRE ATT&CK v14*
