# Technical Security Findings Report
**Client:** [Client Name]
**Assessment Date Range:** [Start Date] — [End Date]
**Report Date:** [Report Date]
**Report Version:** [1.0]
**Classification:** CONFIDENTIAL — RESTRICTED DISTRIBUTION

---

> **CONFIDENTIALITY NOTICE**
> This report contains sensitive technical security information prepared exclusively for [Client Name]. It is intended solely for authorized technical and security personnel listed in the distribution list below. Unauthorized disclosure, reproduction, or transmission of this document — in whole or in part — is strictly prohibited. If you have received this document in error, please contact [Consultant Contact Email] immediately and destroy all copies. This document should be stored in a secure location and disposed of in accordance with [Client Name]'s data handling policy.

**Distribution List:**

| Name | Title | Organization | Authorization Level |
|---|---|---|---|
| [Name] | [Title, e.g., CISO / IT Director] | [Client Name] | Full Report |
| [Name] | [Title, e.g., Systems Administrator] | [Client Name] | Full Report |
| [Name] | [Title, e.g., Consultant Lead] | [Firm Name] | Full Report |
| [Name] | [Title] | [Organization] | [Executive Summary Only] |

---

## Table of Contents

1. [Report Overview](#1-report-overview)
2. [Scope Statement](#2-scope-statement)
3. [Methodology](#3-methodology)
4. [Executive Summary](#4-executive-summary)
5. [Findings Summary Table](#5-findings-summary-table)
6. [Severity Distribution](#6-severity-distribution)
7. [Detailed Findings](#7-detailed-findings)
   - [FIND-001: Unpatched Critical Vulnerabilities on Internet-Facing Servers](#find-001)
   - [FIND-002: Multi-Factor Authentication Not Enforced for Remote Access](#find-002)
   - [FIND-003: Default Credentials on Network Devices](#find-003)
8. [Appendix A: Full Asset List](#appendix-a-full-asset-list)
9. [Appendix B: Tools and Versions Used](#appendix-b-tools-and-versions-used)
10. [Appendix C: Scan Configurations](#appendix-c-scan-configurations)
11. [Appendix D: Methodology Details](#appendix-d-methodology-details)
12. [Revision History](#revision-history)

---

## 1. Report Overview

### 1.1 Purpose

This report documents the findings, evidence, and remediation recommendations resulting from the security assessment conducted for [Client Name] during the period of [Start Date] through [End Date]. The assessment was performed by [Firm Name] under the terms of [Statement of Work / Contract Reference Number].

### 1.2 Assessment Team

| Name | Role | Certifications |
|---|---|---|
| [Consultant Name] | Lead Assessor | [e.g., CISSP, CEH, OSCP] |
| [Consultant Name] | Technical Analyst | [e.g., Security+, GPEN] |
| [Consultant Name] | Report Author | [e.g., CISM] |

### 1.3 Tools Used

| Tool | Version | Purpose |
|---|---|---|
| Nessus Professional | [X.X.X] | Vulnerability scanning |
| Nmap | [X.XX] | Network discovery and port scanning |
| Metasploit Framework | [X.X.X] | Exploitation validation (authorized) |
| Burp Suite Professional | [X.X.X] | Web application testing |
| Bloodhound / SharpHound | [X.X.X] | Active Directory enumeration |
| CIS-CAT Pro | [X.X.X] | CIS benchmark compliance scanning |
| [Additional Tool] | [Version] | [Purpose] |

### 1.4 Assessment Dates

| Activity | Date(s) |
|---|---|
| Kickoff and scoping call | [Date] |
| Reconnaissance and discovery | [Date] — [Date] |
| Vulnerability scanning | [Date] — [Date] |
| Exploitation / validation testing | [Date] — [Date] |
| Report drafting | [Date] — [Date] |
| Draft report delivered | [Date] |
| Final report delivered | [Date] |

---

## 2. Scope Statement

### 2.1 In-Scope Systems and IP Ranges

| Asset Group | IP Range / Hostname | Description |
|---|---|---|
| Corporate network | [e.g., 10.0.0.0/16] | Internal corporate LAN |
| DMZ / perimeter | [e.g., 192.168.100.0/24] | Internet-facing servers and services |
| Web servers | [e.g., webserver01.client.com, 203.0.113.10] | Public-facing web applications |
| Active Directory | [e.g., dc01.corp.client.com] | Domain controllers |
| Remote access infrastructure | [e.g., vpn.client.com] | VPN concentrators and remote access |
| [Additional asset group] | [Range / hostname] | [Description] |

**Total hosts in scope:** [X]
**Total subnets in scope:** [X]

### 2.2 Cloud Environments Assessed

| Provider | Account / Subscription ID | Regions | Services in Scope |
|---|---|---|---|
| [e.g., AWS] | [Account ID] | [e.g., us-east-1, us-west-2] | [e.g., EC2, S3, IAM, RDS] |
| [e.g., Microsoft Azure] | [Subscription ID] | [e.g., East US] | [e.g., Virtual Machines, Azure AD, Storage] |
| [e.g., Google Cloud] | [Project ID] | [e.g., us-central1] | [e.g., Compute Engine, Cloud IAM] |

### 2.3 Excluded Systems

The following systems were explicitly excluded from the assessment scope per client request or technical constraints:

| Excluded Asset | Reason for Exclusion |
|---|---|
| [e.g., Production POS terminals] | [e.g., Operational risk — assessed separately by PCI QSA] |
| [e.g., 10.50.0.0/24] | [e.g., Third-party managed — outside client control] |
| [e.g., legacy-app01.client.com] | [e.g., Scheduled for decommission — risk accepted by client] |

---

## 3. Methodology

### 3.1 Assessment Approach

This assessment followed a [black-box / grey-box / white-box] methodology. The engagement was conducted in [X] phases:

1. **Discovery and Enumeration** — Network scanning to identify live hosts, open ports, and running services without authentication.
2. **Authenticated Scanning** — Credentialed vulnerability scans to identify missing patches, misconfigurations, and software vulnerabilities at the OS and application level.
3. **Targeted Exploitation (Authorized)** — Manual validation and controlled exploitation of select findings to confirm exploitability and assess true business impact.
4. **Configuration Review** — Manual review of system and application configurations against CIS Benchmark standards.
5. **Reporting** — Findings documented with evidence, risk scoring, and actionable remediation guidance.

### 3.2 Authentication Levels

| Scan Type | Authentication | Credential Type |
|---|---|---|
| Network discovery | Unauthenticated | None |
| Vulnerability scanning — Windows | Authenticated | [e.g., Domain admin service account] |
| Vulnerability scanning — Linux | Authenticated | [e.g., SSH key-based — sudo-enabled account] |
| Web application scanning | Authenticated | [e.g., Application-level test account] |
| Cloud configuration review | Authenticated | [e.g., Read-only IAM role] |

### 3.3 Risk Scoring

Findings are rated using the Common Vulnerability Scoring System (CVSS) v3.1 base score as the primary scoring mechanism, supplemented by contextual factors including asset criticality, network exposure, and ease of exploitation.

| Severity | CVSS Score Range |
|---|---|
| Critical | 9.0 — 10.0 |
| High | 7.0 — 8.9 |
| Medium | 4.0 — 6.9 |
| Low | 0.1 — 3.9 |
| Informational | N/A |

---

## 4. Executive Summary

[One-page maximum. Provide a concise, technically-aware summary covering: the overall security posture, number and severity distribution of findings, most significant risks identified, standout positives, and the top 2-3 remediation priorities. This section may be shared with senior technical leadership.]

During the assessment period of [Start Date] through [End Date], [Firm Name] conducted a comprehensive security assessment of [Client Name]'s environment encompassing [X] hosts across [X] subnets and [X] cloud environments. The assessment identified a total of **[X] findings**: [X] Critical, [X] High, [X] Medium, [X] Low, and [X] Informational.

The most significant risks identified are concentrated in [key area, e.g., patch management and privileged access management]. [X] critical-severity findings were identified, all of which are actively exploitable with publicly available tools. Immediate remediation of these findings should be prioritized before any other security activities.

Positive observations include [e.g., consistent use of endpoint protection across workstations, active monitoring of external perimeter via SIEM integration, and evidence of a mature change management process for firewall rule modifications].

The three highest-priority remediation actions are: (1) [action], (2) [action], and (3) [action]. Full details and remediation guidance are provided in Section 7.

---

## 5. Findings Summary Table

| Finding ID | Title | Severity | CVSS Score | Affected Assets | CIS Control | Status |
|---|---|---|---|---|---|---|
| FIND-001 | Unpatched Critical Vulnerabilities on Internet-Facing Servers | Critical | 9.8 | webserver01, webserver02 | CIS 7 — Continuous Vulnerability Management | Open |
| FIND-002 | Multi-Factor Authentication Not Enforced for Remote Access | High | 8.1 | vpn.client.com, RDP gateway | CIS 6 — Access Control Management | Open |
| FIND-003 | Default Credentials on Network Devices | Critical | 9.1 | switch-core-01, fw-perimeter-01 | CIS 4 — Secure Configuration | Open |
| FIND-004 | Sensitive Data Transmitted Over Unencrypted Channels | High | 7.5 | app-server-03, db-server-01 | CIS 3 — Data Protection | Open |
| FIND-005 | Excessive Privileged Account Permissions (Principle of Least Privilege Violation) | Medium | 6.3 | Active Directory — [Domain Name] | CIS 5 — Account Management | Open |

---

## 6. Severity Distribution

> **[CHART PLACEHOLDER: Severity Distribution — Findings by Severity]**
> *Replace this block with a bar chart or pie chart showing the count of findings by severity category: Critical ([X]), High ([X]), Medium ([X]), Low ([X]), Informational ([X]).*
> *Recommended chart type: Horizontal bar chart with color coding — Critical (red), High (orange), Medium (yellow), Low (blue), Informational (grey).*

| Severity | Count | Percentage |
|---|---|---|
| Critical | [X] | [X%] |
| High | [X] | [X%] |
| Medium | [X] | [X%] |
| Low | [X] | [X%] |
| Informational | [X] | [X%] |
| **Total** | **[X]** | **100%** |

---

## 7. Detailed Findings

*Use the template below for each finding. Replicate this block for every identified finding. Assign sequential Finding IDs (FIND-001, FIND-002, etc.).*

---

### FIND-001

**Finding ID:** FIND-001
**Title:** Unpatched Critical Vulnerabilities on Internet-Facing Servers
**Severity:** Critical
**CVSS Score:** 9.8
**CVSS Vector String:** `CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H`
**CVE Reference(s):** CVE-[YYYY-NNNNN], CVE-[YYYY-NNNNN]
**CIS Control Mapping:** CIS Control 7 — Continuous Vulnerability Management (Safeguard 7.3: Perform Automated Operating System Patch Management; Safeguard 7.4: Perform Automated Application Patch Management)
**Affected Assets:**

- `webserver01.client.com` (IP: 203.0.113.10) — Windows Server 2019
- `webserver02.client.com` (IP: 203.0.113.11) — Windows Server 2019

**Description:**
Both internet-facing web servers are missing [X] critical security patches, including updates addressing [CVE-YYYY-NNNNN], a remote code execution vulnerability in [Affected Component, e.g., Microsoft IIS / Apache HTTP Server] with a CVSS base score of 9.8. These patches were released on [Patch Release Date] and have been publicly available for [X] days at the time of assessment. Exploit code for these vulnerabilities is publicly available in the Metasploit Framework and on GitHub, enabling unauthenticated remote exploitation by attackers of any skill level.

**Business Impact:**
Successful exploitation of these vulnerabilities would allow an unauthenticated remote attacker to execute arbitrary code on the affected web servers with SYSTEM-level privileges. This could result in complete compromise of the servers, unauthorized access to data processed by these systems, lateral movement into the internal network, deployment of ransomware, or exfiltration of sensitive customer or business data. These servers are internet-accessible, meaning exploitation requires no prior access to the organization's network.

**Evidence / Proof of Concept:**

> **[SCREENSHOT PLACEHOLDER: Nessus scan output showing CVE-YYYY-NNNNN on webserver01]**

> **[SCREENSHOT PLACEHOLDER: Metasploit module execution confirming exploitability — command shell output showing SYSTEM access on webserver01]**

```
# Example command output (sanitized):
msf6 exploit([module_name]) > run
[*] Started reverse TCP handler on [attacker_ip]:4444
[*] Sending exploit...
[+] [Target IP] - Shell opened — [SYSTEM shell prompt shown]
Microsoft Windows [Version X.X.XXXXX]
(c) Microsoft Corporation. All rights reserved.

C:\Windows\system32> whoami
nt authority\system
```

*Note: Full exploitation evidence including screen recordings is available upon request under secure delivery.*

**Remediation Recommendation:**

1. Apply all outstanding critical and high-severity Windows updates to `webserver01` and `webserver02` immediately, prioritizing patches for [CVE-YYYY-NNNNN].
2. Reboot servers during the next approved maintenance window after patch application.
3. Verify successful patch installation using the Nessus authenticated scan post-remediation.
4. Establish a monthly patching cycle with emergency patching procedures for critical CVEs (CVSS ≥ 9.0) within 72 hours of vendor release.
5. Consider deploying a web application firewall (WAF) as a compensating control while patches are applied.

**References:**

- [https://nvd.nist.gov/vuln/detail/CVE-YYYY-NNNNN](https://nvd.nist.gov/vuln/detail/CVE-YYYY-NNNNN)
- [Vendor Security Advisory URL]
- CIS Control 7: [https://www.cisecurity.org/controls/continuous-vulnerability-management](https://www.cisecurity.org/controls/continuous-vulnerability-management)

**Status:** Open
**Date Identified:** [Date]
**Remediation Target Date:** [Date — e.g., within 15 days per SLA]

---

### FIND-002

**Finding ID:** FIND-002
**Title:** Multi-Factor Authentication Not Enforced for Remote Access
**Severity:** High
**CVSS Score:** 8.1
**CVSS Vector String:** `CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:H/A:N`
**CVE Reference(s):** N/A (Configuration Finding)
**CIS Control Mapping:** CIS Control 6 — Access Control Management (Safeguard 6.3: Require MFA for Externally-Exposed Applications; Safeguard 6.5: Require MFA for Administrative Access)
**Affected Assets:**

- `vpn.client.com` (IP: 203.0.113.20) — [VPN Product, e.g., Cisco AnyConnect / Palo Alto GlobalProtect]
- RDP Gateway: `rdgw.client.com` (IP: 203.0.113.21)
- [X] additional remote access endpoints

**Description:**
Multi-factor authentication (MFA) is not enforced for any remote access pathways into the [Client Name] environment, including VPN connections and Remote Desktop Protocol (RDP) gateway access. Authentication relies solely on username and password credentials. Testing confirmed that access can be achieved with valid credentials alone, with no secondary factor required. Additionally, [X] accounts were identified with passwords meeting minimum complexity requirements but classified as common or previously breached passwords based on comparison against the HaveIBeenPwned corpus.

**Business Impact:**
Remote access systems are among the most frequently targeted attack vectors in ransomware and business email compromise campaigns. Without MFA, a single stolen or guessed password is sufficient for an attacker to gain full network access from anywhere on the internet. Credential theft via phishing, password spraying, or credential stuffing attacks is trivial and automated. [Client Name]'s cyber insurance policy may also require MFA on remote access — failure to comply could affect coverage in the event of a breach.

**Evidence / Proof of Concept:**

> **[SCREENSHOT PLACEHOLDER: Successful VPN authentication using single-factor (username + password only) — connection log showing no MFA challenge]**

> **[SCREENSHOT PLACEHOLDER: RDP gateway login page — no MFA prompt present]**

**Remediation Recommendation:**

1. Enable MFA for all VPN and remote access connections immediately. Recommended solutions include [e.g., Cisco Duo, Microsoft Authenticator with Azure AD Conditional Access, Okta].
2. Enable MFA for all RDP gateway access. If using Azure AD, configure Conditional Access policies to enforce MFA for all remote connections.
3. Enforce MFA for all privileged and administrative accounts within 30 days.
4. Conduct a password audit and force a password reset for accounts identified with compromised or weak passwords.
5. Implement account lockout policies to mitigate password spraying attacks (recommended: 5 failed attempts, 15-minute lockout).

**References:**

- CISA MFA Guidance: [https://www.cisa.gov/mfa](https://www.cisa.gov/mfa)
- CIS Safeguard 6.3: [https://www.cisecurity.org/controls/access-control-management](https://www.cisecurity.org/controls/access-control-management)
- Microsoft MFA Best Practices: [https://docs.microsoft.com/en-us/azure/active-directory/authentication/concept-mfa-howitworks](https://docs.microsoft.com/en-us/azure/active-directory/authentication/concept-mfa-howitworks)

**Status:** Open
**Date Identified:** [Date]
**Remediation Target Date:** [Date — e.g., within 30 days per SLA]

---

### FIND-003

**Finding ID:** FIND-003
**Title:** Default Credentials on Network Infrastructure Devices
**Severity:** Critical
**CVSS Score:** 9.1
**CVSS Vector String:** `CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H`
**CVE Reference(s):** N/A (Configuration Finding)
**CIS Control Mapping:** CIS Control 4 — Secure Configuration of Enterprise Assets and Software (Safeguard 4.1: Establish and Maintain a Secure Configuration Process; Safeguard 4.7: Manage Default Accounts on Enterprise Assets and Software)
**Affected Assets:**

- `switch-core-01` (IP: 10.0.0.1) — [e.g., Cisco Catalyst 3850]
- `fw-perimeter-01` (IP: 192.168.100.1) — [e.g., Fortinet FortiGate 100F]
- `ap-floor2-03` (IP: 10.0.1.45) — [e.g., Ubiquiti UniFi AP]

**Description:**
Three network infrastructure devices were found to be accessible using default vendor-supplied credentials that have not been changed from factory settings. Testing confirmed administrative access to `switch-core-01` using the credentials `admin` / `admin`, and to `fw-perimeter-01` using `admin` / `[vendor-default-password]`. Default credentials for these device models are publicly documented by vendors and included in widely available attack tooling. These devices have administrative interfaces accessible from the internal network and, in the case of the perimeter firewall, partially exposed via the management interface on the external interface.

**Business Impact:**
An attacker with access to the internal network — including any compromised workstation or unauthorized wireless connection — could immediately gain full administrative control of core network switches and the perimeter firewall using default credentials. This would allow an attacker to reroute network traffic, disable security controls, create persistent backdoor access, intercept unencrypted communications, or cause a complete network outage. Compromise of the perimeter firewall would give an attacker the ability to bypass all perimeter security controls.

**Evidence / Proof of Concept:**

> **[SCREENSHOT PLACEHOLDER: SSH session to switch-core-01 using default credentials — showing privileged EXEC mode prompt]**

> **[SCREENSHOT PLACEHOLDER: FortiGate web admin console login successful with default credentials — showing full admin dashboard access]**

```
# Example SSH session output (sanitized):
$ ssh admin@10.0.0.1
Password: [default password]

switch-core-01# show version
Cisco IOS Software...
switch-core-01# show privilege
Current privilege level is 15
```

**Remediation Recommendation:**

1. Immediately change all default credentials on affected devices to strong, unique passwords meeting the organization's password policy (minimum 16 characters, mixed case, numbers, and symbols).
2. Disable or rename default administrative accounts where the platform supports it.
3. Restrict management interface access to a dedicated out-of-band management network or jump host — management interfaces should not be accessible from general user segments or the internet.
4. Conduct a full audit of all network devices, appliances, and IoT devices for default credentials using a credentialed scanning profile.
5. Implement a network device configuration baseline aligned with CIS Benchmark standards for each device model.
6. Store all device credentials in a privileged access management (PAM) vault (e.g., CyberArk, Thycotic, HashiCorp Vault).

**References:**

- CIS Benchmark for [Cisco IOS / Fortinet / applicable platform]: [https://www.cisecurity.org/cis-benchmarks](https://www.cisecurity.org/cis-benchmarks)
- NIST SP 800-128 — Guide for Security-Focused Configuration Management: [https://csrc.nist.gov/publications/detail/sp/800-128/final](https://csrc.nist.gov/publications/detail/sp/800-128/final)
- CIS Safeguard 4.7: [https://www.cisecurity.org/controls/secure-configuration-of-enterprise-assets-and-software](https://www.cisecurity.org/controls/secure-configuration-of-enterprise-assets-and-software)

**Status:** Open
**Date Identified:** [Date]
**Remediation Target Date:** [Date — e.g., within 15 days per SLA]

---

*[Continue with FIND-004, FIND-005, etc. following the same template structure above.]*

---

## Appendix A: Full Asset List

| Hostname | IP Address | OS / Platform | Role | In Scope | Scanned | Notes |
|---|---|---|---|---|---|---|
| webserver01.client.com | 203.0.113.10 | Windows Server 2019 | Web server | Yes | Yes | Internet-facing |
| webserver02.client.com | 203.0.113.11 | Windows Server 2019 | Web server | Yes | Yes | Internet-facing |
| vpn.client.com | 203.0.113.20 | [VPN Platform] | Remote access | Yes | Yes | Internet-facing |
| rdgw.client.com | 203.0.113.21 | Windows Server 2022 | RDP gateway | Yes | Yes | Internet-facing |
| dc01.corp.client.com | 10.0.0.10 | Windows Server 2022 | Domain controller | Yes | Yes | Internal |
| dc02.corp.client.com | 10.0.0.11 | Windows Server 2022 | Domain controller | Yes | Yes | Internal |
| app-server-03 | 10.0.1.30 | [OS] | Application server | Yes | Yes | Internal |
| db-server-01 | 10.0.1.50 | [OS / DB Platform] | Database server | Yes | Yes | Internal |
| switch-core-01 | 10.0.0.1 | Cisco IOS [Version] | Core switch | Yes | Yes | Network infrastructure |
| fw-perimeter-01 | 192.168.100.1 | [Firewall OS/Version] | Perimeter firewall | Yes | Yes | Network infrastructure |
| [Hostname] | [IP] | [OS] | [Role] | [Yes/No] | [Yes/No] | [Notes] |

**Total assets inventoried:** [X]
**Total assets scanned:** [X]
**Scan coverage:** [X%]

---

## Appendix B: Tools and Versions Used

| Tool | Version | Vendor / Source | Purpose | License Type |
|---|---|---|---|---|
| Nessus Professional | [X.X.X] | Tenable | Authenticated vulnerability scanning | Commercial |
| Nmap | [X.XX] | nmap.org | Network discovery, port/service enumeration | Open source |
| Metasploit Framework | [X.X.X] | Rapid7 | Exploitation validation | Commercial / Open source |
| Burp Suite Professional | [X.X.X] | PortSwigger | Web application security testing | Commercial |
| BloodHound | [X.X.X] | BloodHound Enterprise / Community | Active Directory attack path analysis | Open source |
| SharpHound | [X.X.X] | BloodHound Community | AD data collection (used with BloodHound) | Open source |
| CIS-CAT Pro | [X.X.X] | Center for Internet Security | CIS Benchmark compliance assessment | Licensed |
| Mimikatz | [X.X.X] | gentilkiwi | Credential extraction validation (authorized) | Open source |
| Wireshark | [X.X.X] | Wireshark Foundation | Packet capture and analysis | Open source |
| [Tool Name] | [Version] | [Vendor] | [Purpose] | [License] |

---

## Appendix C: Scan Configurations

### C.1 Nessus Scan Profiles

| Scan Name | Target(s) | Policy / Template | Authentication | Scan Window |
|---|---|---|---|---|
| External perimeter scan | 203.0.113.0/24 | Advanced Scan — Unauthenticated | None | [Date/Time] |
| Internal authenticated scan — Windows | 10.0.0.0/16 | Advanced Scan — Credentialed | Domain admin service account | [Date/Time] |
| Internal authenticated scan — Linux | 10.0.1.0/24 | Advanced Scan — SSH Credentialed | SSH key, sudo | [Date/Time] |
| Web application scan | webserver01, webserver02 | Web Application Tests | Application test account | [Date/Time] |

### C.2 Nmap Command Reference

```bash
# Host discovery
nmap -sn [Target Range] -oN discovery_[date].txt

# Full TCP port scan with service version detection
nmap -sV -sC -p- -T4 [Target Range] -oN full_tcp_[date].txt

# UDP top ports
nmap -sU --top-ports 200 [Target Range] -oN udp_[date].txt

# OS fingerprinting (authorized)
nmap -O -sV [Target Range] -oN os_detect_[date].txt
```

### C.3 Scan Exclusions and Limitations

The following constraints applied during scanning:

- Scanning was performed during [off-hours window, e.g., 22:00–06:00 local time] to minimize production impact.
- Scan rate was throttled to [e.g., --max-rate 500] to avoid triggering IDS/IPS alerts and impacting network performance.
- [List any technical limitations encountered, e.g., "SNMP-based enumeration was not possible due to SNMPv3 enforcement without provided credentials."]
- [Note any systems that were unreachable or produced incomplete results.]

---

## Appendix D: Methodology Details

### D.1 CIS Controls Alignment

This assessment maps all findings to the CIS Controls v8 framework. The CIS Controls are a prioritized set of actions that collectively form a defense-in-depth set of cybersecurity best practices. Mapping findings to CIS Controls enables [Client Name] to align remediation efforts with a recognized framework and measure maturity improvement over time.

CIS Controls referenced in this report:

| CIS Control | Name |
|---|---|
| CIS 1 | Inventory and Control of Enterprise Assets |
| CIS 2 | Inventory and Control of Software Assets |
| CIS 3 | Data Protection |
| CIS 4 | Secure Configuration of Enterprise Assets and Software |
| CIS 5 | Account Management |
| CIS 6 | Access Control Management |
| CIS 7 | Continuous Vulnerability Management |
| CIS 8 | Audit Log Management |

### D.2 CVSS Scoring Methodology

All findings are scored using CVSS v3.1 base scores. Temporal and environmental scores are noted where applicable. CVSS base scores do not account for compensating controls or network segmentation; assessors have applied contextual judgment in the overall severity rating where warranted.

### D.3 Responsible Disclosure and Rules of Engagement

All testing activities were performed within the agreed rules of engagement documented in [RoE Document Reference / Appendix]. No destructive testing was performed without explicit written authorization. All exploitation activities were conducted against isolated test accounts or systems designated by [Client Name] for this purpose. All data obtained during the assessment has been handled in accordance with the confidentiality provisions of the engagement contract.

---

## Revision History

| Version | Date | Author | Description of Changes |
|---|---|---|---|
| 0.1 | [Date] | [Author Name] | Initial draft — findings documented |
| 0.2 | [Date] | [Author Name] | Internal peer review — revisions applied |
| 1.0 | [Date] | [Author Name] | Final report — delivered to client |
| [X.X] | [Date] | [Author Name] | [Description] |

---

*Report Version: [1.0] | Classification: CONFIDENTIAL | Prepared by: [Firm Name] | Contact: [Email]*
