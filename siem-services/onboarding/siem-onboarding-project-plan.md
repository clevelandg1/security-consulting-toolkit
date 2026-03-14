# SIEM Onboarding Project Plan
**Client:** [Client Name]
**Platform:** [SIEM Platform]
**Version:** 1.0
**Project Start Date:** [Start Date]
**Target Go-Live Date:** [Go-Live Date]
**Prepared By:** [Consultant Name]
**Last Updated:** [Date]

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Phase Overview](#2-phase-overview)
3. [Roles and Responsibilities](#3-roles-and-responsibilities)
4. [Phase 1: Discovery and Requirements](#4-phase-1-discovery--requirements-weeks-12)
5. [Phase 2: Log Source Identification and Prioritization](#5-phase-2-log-source-identification--prioritization-weeks-23)
6. [Phase 3: SIEM Infrastructure Setup](#6-phase-3-siem-infrastructure-setup-weeks-35)
7. [Phase 4: Log Source Connector Setup](#7-phase-4-log-source-connector-setup-weeks-48)
8. [Phase 5: Alert Rule Configuration](#8-phase-5-alert-rule-configuration-weeks-69)
9. [Phase 6: Tuning and Optimization](#9-phase-6-tuning--optimization-weeks-812)
10. [Phase 7: Handoff and Knowledge Transfer](#10-phase-7-handoff--knowledge-transfer-week-12)
11. [Project Risks and Mitigation](#11-project-risks-and-mitigation)
12. [Project Sign-Off](#12-project-sign-off)

---

## 1. Project Overview

### 1.1 Purpose

This project plan defines the activities, timelines, responsibilities, and success criteria for the SIEM onboarding engagement for [Client Name]. The objective is to deploy [SIEM Platform] in a fully operational state, onboard all priority log sources, configure baseline detection rules, and complete knowledge transfer to the [Client Name] security team.

### 1.2 Success Criteria

The engagement will be considered successful when all of the following criteria are met:

- [ ] SIEM platform is operational and accessible to all authorized users
- [ ] All Tier 1 log sources are connected, parsing correctly, and generating alerts
- [ ] All Tier 2 log sources are connected and validated
- [ ] Baseline detection ruleset is active and tuned to an acceptable false positive rate
- [ ] Client security team has completed platform training and can operate the SIEM independently
- [ ] Operational runbook is complete and approved by client
- [ ] Go-live sign-off checklist is signed by client stakeholders
- [ ] Compliance reporting requirements have been validated (if applicable)

### 1.3 Project Stakeholders

| Name | Organization | Role | Responsibility |
|---|---|---|---|
| [Client Primary Contact] | [Client Name] | Project Sponsor | Final approval authority, executive escalation |
| [Client Security Lead] | [Client Name] | Security Operations Lead | Day-to-day security decisions, alert review, go-live approval |
| [Client IT Lead] | [Client Name] | IT Infrastructure Lead | Log source configuration, network connectivity, firewall rules |
| [Client Compliance Contact] | [Client Name] | Compliance / GRC | Compliance requirements input, evidence validation |
| [Consultant Project Manager] | [Consulting Firm] | Engagement Manager | Overall project coordination, milestone tracking |
| [Lead SIEM Engineer] | [Consulting Firm] | Lead Engineer | Platform deployment, connector configuration, rule setup |
| [Support Engineer] | [Consulting Firm] | SIEM Engineer | Log source connectors, parsing, testing support |

---

## 2. Phase Overview

| Phase | Name | Duration | Key Outputs |
|---|---|---|---|
| **1** | Discovery and Requirements | Weeks 1–2 | Requirements document, use case list, environment architecture diagram |
| **2** | Log Source Identification and Prioritization | Weeks 2–3 | Prioritized log source list, volume estimate, connector plan |
| **3** | SIEM Infrastructure Setup | Weeks 3–5 | Operational SIEM environment, access matrix, storage/retention config |
| **4** | Log Source Connector Setup | Weeks 4–8 | All priority log sources connected and validated |
| **5** | Alert Rule Configuration | Weeks 6–9 | Active alert ruleset, notification routing document |
| **6** | Tuning and Optimization | Weeks 8–12 | Tuned ruleset, tuning documentation, suppression list |
| **7** | Handoff and Knowledge Transfer | Week 12 | Trained client team, operational runbook, signed go-live checklist |

> **Note:** Phases 4 and 5 overlap with Phases 3 and 6 intentionally to allow parallel progress. The project Gantt schedule in [Project Schedule Document] shows the detailed timeline.

---

## 3. Roles and Responsibilities

### 3.1 RACI Matrix

**R** = Responsible | **A** = Accountable | **C** = Consulted | **I** = Informed

| Activity | Client Sponsor | Client Security Lead | Client IT Lead | Client Compliance | Consulting PM | Lead SIEM Engineer | Support Engineer |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Stakeholder interviews | A | R | C | C | R | I | I |
| Requirements documentation | I | A | C | C | C | R | I |
| Environment architecture review | I | C | R | I | C | R | C |
| Log source inventory | I | A | R | I | C | R | C |
| Use case requirements gathering | C | R | I | R | C | A | I |
| Platform provisioning | I | I | C | I | A | R | C |
| Network / firewall configuration | I | I | R | I | I | C | I |
| Log source connector setup | I | C | R | I | A | R | R |
| Parser testing and validation | I | R | C | I | I | A | R |
| Detection rule configuration | I | A | I | C | I | R | C |
| Alert routing configuration | I | R | I | I | I | A | C |
| Tuning and false positive review | I | R | I | I | C | A | R |
| Compliance report validation | I | C | I | A | I | R | I |
| Training delivery | I | A | C | I | C | R | C |
| Runbook creation | I | A | I | I | C | R | C |
| Go-live sign-off | A | R | R | C | R | I | I |

---

## 4. Phase 1: Discovery and Requirements (Weeks 1–2)

### 4.1 Objectives

Establish a complete understanding of the client's environment, compliance requirements, existing security tooling, and SIEM use case priorities to inform all subsequent phases.

### 4.2 Activities and Checklists

#### Stakeholder Interviews

- [ ] Schedule and conduct kickoff meeting with all identified stakeholders
- [ ] Interview security operations lead: current incident response process, alert fatigue pain points, previous SIEM experience
- [ ] Interview IT infrastructure lead: network topology, log source landscape, existing syslog infrastructure
- [ ] Interview compliance/GRC stakeholder: applicable frameworks, audit evidence requirements, reporting expectations
- [ ] Interview executive sponsor: business objectives, success metrics, organizational priorities
- [ ] Document all interview notes and distribute for stakeholder review

#### Environment Documentation Review

- [ ] Collect and review existing network topology diagrams
- [ ] Collect and review existing security architecture documents
- [ ] Review current asset inventory (or conduct inventory if not available)
- [ ] Review existing security tool stack (AV/EDR, firewall, email gateway, IDS/IPS, etc.)
- [ ] Review current logging configuration on priority systems (what is already logging, where does it go?)
- [ ] Identify any existing SIEM or log aggregation infrastructure (predecessor systems)
- [ ] Document cloud environment scope (AWS accounts, Azure subscriptions, GCP projects)

#### Compliance Requirements Identification

- [ ] Identify all applicable compliance frameworks (PCI DSS, HIPAA, SOC 2, CMMC, NIST, ISO 27001, etc.)
- [ ] Document audit evidence requirements that SIEM will need to support
- [ ] Identify log retention requirements per framework (e.g., PCI requires 12 months with 3 months immediately available)
- [ ] Identify required compliance reports and dashboards
- [ ] Confirm audit timeline — are there upcoming audits the SIEM deployment must support?

#### Existing Log Source Inventory

- [ ] Document all systems currently generating security-relevant logs
- [ ] Identify log format for each source (syslog, JSON, CEF, LEEF, Windows Event Log, etc.)
- [ ] Estimate daily log volume per source (GB/day or EPS)
- [ ] Identify current log destination for each source (local only, syslog server, existing SIEM, SIEM bypassed)
- [ ] Identify log source owner (team or individual responsible for each system)
- [ ] Flag any log sources requiring elevated change control or vendor coordination

#### Use Case Requirements Gathering

- [ ] Review the detection use case library with the security lead
- [ ] Prioritize top 20 use cases based on client threat profile and environment
- [ ] Identify any client-specific use cases not covered by the standard library
- [ ] Map use cases to required log sources (confirm all required sources are in scope)
- [ ] Identify any executive or compliance reporting use cases
- [ ] Document and obtain sign-off on final prioritized use case list

### 4.3 Phase 1 Outputs

| Output | Description | Owner | Due Date |
|---|---|---|---|
| Requirements Document | Full documentation of environment, compliance requirements, and technical requirements | Lead SIEM Engineer | End of Week 2 |
| Environment Architecture Diagram | Annotated network/security architecture showing log sources and data flows | Lead SIEM Engineer | End of Week 2 |
| Prioritized Use Case List | Top 20+ use cases signed off by client security lead | Consulting PM | End of Week 2 |
| Phase 1 Sign-Off | Client stakeholder acknowledgment that requirements are complete and accurate | Client Security Lead | End of Week 2 |

---

## 5. Phase 2: Log Source Identification and Prioritization (Weeks 2–3)

### 5.1 Objectives

Produce a definitive, prioritized log source list with volume estimates and connector methods to guide Phases 3 and 4.

### 5.2 Activities and Checklists

#### Full Log Source Inventory

- [ ] Compile complete list of all log sources from Phase 1 interviews and documentation
- [ ] Validate list with client IT lead — confirm all major systems are captured
- [ ] Identify any log sources not yet in the inventory through network scanning or asset management tools
- [ ] Classify each source by type (authentication, network, endpoint, cloud, application, database, etc.)

#### Prioritization Using Detection Value Matrix

- [ ] Apply the Log Source Priority Matrix to rank all identified sources (see log-source-priority-matrix.md)
- [ ] Assign each source to a priority tier (Tier 1–4)
- [ ] Review prioritization with client security lead and adjust based on client-specific risk profile
- [ ] Confirm final prioritized list with client stakeholders

#### Connector Availability Check

- [ ] For each Tier 1 and Tier 2 source, identify the available connector method:
  - [ ] Native platform connector (out-of-the-box)
  - [ ] Syslog (UDP/TCP/TLS)
  - [ ] API pull (REST API, vendor API)
  - [ ] Agent-based (Universal Forwarder, Elastic Agent, InsightIDR Collector, etc.)
  - [ ] Cloud storage ingestion (S3 bucket, Azure Blob, GCP Storage)
  - [ ] Custom/scripted connector (note as high complexity)
- [ ] Identify any sources with no available connector — flag for custom development or descoping
- [ ] Confirm connector compatibility with target SIEM platform version

#### Data Volume Estimation

- [ ] Estimate daily log volume (GB/day or EPS) for each Tier 1 and Tier 2 source
- [ ] Validate estimates against client log infrastructure where possible (existing syslog server stats, cloud storage metrics)
- [ ] Total all volume estimates to produce overall ingestion estimate
- [ ] For GB/day-priced platforms: calculate estimated monthly cost impact
- [ ] Identify any sources with unexpectedly high volume that require data filtering or sampling decisions

### 5.3 Log Source Inventory Worksheet

| Source | Type | Volume Estimate | Priority Tier | Connector Method | Owner | Notes |
|---|---|---|---|---|---|---|
| [Log Source 1] | [Authentication / Network / Endpoint / Cloud / Application / Database / Other] | [GB/day or EPS] | [Tier 1–4] | [Syslog / API / Agent / S3 / Native Connector] | [Team or Individual] | [Notes] |
| [Log Source 2] | | | | | | |
| [Log Source 3] | | | | | | |
| [Log Source 4] | | | | | | |
| [Log Source 5] | | | | | | |
| [Log Source 6] | | | | | | |
| [Log Source 7] | | | | | | |
| [Log Source 8] | | | | | | |
| [Log Source 9] | | | | | | |
| [Log Source 10] | | | | | | |
| **TOTAL** | | **[X GB/day]** | | | | |

### 5.4 Phase 2 Outputs

| Output | Description | Owner | Due Date |
|---|---|---|---|
| Prioritized Log Source List | Ranked list of all log sources with tier assignments and detection value rationale | Lead SIEM Engineer | End of Week 3 |
| Volume Estimate | Total estimated ingestion volume with per-source breakdown | Lead SIEM Engineer | End of Week 3 |
| Connector Plan | Connector method, complexity, and owner for each Tier 1 and Tier 2 source | Lead SIEM Engineer | End of Week 3 |
| Phase 2 Sign-Off | Client sign-off on prioritized list and connector approach | Client Security Lead | End of Week 3 |

---

## 6. Phase 3: SIEM Infrastructure Setup (Weeks 3–5)

### 6.1 Objectives

Provision a fully operational SIEM environment with appropriate storage, retention, access controls, and backup configuration ready to receive log sources.

### 6.2 Cloud-Native SIEM Setup (Splunk Cloud / Microsoft Sentinel / Rapid7 InsightIDR)

#### Platform Provisioning

- [ ] Create and configure cloud SIEM tenant / workspace
- [ ] Configure tenant settings: organization name, time zone, data region
- [ ] Validate platform access from client networks (no firewall blocking)
- [ ] Confirm platform version and feature availability for licensed tier
- [ ] Enable required platform modules (e.g., Splunk ES premium app, Sentinel analytics rules, InsightIDR UEBA)

#### Network Connectivity

- [ ] Identify all log source network segments that need to reach the SIEM collector
- [ ] Configure cloud collector endpoints (Splunk Cloud HEC, Sentinel DCE endpoint, InsightIDR Collector)
- [ ] Submit firewall change requests for required outbound connectivity from log sources
- [ ] Test connectivity from each network segment to the SIEM collector (confirm no drop)
- [ ] Configure TLS certificate for collector endpoints (validate cert chain)
- [ ] Document all firewall rules opened for this project

#### Storage and Retention Configuration

- [ ] Define retention periods by log source type based on compliance requirements:
  - Critical security logs (authentication, firewall): [X months/years]
  - Network logs: [X months/years]
  - Application logs: [X months/years]
  - Endpoint logs: [X months/years]
- [ ] Configure hot/warm/cold storage tiers if applicable (Splunk: tiered storage; Sentinel: analytics vs. basic vs. archive)
- [ ] Validate storage capacity for estimated volume over retention period
- [ ] Set up storage cost alerts / quota alerts if applicable

#### User Access Provisioning

- [ ] Define SIEM role taxonomy: Admin, Power User, Analyst, Read-Only
- [ ] Create or import all user accounts (SSO/SAML integration preferred)
- [ ] Assign roles per the access matrix document
- [ ] Enable MFA for all accounts
- [ ] Configure service accounts for integrations (alert routing, SOAR, ticketing)
- [ ] Document all user accounts and permissions in access matrix

#### Backup Configuration

- [ ] Configure platform backup or export to cold storage (where platform supports)
- [ ] Document backup schedule and retention
- [ ] Test backup restoration procedure
- [ ] For self-managed deployments: configure snapshots of SIEM server infrastructure

### 6.3 On-Premises SIEM Setup (IBM QRadar / Elastic Self-Managed)

#### Infrastructure Provisioning

- [ ] Confirm server/VM hardware meets SIEM vendor minimum specifications
- [ ] Provision servers (physical or virtual) per platform sizing guide
- [ ] Install base operating system and apply security baseline (CIS benchmark)
- [ ] Allocate and mount storage volumes per SIEM data storage requirements
- [ ] Configure network interfaces and routing
- [ ] Apply server hardening: disable unnecessary services, configure firewall, patch OS

#### SIEM Software Installation and Configuration

- [ ] Install SIEM platform software per vendor installation guide
- [ ] Apply license key
- [ ] Configure platform initialization settings (admin password, time zone, NTP)
- [ ] Configure high availability (if applicable) — primary and secondary nodes
- [ ] Validate platform health via platform health dashboard / CLI checks
- [ ] Apply latest platform patches and updates
- [ ] Configure log storage volumes and retention indices

#### Network Connectivity

- [ ] Configure syslog listener (UDP 514, TCP 514, TCP 6514 for TLS — per source requirements)
- [ ] Submit firewall change requests for log source → SIEM connectivity
- [ ] Configure TLS certificates for encrypted log forwarding sources
- [ ] Test connectivity from each source network segment

### 6.4 Phase 3 Outputs

| Output | Description | Owner | Due Date |
|---|---|---|---|
| Operational SIEM Environment | Fully deployed and accessible SIEM platform | Lead SIEM Engineer | End of Week 5 |
| Access Matrix Document | All user accounts, roles, and permissions documented | Lead SIEM Engineer | End of Week 5 |
| Storage/Retention Config Document | Retention periods, storage tiers, capacity plan | Lead SIEM Engineer | End of Week 5 |
| Network Connectivity Validation | Confirmation that all required network paths are open | Support Engineer | End of Week 5 |
| Phase 3 Sign-Off | Client IT lead sign-off on infrastructure configuration | Client IT Lead | End of Week 5 |

---

## 7. Phase 4: Log Source Connector Setup (Weeks 4–8)

### 7.1 Objectives

Connect all Tier 1 and Tier 2 log sources to the SIEM, validate parsing accuracy, and confirm data normalization for all connected sources.

### 7.2 Activities and Checklists

#### Connector Configuration

- [ ] Configure connectors for all Tier 1 sources first (parallel to Phase 3 infrastructure completion)
- [ ] For each source: configure log forwarding from source system (syslog config, API credentials, agent install, S3 bucket policy)
- [ ] Validate log flow: confirm events arriving in SIEM from each source
- [ ] Document any source-side configuration changes required (with change request reference)

#### Common Connector Methods

**Syslog (UDP/TCP/TLS):**
- [ ] Configure rsyslog / syslog-ng on source system to forward to SIEM collector
- [ ] Confirm UDP/TCP port connectivity
- [ ] For TLS: validate certificate, confirm successful TLS handshake, test encrypted forwarding
- [ ] Confirm expected message format (RFC 3164 or RFC 5424)

**API Pull:**
- [ ] Create API credentials / OAuth token on source platform (read-only minimum)
- [ ] Configure API polling interval in SIEM connector
- [ ] Validate API authentication successful
- [ ] Confirm data returned and volume aligns with estimate

**Agent-Based:**
- [ ] Deploy SIEM agent/collector on target systems (Universal Forwarder, Elastic Agent, InsightIDR Insight Agent)
- [ ] Configure agent to collect required log paths (Windows Event Log channels, Linux syslog paths, application log files)
- [ ] Validate agent health and connectivity in SIEM management console
- [ ] Confirm events arriving in SIEM from agent-managed sources

**Cloud Storage Ingestion (S3 / Azure Blob / GCP):**
- [ ] Configure cloud storage bucket/container for log export (CloudTrail → S3, Diagnostic Settings → Blob)
- [ ] Configure SIEM polling or event-driven trigger (SQS notification, Event Grid, Pub/Sub)
- [ ] Validate SIEM credentials/role has read access to storage
- [ ] Confirm logs flowing from cloud storage to SIEM

#### Parser Testing and Validation

- [ ] For each connected source: review 20+ sample events in SIEM to confirm correct parsing
- [ ] Validate that all required fields are extracted: source IP, destination IP, user, timestamp, event type, action/result
- [ ] Confirm timestamp is parsed correctly and converted to UTC (or normalized per platform)
- [ ] Identify any parser failures or unparsed event types — escalate to vendor or create custom parser
- [ ] Document parser name and version used for each source

#### Data Normalization Validation

- [ ] Confirm events are mapped to the SIEM's common information model (CIM) or ECS schema
- [ ] Run baseline queries against each source to confirm event counts and field quality
- [ ] Validate that identity fields (usernames) are normalized across sources (critical for UEBA)
- [ ] Confirm asset enrichment is functioning (IP → hostname → asset owner mapping)

### 7.3 Connector Status Tracking Table

| Log Source | Connector Type | Config Status | Parsing Status | Volume (GB/day) | Sign-Off |
|---|---|---|---|---|---|
| [Source 1] | [Syslog / API / Agent / S3 / Native] | [ ] Not Started / [ ] In Progress / [ ] Complete | [ ] Not Started / [ ] Testing / [ ] Validated / [ ] Issue | [X.XX] | [ ] |
| [Source 2] | | [ ] Not Started / [ ] In Progress / [ ] Complete | [ ] Not Started / [ ] Testing / [ ] Validated / [ ] Issue | | [ ] |
| [Source 3] | | [ ] Not Started / [ ] In Progress / [ ] Complete | [ ] Not Started / [ ] Testing / [ ] Validated / [ ] Issue | | [ ] |
| [Source 4] | | [ ] Not Started / [ ] In Progress / [ ] Complete | [ ] Not Started / [ ] Testing / [ ] Validated / [ ] Issue | | [ ] |
| [Source 5] | | [ ] Not Started / [ ] In Progress / [ ] Complete | [ ] Not Started / [ ] Testing / [ ] Validated / [ ] Issue | | [ ] |
| [Source 6] | | [ ] Not Started / [ ] In Progress / [ ] Complete | [ ] Not Started / [ ] Testing / [ ] Validated / [ ] Issue | | [ ] |
| [Source 7] | | [ ] Not Started / [ ] In Progress / [ ] Complete | [ ] Not Started / [ ] Testing / [ ] Validated / [ ] Issue | | [ ] |
| [Source 8] | | [ ] Not Started / [ ] In Progress / [ ] Complete | [ ] Not Started / [ ] Testing / [ ] Validated / [ ] Issue | | [ ] |
| [Source 9] | | [ ] Not Started / [ ] In Progress / [ ] Complete | [ ] Not Started / [ ] Testing / [ ] Validated / [ ] Issue | | [ ] |
| [Source 10] | | [ ] Not Started / [ ] In Progress / [ ] Complete | [ ] Not Started / [ ] Testing / [ ] Validated / [ ] Issue | | [ ] |

### 7.4 Phase 4 Outputs

| Output | Description | Owner | Due Date |
|---|---|---|---|
| All Tier 1 Sources Connected | All Tier 1 log sources forwarding events and parsing correctly | Lead SIEM Engineer | End of Week 6 |
| All Tier 2 Sources Connected | All Tier 2 log sources forwarding events and parsing correctly | Support Engineer | End of Week 8 |
| Connector Status Tracking Table | Completed status table with sign-off for all sources | Lead SIEM Engineer | End of Week 8 |
| Phase 4 Sign-Off | Client sign-off on all connected and validated log sources | Client Security Lead | End of Week 8 |

---

## 8. Phase 5: Alert Rule Configuration (Weeks 6–9)

### 8.1 Objectives

Configure a baseline detection ruleset aligned to the use case list, mapped to connected log sources, with appropriate severity thresholds and alert routing.

### 8.2 Activities and Checklists

#### Import and Configure Baseline Detection Rules

- [ ] Import platform-native detection content (Splunk ES content pack, Sentinel Analytics rules, InsightIDR built-in rules)
- [ ] Import any third-party detection content applicable to the environment (Sigma rules converted, SOC Prime content, etc.)
- [ ] Configure all use cases from the approved use case list (Phase 1 output)
- [ ] For each rule: confirm required log sources are connected and data is flowing

#### Top 20 Detection Rules to Implement

The following baseline ruleset should be implemented and validated for all client engagements. Adjust based on available log sources and client use case priorities.

| # | Detection Use Case | Required Log Sources | Severity | Priority |
|---|---|---|---|---|
| 1 | Brute force login — multiple failed authentications | AD, VPN, email, cloud IAM | High | Must Have |
| 2 | Successful login after multiple failures (spray success) | AD, cloud IAM | Critical | Must Have |
| 3 | Impossible travel — login from geographically distant locations | AD, VPN, cloud IAM | High | Must Have |
| 4 | Privileged account usage outside business hours | AD, cloud IAM | Medium | Must Have |
| 5 | New admin account created | AD, cloud IAM | High | Must Have |
| 6 | Mass file deletion or encryption (ransomware indicator) | Endpoint/EDR, file share logs | Critical | Must Have |
| 7 | Known malware hash execution | Endpoint/EDR, AV | Critical | Must Have |
| 8 | Outbound connection to known malicious IP | Firewall, proxy, DNS | High | Must Have |
| 9 | DNS query to newly registered or DGA domain | DNS logs | Medium | Must Have |
| 10 | Large outbound data transfer (exfiltration indicator) | Firewall, proxy, DLP | High | Must Have |
| 11 | Lateral movement — pass-the-hash / pass-the-ticket indicators | AD, endpoint | Critical | Must Have |
| 12 | Service account interactive login (anomalous behavior) | AD | High | Must Have |
| 13 | Cloud storage bucket made public | Cloud IAM, cloud storage logs | Critical | Must Have |
| 14 | Privileged cloud role assigned | Cloud IAM | High | Must Have |
| 15 | Firewall policy change | Firewall logs | Medium | Must Have |
| 16 | Security tool disabled or uninstalled | Endpoint/EDR | High | Must Have |
| 17 | RDP enabled on non-standard system | Endpoint, Windows event log | Medium | Should Have |
| 18 | PowerShell encoded command execution | Endpoint/EDR, Windows event log | High | Should Have |
| 19 | Email with malicious attachment delivered | Email gateway | High | Should Have |
| 20 | Vulnerability scan from internal source | Network, IDS | Medium | Should Have |

#### Map Rules to Log Sources

- [ ] For each configured rule: confirm all required log sources are connected and generating events
- [ ] Flag any rules that cannot be activated due to missing log sources (document gap)
- [ ] Verify rule logic against sample events from each required source

#### Severity Threshold Configuration

- [ ] Define severity levels for this client: Critical, High, Medium, Low, Informational
- [ ] Confirm escalation thresholds (which severity levels auto-page on-call, which go to email queue)
- [ ] Set alert suppression windows for maintenance periods
- [ ] Configure alert deduplication to prevent alert flooding from repeated events

#### Notification Routing Configuration

- [ ] Configure email notification for [Client Security Lead email] for all High and Critical alerts
- [ ] Configure ticketing integration (ServiceNow / Jira) if in scope — auto-create ticket on High/Critical
- [ ] Configure SOAR playbook triggers if in scope
- [ ] Configure on-call escalation path for Critical alerts (PagerDuty / OpsGenie / direct SMS)
- [ ] Test all notification channels with a test alert — confirm receipt at destination
- [ ] Document complete notification routing matrix

### 8.3 Phase 5 Outputs

| Output | Description | Owner | Due Date |
|---|---|---|---|
| Active Alert Ruleset | All use case rules deployed, mapped to log sources, and generating test alerts | Lead SIEM Engineer | End of Week 9 |
| Notification Routing Document | Documented routing matrix for all alert severity levels | Lead SIEM Engineer | End of Week 9 |
| Rule Gap Log | Any rules not activated due to missing log sources, with remediation plan | Lead SIEM Engineer | End of Week 9 |
| Phase 5 Sign-Off | Client security lead confirms alert rules are operational | Client Security Lead | End of Week 9 |

---

## 9. Phase 6: Tuning and Optimization (Weeks 8–12)

### 9.1 Objectives

Reduce false positive rate to an acceptable level, establish behavioral baselines for UEBA (if applicable), configure asset enrichment, and refine allowlists/suppression lists to enable efficient SOC operations.

### 9.2 Activities and Checklists

#### False Positive Identification and Suppression

- [ ] Run all configured rules for a minimum of one week (overlap with Phase 5)
- [ ] Review all alerts fired during the tuning period — classify as True Positive, False Positive, or Benign True Positive
- [ ] Identify top false positive rules (by volume of false positives)
- [ ] For each high-FP rule: determine root cause (threshold too sensitive, log source noise, missing exclusion)
- [ ] Apply appropriate suppression: source IP exclusion, time-of-day exclusion, known-good process exclusion, threshold adjustment
- [ ] Document every tuning action taken (rule, change applied, rationale)

#### Threshold Adjustment

- [ ] Review brute force rules: calibrate failed login count thresholds to client's baseline (avoid suppressing real attacks, avoid FP flood)
- [ ] Review data exfiltration rules: calibrate volume thresholds based on client's normal large-transfer patterns (backup jobs, CDN uploads)
- [ ] Review privilege escalation rules: whitelist known legitimate admin activities
- [ ] Review off-hours rules: confirm "business hours" definition matches client's actual schedule (include time zones, shift workers)

#### Asset Enrichment

- [ ] Import asset inventory into SIEM (from client CMDB, CrowdStrike, Rapid7 InsightVM, or manual import)
- [ ] Map IP addresses to hostnames, system owners, criticality ratings, and business function
- [ ] Configure dynamic asset lookup if supported by platform
- [ ] Validate that high-criticality assets are tagged for elevated alert priority

#### User and Entity Baseline Establishment

- [ ] If UEBA is enabled: confirm baselining period is active (typically 2–4 weeks of observation)
- [ ] Review initial UEBA risk scores — suppress known false positives (executives who travel frequently, admins with legitimate cross-system access)
- [ ] Establish peer group assignments for UEBA (executives, IT admins, standard users)
- [ ] Document UEBA configuration and peer group logic

#### Allowlist and Suppression List Refinement

- [ ] Create allowlist for known vulnerability scanners (internal scan IPs should not trigger brute force rules)
- [ ] Allowlist backup agent activity (large data transfers from backup servers)
- [ ] Allowlist privileged service accounts with known off-hours activity
- [ ] Allowlist IT admin systems for lateral movement detection (known admin jump hosts)
- [ ] Document all allowlist entries with rationale and review date

### 9.3 Tuning Tracker Table

| Rule | Initial False Positive Rate | Tuning Applied | Post-Tuning FP Rate | Status |
|---|---|---|---|---|
| [Rule 1] | [X FPs/day] | [Description of tuning change] | [Y FPs/day] | [ ] Acceptable / [ ] Needs Further Tuning |
| [Rule 2] | | | | |
| [Rule 3] | | | | |
| [Rule 4] | | | | |
| [Rule 5] | | | | |
| [Rule 6] | | | | |
| [Rule 7] | | | | |
| [Rule 8] | | | | |
| [Rule 9] | | | | |
| [Rule 10] | | | | |

**Target False Positive Rate:** Fewer than [X] FPs per analyst per 8-hour shift. (Recommended target: <10 FPs per analyst per day across the entire ruleset.)

### 9.4 Phase 6 Outputs

| Output | Description | Owner | Due Date |
|---|---|---|---|
| Tuned Ruleset | All rules operating at acceptable FP rate | Lead SIEM Engineer | End of Week 12 |
| Tuning Documentation | Complete record of all tuning actions, rationale, and resulting FP rates | Lead SIEM Engineer | End of Week 12 |
| Suppression and Allowlist Register | All suppressions and allowlists documented with rationale and review dates | Lead SIEM Engineer | End of Week 12 |
| Phase 6 Sign-Off | Client confirms FP rate is acceptable and operational baseline is established | Client Security Lead | End of Week 12 |

---

## 10. Phase 7: Handoff and Knowledge Transfer (Week 12)

### 10.1 Objectives

Ensure the client security team can operate the SIEM independently after the engagement concludes, with appropriate documentation and a defined ongoing support model.

### 10.2 Training Topics

Training should be delivered in [live sessions / recorded video / written guide — select per client preference]. Minimum training content:

| Training Topic | Audience | Duration | Format |
|---|---|---|---|
| Platform overview and navigation | All SIEM users | 60 minutes | Live walkthrough |
| Alert investigation workflow | Analysts | 90 minutes | Guided hands-on |
| Escalation and incident response procedure | Analysts, Security Lead | 45 minutes | Discussion + documentation review |
| Log source management (adding sources, health monitoring) | Security Lead, IT Lead | 60 minutes | Live walkthrough |
| Detection rule management (enable/disable/modify rules) | Security Lead | 60 minutes | Hands-on lab |
| Report generation and compliance dashboards | Security Lead, Compliance | 45 minutes | Live walkthrough |
| Tuning workflow (how to suppress FPs, update allowlists) | Security Lead | 60 minutes | Hands-on lab |
| Platform administration (user management, backup, updates) | IT Lead | 45 minutes | Live walkthrough |

### 10.3 Documentation Delivered to Client

- [ ] **Operational Runbook** — step-by-step procedures for all common SIEM tasks
- [ ] **Alert Investigation Runbook** — per-alert-type investigation guidance and escalation criteria
- [ ] **Log Source Inventory** — complete list of all connected sources with connector method and owner
- [ ] **Detection Rule Reference** — list of all active rules with description, severity, and required response
- [ ] **Suppression and Allowlist Register** — all suppression entries with rationale
- [ ] **User Access Matrix** — all accounts, roles, and permissions
- [ ] **Retention and Storage Configuration** — policy document with compliance mapping
- [ ] **Notification Routing Matrix** — all alert routing paths and escalation contacts
- [ ] **Tuning Documentation** — history of tuning decisions for future reference
- [ ] **Platform Administration Guide** — maintenance tasks, patching process, backup procedures
- [ ] **Vendor Support Contact Sheet** — platform vendor support contacts, SLAs, case submission process

### 10.4 Runbook Creation

The following runbooks must be created and reviewed with the client team before go-live:

- [ ] **Daily SIEM Health Check Runbook** — morning routine to verify all sources are healthy
- [ ] **Alert Triage Runbook** — how to assess, classify, and escalate each alert type
- [ ] **Log Source Onboarding Runbook** — step-by-step for adding a new source after go-live
- [ ] **User Provisioning/Deprovisioning Runbook** — adding and removing SIEM user accounts
- [ ] **Incident Response Escalation Runbook** — criteria for escalating from SIEM alert to full IR engagement
- [ ] **Platform Maintenance Runbook** — patching, backup verification, quarterly health review tasks

### 10.5 Go-Live Criteria Checklist

The following criteria must be met and verified before go-live sign-off is accepted:

#### Platform and Infrastructure
- [ ] SIEM platform fully operational and accessible to all authorized users
- [ ] All user accounts provisioned with correct roles and MFA enabled
- [ ] Storage and retention policies configured per compliance requirements
- [ ] Backup configuration verified and tested
- [ ] Network connectivity confirmed for all log sources

#### Log Sources
- [ ] All Tier 1 log sources connected and validated
- [ ] All Tier 2 log sources connected and validated
- [ ] Parser validation complete for all connected sources
- [ ] No critical log sources with 0 events in the last 24 hours

#### Detection Rules
- [ ] All use case rules from the approved list are active
- [ ] All rules verified against test events
- [ ] Alert routing confirmed — notifications arriving at correct destination
- [ ] False positive rate within acceptable threshold

#### Tuning
- [ ] All high-FP rules tuned to acceptable rate
- [ ] Allowlist and suppression list documented and reviewed
- [ ] UEBA baselines established (if applicable)

#### Knowledge Transfer
- [ ] All training sessions completed
- [ ] All documentation delivered to client
- [ ] All runbooks reviewed with client team
- [ ] Client team has successfully completed at least one simulated alert investigation

### 10.6 Ongoing Support Model

| Support Type | Description | Contact Method |
|---|---|---|
| **Break-Fix Support** | Platform errors, log source connectivity failures, parser issues | [Support email / ticket portal] |
| **SLA Response Time (Critical)** | Response within [X hours] for critical platform failures | [Phone / PagerDuty] |
| **SLA Response Time (Standard)** | Response within [X business days] for standard issues | [Ticket portal] |
| **Monthly Health Check** | Monthly review of SIEM health using the SIEM Health Check Checklist | Scheduled call |
| **Quarterly Business Review** | Quarterly review of detection effectiveness, rule updates, expansion opportunities | Scheduled meeting |
| **Ongoing Tuning Support** | Ad-hoc tuning support for new FP patterns or rule adjustments | [Support email] |
| **New Log Source Onboarding** | Support for adding additional log sources post-go-live | [Ticket portal + SOW] |

---

## 11. Project Risks and Mitigation

| # | Risk | Probability | Impact | Mitigation | Owner |
|---|---|---|---|---|---|
| 1 | Log source access delayed by client change control process | High | High | Identify change control requirements in Phase 1; submit requests early; use phased approach | Client IT Lead |
| 2 | Log volume significantly higher than estimated, driving up cost | Medium | High | Volume estimates validated in Phase 2; cost alerts configured; filtering options evaluated before go-live | Lead SIEM Engineer |
| 3 | Client staff availability limited during onboarding (competing priorities) | High | Medium | Confirm stakeholder time commitments at kickoff; identify backup contacts for each role | Consulting PM |
| 4 | Cloud firewall / security group rules blocking log forwarding | Medium | High | Network connectivity testing in Phase 3 before log sources configured; firewall rules submitted with lead time | Client IT Lead |
| 5 | Parser unavailable for non-standard log source | Low | Medium | Custom parser development scoped as contingency; fallback: raw log ingestion with manual field extraction | Lead SIEM Engineer |
| 6 | Platform licensing quota reached before all sources connected | Low | High | Volume estimates reviewed before go-live; quota alerts configured in Phase 3; license expansion path confirmed | Client Sponsor |
| 7 | Key client stakeholder turnover during project | Low | High | Document all decisions and configurations throughout; knowledge transfer to multiple client staff, not just one | Consulting PM |
| 8 | High false positive rate preventing analyst adoption | Medium | High | Dedicated tuning phase (Phase 6) with explicit FP-rate success criteria; tuning supported for 4 weeks post-go-live | Lead SIEM Engineer |
| 9 | Compliance audit occurs before SIEM fully operational | Medium | High | Identify compliance audit dates in Phase 1; prioritize log sources and reports critical to that audit first | Client Compliance |
| 10 | Integration dependency on third-party vendor (email gateway vendor, EDR vendor) | Medium | Medium | Identify vendor dependencies in Phase 2; engage vendors early; maintain alternative connector options | Support Engineer |

---

## 12. Project Sign-Off

### Phase Sign-Off Log

| Phase | Completion Date | Client Sign-Off | Consulting Sign-Off | Notes |
|---|---|---|---|---|
| Phase 1: Discovery and Requirements | [Date] | [Client Signature / Initials] | [Consultant Initials] | |
| Phase 2: Log Source Identification and Prioritization | [Date] | | | |
| Phase 3: SIEM Infrastructure Setup | [Date] | | | |
| Phase 4: Log Source Connector Setup | [Date] | | | |
| Phase 5: Alert Rule Configuration | [Date] | | | |
| Phase 6: Tuning and Optimization | [Date] | | | |
| Phase 7: Handoff and Knowledge Transfer | [Date] | | | |

### Final Go-Live Sign-Off

By signing below, [Client Name] acknowledges that the SIEM onboarding engagement has been completed in accordance with the project plan and that the go-live criteria checklist has been satisfied.

| Role | Name | Signature | Date |
|---|---|---|---|
| Client Project Sponsor | [Name] | _____________________________ | [Date] |
| Client Security Lead | [Name] | _____________________________ | [Date] |
| Consulting Engagement Manager | [Name] | _____________________________ | [Date] |
| Lead SIEM Engineer | [Name] | _____________________________ | [Date] |

**Exceptions or Outstanding Items at Go-Live:**

[List any items not fully complete at go-live with agreed remediation timeline]

---

> **Document Control**
> Project Plan Version: 1.0 | Owner: [Consulting PM] | Client: [Client Name]
> This document contains confidential engagement information. Do not distribute outside the project team.
