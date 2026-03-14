# Log Source Priority Matrix
**Client:** [Client Name]
**Date:** [Date]
**Prepared By:** [Consultant Name]
**SIEM Platform:** [SIEM Platform]

---

## Table of Contents

1. [How to Use This Matrix](#1-how-to-use-this-matrix)
2. [Priority Tier Definitions](#2-priority-tier-definitions)
3. [Master Priority Matrix](#3-master-priority-matrix)
4. [By Environment Type — Recommended Priority Order](#4-by-environment-type--recommended-priority-order)
5. [Quick Win vs. High Effort Matrix](#5-quick-win-vs-high-effort-matrix)
6. [Client-Specific Priority Worksheet](#6-client-specific-priority-worksheet)

---

## 1. How to Use This Matrix

This matrix provides a standardized ranking of log source categories based on their detection value, compliance contribution, and MITRE ATT&CK coverage. Use this matrix to:

1. **Prioritize which log sources to onboard first** — start with Tier 1 sources before moving to lower tiers
2. **Justify prioritization decisions** to client stakeholders — use the detection value scores and coverage columns in those conversations
3. **Tailor the priority order** to the client's environment type (Section 4) — a cloud-native AWS environment will have different priorities than an on-premises Active Directory shop
4. **Identify quick wins** (Section 5) — high-value sources that are also fast to connect, enabling early alert activity
5. **Complete the client-specific worksheet** (Section 6) — fill in actual volumes and owners for each source in the client environment

**Detection Value Score (1–10):**
- **9–10:** Direct, high-confidence detection of critical attack categories; must have
- **7–8:** Strong detection value across multiple attack categories; should have early
- **5–6:** Meaningful detection coverage; adds breadth; valuable when Tier 1/2 are complete
- **3–4:** Useful supplemental data; enhances existing detections; onboard when capacity allows
- **1–2:** Primarily useful for enrichment or specific niche use cases; low standalone value

**Onboarding Complexity:**
- **Low:** Native connector, standard syslog or API pull, minimal configuration, typically operational in < 1 day
- **Medium:** Requires source-side configuration, credential provisioning, or parser tuning; typically 1–3 days
- **High:** Custom connector, agent deployment at scale, complex filtering, or significant source-side changes; typically 3–10 days or more

---

## 2. Priority Tier Definitions

| Tier | Label | Timeline | Description |
|---|---|---|---|
| **Tier 1** | Critical | Onboard in Week 1–2 | Highest detection value. These sources are required to detect the most common and highest-impact attack scenarios. A SIEM without Tier 1 sources is not providing meaningful security value. |
| **Tier 2** | High | Onboard within 30 days | Strong detection value that significantly broadens coverage. Tier 2 sources typically enable detection of a second layer of attack techniques and are required for most compliance frameworks. |
| **Tier 3** | Medium | Onboard within 60 days | Valuable for detection breadth, enrichment, and compliance reporting. Tier 3 sources enhance the quality of alerts from Tier 1 and 2 sources through additional context and correlation. |
| **Tier 4** | Low / Supplemental | Onboard as capacity allows | Nice-to-have sources. These may generate high volumes at lower detection value, serve specific niche use cases, or require significant effort relative to their return. |

---

## 3. Master Priority Matrix

| Rank | Log Source | Tier | Detection Value (1–10) | Compliance Value | Coverage (MITRE ATT&CK Tactics) | Avg Daily Volume | Onboarding Complexity | Recommended Order |
|---|---|---|---|---|---|---|---|---|
| 1 | **Active Directory / Domain Controller Logs** (Windows Security Event Log — Event IDs 4624, 4625, 4648, 4720, 4728, 4732, 4740, 4768, 4769, 4776) | Tier 1 | 10 | PCI 8.x, 10.x; HIPAA 164.312; SOC 2 CC6; CMMC AU.2.042 | Initial Access, Credential Access, Privilege Escalation, Lateral Movement, Persistence, Defense Evasion | High (5–50 GB/day depending on org size) | Medium | **1st** |
| 2 | **Perimeter Firewall Logs** (allow/deny, connection state, NAT) | Tier 1 | 9 | PCI 1.x, 10.x; HIPAA 164.312(e); CMMC SC.3.177 | Initial Access, Command and Control, Exfiltration, Discovery | Very High (10–100+ GB/day) | Low–Medium | **2nd** |
| 3 | **Endpoint Detection and Response (EDR) / AV Logs** (CrowdStrike, SentinelOne, Microsoft Defender for Endpoint, Carbon Black) | Tier 1 | 10 | PCI 5.x; HIPAA 164.312; CMMC SI.1.210 | Execution, Persistence, Privilege Escalation, Defense Evasion, Credential Access, Lateral Movement, Collection | Medium–High (2–20 GB/day) | Low–Medium (cloud EDR APIs simple) | **3rd** |
| 4 | **Cloud IAM Logs** (AWS CloudTrail, Azure AD Sign-in/Audit, GCP Cloud Audit Logs — IAM events) | Tier 1 | 9 | PCI 8.x, 10.x; SOC 2 CC6; CMMC AC.2.006 | Initial Access, Privilege Escalation, Persistence, Defense Evasion, Credential Access | Medium (1–10 GB/day) | Low–Medium (API pull or native connector) | **4th** |
| 5 | **Email Gateway Logs** (Microsoft Defender for Office 365, Proofpoint, Mimecast, Google Workspace mail logs) | Tier 1 | 9 | PCI 12.x; HIPAA 164.308; CMMC AT.2.056 | Initial Access (phishing), Execution (malicious attachment), Credential Access (BEC) | Medium (1–10 GB/day) | Low–Medium | **5th** |
| 6 | **VPN / Remote Access Logs** (Cisco AnyConnect, Palo Alto GlobalProtect, Fortinet SSL VPN, Citrix Gateway) | Tier 2 | 8 | PCI 8.x, 10.x; HIPAA 164.312; SOC 2 CC6 | Initial Access, Credential Access, Lateral Movement | Low–Medium (0.5–5 GB/day) | Low–Medium | **6th** |
| 7 | **DNS Logs** (Windows DNS, BIND, Umbrella/Cisco DNS, Infoblox) | Tier 2 | 8 | PCI 10.x; CMMC SC.3.190 | Command and Control (DNS beaconing, DNS tunneling), Initial Access (malicious domain resolution), Exfiltration | Very High (5–50+ GB/day; sampling recommended) | Medium | **7th** |
| 8 | **Web Proxy / Secure Web Gateway Logs** (Zscaler, Palo Alto, Bluecoat, Cisco WSA) | Tier 2 | 8 | PCI 10.x, 12.x; CMMC SC.3.192 | Command and Control, Exfiltration, Initial Access (malware download) | High (5–50 GB/day) | Low–Medium | **8th** |
| 9 | **Cloud Infrastructure and Service Logs** (AWS CloudTrail — non-IAM events, S3 access, EC2; Azure Activity Logs; GCP) | Tier 2 | 8 | PCI 10.x; SOC 2 CC7; CMMC AU.2.042 | Privilege Escalation, Persistence, Defense Evasion, Exfiltration (cloud storage) | Medium–High (varies widely by cloud footprint) | Medium | **9th** |
| 10 | **Identity Provider / SSO Logs** (Okta, Azure AD, Ping, Duo) | Tier 2 | 8 | PCI 8.x; SOC 2 CC6; HIPAA 164.312 | Initial Access, Credential Access, Privilege Escalation | Low–Medium (0.5–5 GB/day) | Low (API pull standard) | **10th** |
| 11 | **DHCP Logs** (Windows DHCP Server, ISC DHCP, IPAM) | Tier 3 | 6 | PCI 10.x (asset tracking) | Discovery (IP-to-hostname resolution enrichment), Lateral Movement context | Medium (1–10 GB/day) | Low | **11th** |
| 12 | **Linux / Unix System Logs** (/var/log/auth.log, /var/log/secure, auditd, syslog) | Tier 3 | 7 | PCI 10.x; HIPAA 164.312; CMMC AU.2.042 | Privilege Escalation, Credential Access, Lateral Movement, Persistence | Medium (varies; 1–20 GB/day for large server estates) | Medium (agent or syslog per host) | **12th** |
| 13 | **Database Audit Logs** (Oracle Audit, Microsoft SQL Server, MySQL, PostgreSQL pgaudit) | Tier 3 | 7 | PCI 10.x; HIPAA 164.312 (PHI access); SOC 2 CC6 | Collection (data theft), Initial Access (SQL injection), Insider Threat | Medium (1–20 GB/day; depends on database activity) | High (DBA coordination, performance impact concerns) | **13th** |
| 14 | **NetFlow / IPFIX / Network Traffic Metadata** (Cisco NetFlow, Juniper J-Flow, sFlow, Zeek/Bro) | Tier 4 | 5 | PCI 10.x (network monitoring) | Discovery, Lateral Movement, Exfiltration, Command and Control | Very High (10–500+ GB/day depending on network size) | High (requires network tap or flow exporter; high volume management) | **14th** |

> **Note on NetFlow:** NetFlow is Tier 4 as a standalone SIEM source because its detection value per gigabyte of storage is low without significant enrichment and correlation against other sources. It is very high value in a dedicated NDR (Network Detection and Response) tool (Darktrace, ExtraHop, Vectra, Corelight) and those alerts/findings can be ingested into the SIEM at much lower volume for higher-value correlation.

---

## 4. By Environment Type — Recommended Priority Order

### 4.1 Microsoft-Dominant Environment (Heavy AD, M365, Azure)

Organizations running primarily Windows infrastructure, Microsoft 365, Azure AD, and Azure cloud services.

| Priority | Log Source | Rationale |
|---|---|---|
| 1st | Active Directory / Domain Controller | Core identity plane; all authentication flows through AD |
| 2nd | Microsoft Defender for Office 365 (Email) | M365 email is primary phishing vector; native connector easy to enable |
| 3rd | Azure AD Sign-in and Audit Logs | Cloud identity complement to on-prem AD; covers M365 service access |
| 4th | Microsoft Defender for Endpoint (EDR) | Native MDE integration; agent already deployed via Intune/SCCM in most cases |
| 5th | Perimeter Firewall | Network visibility; typically on-prem Palo Alto, Fortinet, or Azure Firewall |
| 6th | VPN / Remote Access | Always high value; often Microsoft DirectAccess, Azure P2S VPN, or third-party |
| 7th | Microsoft Defender for Cloud (Azure security alerts) | Cloud workload protection; easy native connector |
| 8th | Azure Activity Logs (non-IAM) | Azure resource changes; infrastructure visibility |
| 9th | DNS (Windows DNS) | C2 detection; Windows DNS logs via ETW or Sysmon |
| 10th | DHCP | IP-to-hostname enrichment; Windows DHCP easy to configure |

**Microsoft Sentinel Note:** In Sentinel, Microsoft-origin sources (Azure AD, Defender XDR, M365) often ingest at no additional cost under the Microsoft benefit. Prioritize connecting these first as they deliver high value at zero incremental ingestion cost.

---

### 4.2 AWS-Primary Cloud Environment

Organizations with their primary infrastructure in AWS and limited on-premises footprint.

| Priority | Log Source | Rationale |
|---|---|---|
| 1st | AWS CloudTrail (all management events) | Complete IAM and API audit trail; foundational for cloud detection |
| 2nd | Amazon GuardDuty findings | Pre-processed threat detection for AWS; ingest findings, not raw logs |
| 3rd | AWS IAM Access Advisor and Credential Reports | Privilege sprawl detection, unused credentials identification |
| 4th | EDR on EC2 workloads | Endpoint visibility within cloud VMs |
| 5th | VPC Flow Logs (sampled) | Network visibility within AWS VPCs; filter to reduce volume |
| 6th | AWS S3 Access Logs (for sensitive buckets) | Data exfiltration detection from critical S3 buckets |
| 7th | Email Gateway (SES, Google Workspace, M365) | Email threat detection; platform-independent requirement |
| 8th | Identity Provider (Okta, AWS SSO / IAM Identity Center) | SSO and federated identity visibility |
| 9th | AWS Config (configuration change events) | Infrastructure compliance drift; resource configuration changes |
| 10th | Application Load Balancer / WAF Logs | Web application attack detection |

---

### 4.3 Hybrid On-Premises and Cloud Environment

Organizations with significant on-premises infrastructure alongside one or more cloud providers.

| Priority | Log Source | Rationale |
|---|---|---|
| 1st | Active Directory / Domain Controller | On-prem identity still core in hybrid; Kerberos, LDAP, NTLM |
| 2nd | Cloud IAM (AWS CloudTrail and/or Azure AD) | Cloud identity plane complement |
| 3rd | Perimeter Firewall (on-prem) | Network boundary visibility |
| 4th | EDR (covers on-prem endpoints and cloud VMs) | Unified endpoint detection |
| 5th | VPN / Remote Access | Hybrid access control — who is connecting from where |
| 6th | Email Gateway | Phishing is environment-agnostic |
| 7th | Identity Provider / SSO (Okta, Azure AD hybrid join) | Federation layer bridging on-prem and cloud identity |
| 8th | Cloud storage / services logs (S3, Blob, etc.) | Cloud data plane visibility |
| 9th | Web Proxy or CASB | Unified web egress visibility across on-prem and cloud users |
| 10th | DNS (on-prem DNS + cloud DNS resolver logs) | C2 detection; hybrid DNS requires both sources |

---

### 4.4 Small Business — Must-Have 5 Sources First

For organizations with limited resources that must prioritize ruthlessly. These five sources provide the highest security return for the smallest operational investment.

| Priority | Log Source | Why It Is Non-Negotiable |
|---|---|---|
| **1st** | Active Directory or Cloud Identity (Azure AD / Okta) | Identity compromise is the most common attack vector; no detection is possible without authentication logs |
| **2nd** | Endpoint / EDR | Malware execution, ransomware, and attacker tooling is detected here; if you can only have one detection source, make it your endpoints |
| **3rd** | Perimeter Firewall | Network boundary — command-and-control detection, unauthorized access from internet, exfiltration |
| **4th** | Email Gateway | Phishing delivers the majority of initial access; email logs are critical for catching the attack before the endpoint is compromised |
| **5th** | VPN / Remote Access | Remote work has made VPN the de facto network perimeter; authentication and session logs here are essential |

**Advice for SMB:** These five sources, properly configured and with a baseline ruleset, will detect the most common attack patterns targeting small businesses: ransomware delivered via phishing, credential stuffing, brute force, and basic lateral movement. Add DNS and web proxy next once the first five are stable.

---

## 5. Quick Win vs. High Effort Matrix

Use this 2x2 to sequence your log source onboarding for maximum early impact.

```
                    HIGH DETECTION VALUE
                           |
     START HERE            |    PLAN CAREFULLY
   (Quick Win /            |    (Hard / High Value)
    High Value)            |
                           |
  Active Directory         |    Database Audit Logs
  EDR / Endpoint          |    NetFlow (with enrichment)
  Email Gateway            |    Linux Auditd at scale
  Cloud IAM (API pull)     |    Custom app logs
  Okta / SSO              |    Industrial/OT logs
                           |
  ─────────────────────────┼─────────────────────────
                           |
   FILL IN EARLY           |    CONSIDER LATER
   (Quick Win /            |    (Hard / Lower Value)
    Lower Value)           |
                           |
  DHCP logs               |    NetFlow standalone
  VPN logs (standard)     |    Legacy application logs
  GuardDuty findings      |    Mainframe logs
  Windows DNS             |    Physical access control
  Azure Activity Logs     |    IoT device logs (non-critical)
                           |
                    LOW DETECTION VALUE
```

**START HERE — Quick Win / High Value:**
These sources have both high detection value and low-to-medium onboarding complexity. Prioritize these first to get meaningful detections running as early as possible. Early alert activity builds confidence with the client and demonstrates SIEM value within the first weeks.

**PLAN CAREFULLY — Hard / High Value:**
These sources have high detection value but require significant effort to onboard correctly. Plan these early in the project timeline, initiate the required coordination (DBA approval for database logs, network engineer for packet capture infrastructure), and execute them in parallel with the Quick Win sources rather than sequentially after them.

**FILL IN EARLY — Quick Win / Lower Value:**
These sources are fast to connect and provide enrichment value or compliance coverage, but their standalone detection value is lower. Connect them once the Start Here sources are stable — they improve the quality of detections from higher-priority sources.

**CONSIDER LATER — Hard / Lower Value:**
These sources require significant effort at lower standalone detection return. Evaluate whether the detection value justifies the onboarding cost in this specific client environment. In some cases (e.g., a manufacturing client where OT logs are critical), these move up the priority matrix — use the client-specific worksheet to make that adjustment.

---

## 6. Client-Specific Priority Worksheet

Complete this worksheet based on the actual client environment. Override the standard tier assignments where the client's specific risk profile, compliance requirements, or environment warrants a different priority.

| Rank | Log Source | Standard Tier | Client-Adjusted Tier | Reason for Adjustment | Actual Daily Volume | Source Owner | Connector Method | Target Onboard Date | Status |
|---|---|---|---|---|---|---|---|---|---|
| 1 | [Log Source] | [Tier 1–4] | [Adjusted Tier] | [Rationale if adjusted] | [GB/day or EPS] | [Team/Name] | [Syslog/API/Agent/S3/Native] | [Date] | [ ] Not Started / [ ] In Progress / [ ] Complete |
| 2 | | | | | | | | | |
| 3 | | | | | | | | | |
| 4 | | | | | | | | | |
| 5 | | | | | | | | | |
| 6 | | | | | | | | | |
| 7 | | | | | | | | | |
| 8 | | | | | | | | | |
| 9 | | | | | | | | | |
| 10 | | | | | | | | | |
| 11 | | | | | | | | | |
| 12 | | | | | | | | | |
| 13 | | | | | | | | | |
| 14 | | | | | | | | | |
| 15 | | | | | | | | | |
| 16 | | | | | | | | | |
| 17 | | | | | | | | | |
| 18 | | | | | | | | | |
| 19 | | | | | | | | | |
| 20 | | | | | | | | | |

### Worksheet Notes

**Tier Adjustment Guidance:**
- Move a source UP a tier if: it covers a specific compliance requirement with an imminent audit deadline, it is the primary vector for a threat the client has previously experienced, or the client's business makes it uniquely high-risk (e.g., email logs move to #1 for a financial services firm that recently experienced BEC)
- Move a source DOWN a tier if: the system is end-of-life and will be decommissioned within 90 days, the source generates extremely high volume with filters not available, or the client has a dedicated tool providing equivalent coverage (e.g., a mature NDR solution may reduce the urgency of raw NetFlow ingestion)

**Volume Validation:**
Actual client volumes should be validated against existing log infrastructure (syslog server statistics, cloud storage metrics, vendor dashboards) during Phase 2 of the onboarding project. Adjust the worksheet when actual measurements are available.

**Sign-Off:**
This client-specific priority worksheet should be reviewed and signed off by [Client Security Lead] before Phase 4 (Log Source Connector Setup) begins.

| Sign-Off | Name | Date |
|---|---|---|
| Client Security Lead | [Name] | [Date] |
| Lead SIEM Engineer | [Name] | [Date] |

---

> **Document Control**
> Version: 1.0 | Owner: [Lead SIEM Engineer] | Client: [Client Name]
> Review: Revisit this worksheet at each quarterly business review and update as new sources are identified.
