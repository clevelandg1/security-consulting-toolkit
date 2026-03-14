# CIS Controls v8 Assessment Checklist

**Client Name:** [Client Name]
**Assessment Date:** [Assessment Date]
**Assessor:** [Assessor Name]
**Engagement ID:** [Engagement ID]
**Report Version:** 1.0

---

## How to Use This Checklist

This checklist is designed to be completed during or immediately following technical discovery and stakeholder interviews. It maps directly to the CIS Controls v8 framework and is structured around Implementation Groups (IG1, IG2, IG3) to help prioritize findings relative to the client's organizational maturity and resource capacity.

**Process:**
1. Complete the Overall Summary table first using prior knowledge or a high-level review, then validate each control section in detail.
2. For each sub-control, assign a status based on evidence gathered: interviews, tool outputs, documentation review, or direct observation.
3. Score each control on a 0–5 scale (see scoring guide below).
4. Use the Priority field to drive the remediation roadmap.

**Scoring Guide:**

| Score | Meaning |
|-------|---------|
| 0 | Not implemented; no evidence of awareness |
| 1 | Awareness exists but no formal process or tooling |
| 2 | Partially implemented; gaps are significant |
| 3 | Implemented in most areas; some gaps remain |
| 4 | Fully implemented; minor improvements possible |
| 5 | Fully implemented, measured, and continuously improved |

**Status Definitions:**

| Symbol | Meaning |
|--------|---------|
| Pass | Control is fully met with evidence |
| Partial | Control is partially met; gaps exist |
| Fail | Control is not met or no evidence found |
| N/A | Not applicable to this environment |

**Implementation Groups:**

| Group | Description | Typical Profile |
|-------|-------------|-----------------|
| IG1 | Basic — essential cyber hygiene | Small org, limited IT/security staff |
| IG2 | Foundational — builds on IG1 | Mid-size org, some dedicated security staff |
| IG3 | Organizational — advanced controls | Large org, dedicated security function |

---

## Overall Summary

| CIS Control | Control Name | IG | Status | Score (0–5) | Priority |
|-------------|-------------|-----|--------|-------------|----------|
| 1 | Inventory and Control of Enterprise Assets | IG1 | | | |
| 2 | Inventory and Control of Software Assets | IG1 | | | |
| 3 | Data Protection | IG1 | | | |
| 4 | Secure Configuration of Enterprise Assets and Software | IG1 | | | |
| 5 | Account Management | IG1 | | | |
| 6 | Access Control Management | IG1 | | | |
| 7 | Continuous Vulnerability Management | IG1 | | | |
| 8 | Audit Log Management | IG1 | | | |
| 9 | Email and Web Browser Protections | IG1 | | | |
| 10 | Malware Defenses | IG1 | | | |
| 11 | Data Recovery | IG1 | | | |
| 12 | Network Infrastructure Management | IG1 | | | |
| 13 | Network Monitoring and Defense | IG1 | | | |
| 14 | Security Awareness and Skills Training | IG1 | | | |
| 15 | Service Provider Management | IG2 | | | |
| 16 | Application Software Security | IG2 | | | |
| 17 | Incident Response Management | IG2 | | | |
| 18 | Penetration Testing | IG2 | | | |

**Overall Score:** _______ / 90
**Overall Maturity Rating:** [ ] Initial [ ] Developing [ ] Defined [ ] Managed [ ] Optimizing

---

## Control 1: Inventory and Control of Enterprise Assets

**Implementation Group:** IG1
**Why This Matters:** You cannot protect what you do not know exists. A complete, accurate, and continuously maintained asset inventory is the foundation of every other security control. Without it, coverage gaps are invisible and attack surface is unmanaged.

### Sub-Control Checklist

| # | Sub-Control Description | IG | Status | Evidence / Notes |
|---|------------------------|----|--------|-----------------|
| 1.1 | Establish and maintain a detailed enterprise asset inventory (hardware, including portable devices, network devices, IoT) | IG1 | | |
| 1.2 | Address unauthorized assets by either removing them from the network, denying them network access, or quarantining them | IG1 | | |
| 1.3 | Utilize an active discovery tool to identify assets connected to the enterprise network | IG2 | | |
| 1.4 | Use DHCP logging on all DHCP servers or IP address management tools to update the enterprise asset inventory | IG2 | | |
| 1.5 | Use a passive discovery tool to identify assets connected to the enterprise network and automatically update the asset inventory | IG3 | | |

**Control Score:** _______ / 5
**Recommended Priority:** [ ] Immediate [ ] Short-term [ ] Long-term
**Key Finding / Notes:**

_______________________________________________
_______________________________________________

---

## Control 2: Inventory and Control of Software Assets

**Implementation Group:** IG1
**Why This Matters:** Unauthorized or unmanaged software creates attack surface and introduces unknown risk. A software asset inventory enables license compliance, identifies unsupported software, and supports rapid response when a vulnerability in a specific application is disclosed.

### Sub-Control Checklist

| # | Sub-Control Description | IG | Status | Evidence / Notes |
|---|------------------------|----|--------|-----------------|
| 2.1 | Establish and maintain a software inventory of all licensed software installed on enterprise assets | IG1 | | |
| 2.2 | Ensure that only currently supported software is designated as authorized in the software inventory | IG1 | | |
| 2.3 | Address unauthorized software by either removing or denying it network access | IG1 | | |
| 2.4 | Utilize automated software inventory tools where supported to track installed software on enterprise assets | IG2 | | |
| 2.5 | Allow only authorized software libraries to load during runtime (allowlisting) | IG2 | | |
| 2.6 | Allow only authorized scripts to execute on enterprise assets | IG3 | | |

**Control Score:** _______ / 5
**Recommended Priority:** [ ] Immediate [ ] Short-term [ ] Long-term
**Key Finding / Notes:**

_______________________________________________
_______________________________________________

---

## Control 3: Data Protection

**Implementation Group:** IG1
**Why This Matters:** Data protection controls ensure that sensitive data is identified, classified, and handled appropriately throughout its lifecycle. Failure to protect sensitive data is frequently both a regulatory liability and the primary goal of threat actors targeting the organization.

### Sub-Control Checklist

| # | Sub-Control Description | IG | Status | Evidence / Notes |
|---|------------------------|----|--------|-----------------|
| 3.1 | Establish and maintain a data management process that addresses data sensitivity, ownership, retention, disposal, and handling | IG1 | | |
| 3.2 | Establish and maintain a data inventory that identifies sensitive data (PII, financial, health, IP) and the systems that store or process it | IG1 | | |
| 3.3 | Configure data access control lists based on a user's need to know | IG1 | | |
| 3.4 | Enforce data retention policies and dispose of data in accordance with defined schedules | IG1 | | |
| 3.5 | Encrypt data on end-user devices (laptops, mobile) that contain sensitive data at rest | IG1 | | |
| 3.6 | Encrypt sensitive data in transit using TLS 1.2+ or equivalent | IG2 | | |
| 3.7 | Use a Data Loss Prevention (DLP) tool to detect and block exfiltration of sensitive data | IG3 | | |

**Control Score:** _______ / 5
**Recommended Priority:** [ ] Immediate [ ] Short-term [ ] Long-term
**Key Finding / Notes:**

_______________________________________________
_______________________________________________

---

## Control 4: Secure Configuration of Enterprise Assets and Software

**Implementation Group:** IG1
**Why This Matters:** Default configurations of operating systems, applications, and network devices are rarely secure. Hardening assets to a known baseline eliminates a large class of vulnerabilities and reduces exploitability, especially for commodity attack techniques.

### Sub-Control Checklist

| # | Sub-Control Description | IG | Status | Evidence / Notes |
|---|------------------------|----|--------|-----------------|
| 4.1 | Establish and maintain a secure configuration process for enterprise assets and software | IG1 | | |
| 4.2 | Establish and maintain a secure configuration process for network infrastructure | IG1 | | |
| 4.3 | Configure automatic session lock on enterprise assets after a defined period of inactivity | IG1 | | |
| 4.4 | Implement and manage a firewall on end-user devices | IG1 | | |
| 4.5 | Implement and manage a firewall on servers; apply access control lists per approved network flows | IG2 | | |
| 4.6 | Securely manage enterprise assets and software using a configuration management system (e.g., GPO, Ansible, Chef) | IG2 | | |
| 4.7 | Manage default accounts — disable or rename built-in admin accounts, change default credentials | IG1 | | |

**Control Score:** _______ / 5
**Recommended Priority:** [ ] Immediate [ ] Short-term [ ] Long-term
**Key Finding / Notes:**

_______________________________________________
_______________________________________________

---

## Control 5: Account Management

**Implementation Group:** IG1
**Why This Matters:** Compromised credentials are the leading initial access vector in breaches. Proper account lifecycle management, including timely deprovisioning and privilege limitation, reduces the risk of unauthorized access through valid accounts.

### Sub-Control Checklist

| # | Sub-Control Description | IG | Status | Evidence / Notes |
|---|------------------------|----|--------|-----------------|
| 5.1 | Establish and maintain an inventory of all accounts (user, admin, service) managed in the enterprise | IG1 | | |
| 5.2 | Use unique passwords for all enterprise assets — enforce password policy via technical controls | IG1 | | |
| 5.3 | Disable dormant accounts after a period of inactivity (90 days or defined policy) | IG1 | | |
| 5.4 | Restrict administrator privileges to dedicated administrator accounts | IG1 | | |
| 5.5 | Establish and maintain an inventory of service accounts and review annually | IG2 | | |
| 5.6 | Centralize account management through a directory service (e.g., Active Directory, Azure AD) | IG2 | | |

**Control Score:** _______ / 5
**Recommended Priority:** [ ] Immediate [ ] Short-term [ ] Long-term
**Key Finding / Notes:**

_______________________________________________
_______________________________________________

---

## Control 6: Access Control Management

**Implementation Group:** IG1
**Why This Matters:** Least-privilege and need-to-know principles limit the blast radius of a breach. Role-based access control, multi-factor authentication, and privilege management ensure that even if credentials are compromised, lateral movement and data access remain restricted.

### Sub-Control Checklist

| # | Sub-Control Description | IG | Status | Evidence / Notes |
|---|------------------------|----|--------|-----------------|
| 6.1 | Establish an access granting process to document and approve access provisioning to enterprise assets and data | IG1 | | |
| 6.2 | Establish an access revoking process to ensure timely removal of access when no longer required | IG1 | | |
| 6.3 | Require MFA for all enterprise access — at minimum for remote access and privileged users | IG1 | | |
| 6.4 | Require MFA for externally-exposed applications | IG2 | | |
| 6.5 | Require MFA for all administrative access | IG2 | | |
| 6.6 | Establish and maintain an inventory of authentication and authorization systems | IG2 | | |
| 6.7 | Centralize access control using a PAM solution for privileged access | IG3 | | |

**Control Score:** _______ / 5
**Recommended Priority:** [ ] Immediate [ ] Short-term [ ] Long-term
**Key Finding / Notes:**

_______________________________________________
_______________________________________________

---

## Control 7: Continuous Vulnerability Management

**Implementation Group:** IG1
**Why This Matters:** Vulnerabilities are discovered daily. A continuous vulnerability management program ensures that weaknesses are identified, prioritized by risk, and remediated within defined SLAs before threat actors can exploit them.

### Sub-Control Checklist

| # | Sub-Control Description | IG | Status | Evidence / Notes |
|---|------------------------|----|--------|-----------------|
| 7.1 | Establish and maintain a vulnerability management process — includes scanning, prioritization, and remediation tracking | IG1 | | |
| 7.2 | Establish and maintain a remediation process to address vulnerabilities, including SLA definitions by severity | IG1 | | |
| 7.3 | Perform automated operating system patch management | IG1 | | |
| 7.4 | Perform automated application patch management | IG2 | | |
| 7.5 | Perform automated vulnerability scans of internal enterprise assets on a defined frequency (at minimum quarterly, ideally continuous) | IG2 | | |
| 7.6 | Perform automated vulnerability scans of externally-exposed enterprise assets | IG2 | | |
| 7.7 | Remediate detected vulnerabilities based on defined SLAs by severity level | IG2 | | |

**Control Score:** _______ / 5
**Recommended Priority:** [ ] Immediate [ ] Short-term [ ] Long-term
**Key Finding / Notes:**

_______________________________________________
_______________________________________________

---

## Control 8: Audit Log Management

**Implementation Group:** IG1
**Why This Matters:** Without audit logs, investigations are impossible and dwell time extends. Comprehensive log collection, centralization, and retention enables detection, incident response, forensic investigation, and compliance evidence.

### Sub-Control Checklist

| # | Sub-Control Description | IG | Status | Evidence / Notes |
|---|------------------------|----|--------|-----------------|
| 8.1 | Establish and maintain an audit log management process covering collection, storage, review, and retention | IG1 | | |
| 8.2 | Collect audit logs from enterprise assets | IG1 | | |
| 8.3 | Ensure adequate storage for audit logs — prevent loss due to storage exhaustion | IG1 | | |
| 8.4 | Standardize time synchronization across enterprise assets (NTP) | IG2 | | |
| 8.5 | Collect detailed audit logs for enterprise assets — authentication events, privilege use, configuration changes | IG2 | | |
| 8.6 | Collect DNS query audit logs to detect malicious outbound communication | IG2 | | |
| 8.7 | Centralize audit logs in a SIEM or log management system | IG2 | | |
| 8.8 | Retain audit logs for a minimum of 90 days on hot storage, 1 year total | IG3 | | |

**Control Score:** _______ / 5
**Recommended Priority:** [ ] Immediate [ ] Short-term [ ] Long-term
**Key Finding / Notes:**

_______________________________________________
_______________________________________________

---

## Control 9: Email and Web Browser Protections

**Implementation Group:** IG1
**Why This Matters:** Email and web browsing are the two most common initial access vectors for malware, phishing, and credential theft. Layered technical controls on these channels significantly reduce successful attacks even when end users are deceived.

### Sub-Control Checklist

| # | Sub-Control Description | IG | Status | Evidence / Notes |
|---|------------------------|----|--------|-----------------|
| 9.1 | Ensure only fully supported web browsers and email clients are allowed to execute in the enterprise | IG1 | | |
| 9.2 | Use DNS filtering services on all enterprise assets to block known malicious domains | IG1 | | |
| 9.3 | Maintain and enforce network-based URL filters to limit access to potentially harmful sites | IG2 | | |
| 9.4 | Restrict unnecessary or unauthorized browser and email client plugins, extensions, and add-on applications | IG2 | | |
| 9.5 | Implement DMARC, DKIM, and SPF records on all enterprise email domains | IG2 | | |
| 9.6 | Block unnecessary file types from entering the enterprise via email attachments | IG2 | | |

**Control Score:** _______ / 5
**Recommended Priority:** [ ] Immediate [ ] Short-term [ ] Long-term
**Key Finding / Notes:**

_______________________________________________
_______________________________________________

---

## Control 10: Malware Defenses

**Implementation Group:** IG1
**Why This Matters:** Malware remains the primary mechanism for ransomware deployment, data theft, and persistent access. Multi-layered malware defenses — including endpoint protection, behavioral detection, and anti-exploitation — are essential at every tier of the environment.

### Sub-Control Checklist

| # | Sub-Control Description | IG | Status | Evidence / Notes |
|---|------------------------|----|--------|-----------------|
| 10.1 | Deploy and maintain anti-malware software on all enterprise assets | IG1 | | |
| 10.2 | Configure automatic updates for anti-malware signature files on all enterprise assets | IG1 | | |
| 10.3 | Disable autorun and autoplay for removable media | IG1 | | |
| 10.4 | Configure anti-malware scanning of removable media | IG2 | | |
| 10.5 | Enable anti-exploitation features on enterprise assets (e.g., DEP, ASLR, Windows Defender Exploit Guard) | IG2 | | |
| 10.6 | Centrally manage anti-malware software and maintain visibility into malware events across the enterprise | IG2 | | |
| 10.7 | Use behavior-based anti-malware (EDR/XDR) with centralized alerting | IG3 | | |

**Control Score:** _______ / 5
**Recommended Priority:** [ ] Immediate [ ] Short-term [ ] Long-term
**Key Finding / Notes:**

_______________________________________________
_______________________________________________

---

## Control 11: Data Recovery

**Implementation Group:** IG1
**Why This Matters:** When preventive controls fail — and eventually they will — the ability to recover data quickly and completely determines the business impact of a ransomware attack or destructive incident. Tested, isolated backups are a critical last line of defense.

### Sub-Control Checklist

| # | Sub-Control Description | IG | Status | Evidence / Notes |
|---|------------------------|----|--------|-----------------|
| 11.1 | Establish and maintain a data recovery practice sufficient to restore in-scope enterprise assets to pre-incident state | IG1 | | |
| 11.2 | Perform automated backups of in-scope enterprise assets — at minimum weekly | IG1 | | |
| 11.3 | Protect recovery data with technical controls to prevent unauthorized access and modification | IG1 | | |
| 11.4 | Establish and maintain an isolated instance of recovery data (offsite or air-gapped; immutable backup) | IG2 | | |
| 11.5 | Test backup and recovery procedures at least quarterly and after significant changes | IG2 | | |

**Control Score:** _______ / 5
**Recommended Priority:** [ ] Immediate [ ] Short-term [ ] Long-term
**Key Finding / Notes:**

_______________________________________________
_______________________________________________

---

## Control 12: Network Infrastructure Management

**Implementation Group:** IG1
**Why This Matters:** Network infrastructure (routers, switches, firewalls, wireless) represents a high-value target for attackers seeking to intercept traffic or pivot laterally. Maintaining hardened, documented, and actively managed network infrastructure limits exposure significantly.

### Sub-Control Checklist

| # | Sub-Control Description | IG | Status | Evidence / Notes |
|---|------------------------|----|--------|-----------------|
| 12.1 | Ensure network infrastructure is kept up-to-date — firmware, OS, and security patches applied on schedule | IG1 | | |
| 12.2 | Establish and maintain a secure network architecture including segmentation, DMZ, and least-privilege network flows | IG1 | | |
| 12.3 | Securely manage network infrastructure using MFA, encrypted sessions (SSH/HTTPS), and out-of-band management where possible | IG2 | | |
| 12.4 | Establish and maintain architecture diagrams and inventories of all network infrastructure | IG2 | | |
| 12.5 | Centralize network authentication, authorization, and auditing (AAA) for network infrastructure | IG2 | | |
| 12.6 | Use of dedicated management VLAN or OOB management network for network infrastructure | IG3 | | |

**Control Score:** _______ / 5
**Recommended Priority:** [ ] Immediate [ ] Short-term [ ] Long-term
**Key Finding / Notes:**

_______________________________________________
_______________________________________________

---

## Control 13: Network Monitoring and Defense

**Implementation Group:** IG1
**Why This Matters:** Attackers operating inside a network leave detectable signals. Network monitoring — including traffic analysis, intrusion detection, and behavioral analytics — enables detection of lateral movement, data exfiltration, and command-and-control communication before significant damage occurs.

### Sub-Control Checklist

| # | Sub-Control Description | IG | Status | Evidence / Notes |
|---|------------------------|----|--------|-----------------|
| 13.1 | Centralize security event alerting across enterprise assets for log correlation and analysis | IG1 | | |
| 13.2 | Deploy a host-based intrusion detection solution on enterprise assets where supported | IG2 | | |
| 13.3 | Deploy a network intrusion detection solution (NIDS/IPS) to detect and alert on suspicious traffic | IG2 | | |
| 13.4 | Perform traffic filtering between network segments to limit unauthorized lateral movement | IG2 | | |
| 13.5 | Manage access control for assets remotely connecting to the enterprise — enforce VPN with MFA | IG2 | | |
| 13.6 | Collect network traffic flow logs (NetFlow, sFlow) and feed into log management / SIEM | IG3 | | |
| 13.7 | Deploy a network-based DLP solution to monitor and alert on exfiltration attempts | IG3 | | |

**Control Score:** _______ / 5
**Recommended Priority:** [ ] Immediate [ ] Short-term [ ] Long-term
**Key Finding / Notes:**

_______________________________________________
_______________________________________________

---

## Control 14: Security Awareness and Skills Training

**Implementation Group:** IG1
**Why This Matters:** Technical controls are bypassed every day through social engineering. A well-structured, role-appropriate security awareness program reduces successful phishing, credential theft, and insider risk by building security behaviors as organizational culture.

### Sub-Control Checklist

| # | Sub-Control Description | IG | Status | Evidence / Notes |
|---|------------------------|----|--------|-----------------|
| 14.1 | Establish and maintain a security awareness program — all employees complete training at hire and annually | IG1 | | |
| 14.2 | Train workforce members to recognize social engineering attacks (phishing, vishing, pretexting) | IG1 | | |
| 14.3 | Train workforce members on authentication best practices and use of password managers | IG1 | | |
| 14.4 | Train workforce members on causes of unintentional data exposure and how to prevent it | IG1 | | |
| 14.5 | Train workforce members on how to identify and report suspected security incidents | IG1 | | |
| 14.6 | Train high-risk workforce members (finance, executives, IT admins) on role-specific security threats | IG2 | | |
| 14.7 | Conduct phishing simulation exercises at least quarterly; track and trend click rates | IG2 | | |

**Control Score:** _______ / 5
**Recommended Priority:** [ ] Immediate [ ] Short-term [ ] Long-term
**Key Finding / Notes:**

_______________________________________________
_______________________________________________

---

## Control 15: Service Provider Management

**Implementation Group:** IG2
**Why This Matters:** Third-party vendors with access to your environment or data are an extension of your attack surface. The supply chain is a leading vector for breaches. A structured vendor risk management program ensures third parties meet your security standards.

### Sub-Control Checklist

| # | Sub-Control Description | IG | Status | Evidence / Notes |
|---|------------------------|----|--------|-----------------|
| 15.1 | Establish and maintain an inventory of service providers — all third parties with access to enterprise data or systems | IG2 | | |
| 15.2 | Establish and maintain a service provider management policy defining minimum security requirements | IG2 | | |
| 15.3 | Classify service providers by data sensitivity and criticality; apply appropriate oversight | IG2 | | |
| 15.4 | Ensure service provider contracts include security requirements (right-to-audit, incident notification, data handling) | IG2 | | |
| 15.5 | Assess service providers annually against your security requirements | IG3 | | |
| 15.6 | Monitor service providers for security events that may impact your environment | IG3 | | |

**Control Score:** _______ / 5
**Recommended Priority:** [ ] Immediate [ ] Short-term [ ] Long-term
**Key Finding / Notes:**

_______________________________________________
_______________________________________________

---

## Control 16: Application Software Security

**Implementation Group:** IG2
**Why This Matters:** Custom and third-party applications are common targets for exploitation. Integrating security into the software development lifecycle — including secure coding standards, dependency management, and application testing — prevents the introduction of exploitable vulnerabilities into production.

### Sub-Control Checklist

| # | Sub-Control Description | IG | Status | Evidence / Notes |
|---|------------------------|----|--------|-----------------|
| 16.1 | Establish and maintain a secure application development policy and process | IG2 | | |
| 16.2 | Establish and maintain a process to accept and address software vulnerabilities reported from external parties | IG2 | | |
| 16.3 | Perform root cause analysis on security vulnerabilities discovered in developed or acquired software | IG2 | | |
| 16.4 | Establish and maintain a process for receiving and vetting security advisories for third-party software | IG2 | | |
| 16.5 | Use software composition analysis (SCA) tools to identify vulnerable or outdated third-party libraries | IG3 | | |
| 16.6 | Perform application layer penetration testing on in-house developed or customized applications | IG3 | | |
| 16.7 | Use threat modeling to identify and address security risks in application design | IG3 | | |

**Control Score:** _______ / 5
**Recommended Priority:** [ ] Immediate [ ] Short-term [ ] Long-term
**Key Finding / Notes:**

_______________________________________________
_______________________________________________

---

## Control 17: Incident Response Management

**Implementation Group:** IG2
**Why This Matters:** Organizations that plan and practice incident response recover faster, experience lower costs, and minimize regulatory and reputational exposure. A documented, exercised IR plan is essential for coordinated, effective response when an incident occurs.

### Sub-Control Checklist

| # | Sub-Control Description | IG | Status | Evidence / Notes |
|---|------------------------|----|--------|-----------------|
| 17.1 | Designate personnel to manage incident handling — define IR team roles, responsibilities, and escalation paths | IG2 | | |
| 17.2 | Establish and maintain a contact list of parties to be notified in the event of a security incident | IG2 | | |
| 17.3 | Establish and maintain an enterprise incident response plan — document detection, containment, eradication, recovery, and post-incident steps | IG2 | | |
| 17.4 | Conduct incident response tabletop exercises at least annually | IG2 | | |
| 17.5 | Assign key roles in the incident response plan — legal, communications, executive, technical leads | IG2 | | |
| 17.6 | Define and document security event severity levels and corresponding response SLAs | IG3 | | |
| 17.7 | Conduct post-incident reviews and document lessons learned after every significant incident | IG3 | | |

**Control Score:** _______ / 5
**Recommended Priority:** [ ] Immediate [ ] Short-term [ ] Long-term
**Key Finding / Notes:**

_______________________________________________
_______________________________________________

---

## Control 18: Penetration Testing

**Implementation Group:** IG2
**Why This Matters:** Penetration testing validates the real-world effectiveness of your security controls by simulating adversary techniques. It identifies exploitable vulnerabilities that automated scanners miss and provides prioritized, evidence-based findings to drive remediation investment.

### Sub-Control Checklist

| # | Sub-Control Description | IG | Status | Evidence / Notes |
|---|------------------------|----|--------|-----------------|
| 18.1 | Establish and maintain a penetration testing program appropriate to the organization's size, complexity, and risk profile | IG2 | | |
| 18.2 | Perform periodic external penetration tests — at minimum annually | IG2 | | |
| 18.3 | Remediate penetration testing findings within defined SLAs; track remediation to closure | IG2 | | |
| 18.4 | Validate security measures using penetration test results — update controls accordingly | IG3 | | |
| 18.5 | Perform internal network penetration testing annually — test lateral movement and privilege escalation paths | IG3 | | |
| 18.6 | Include red team or adversary simulation exercises to test detection and response capability | IG3 | | |

**Control Score:** _______ / 5
**Recommended Priority:** [ ] Immediate [ ] Short-term [ ] Long-term
**Key Finding / Notes:**

_______________________________________________
_______________________________________________

---

## Assessment Summary & Recommendations

### Score Summary

| Priority Tier | Controls | Rationale |
|---------------|---------|-----------|
| Immediate (0–30 days) | | |
| Short-term (30–90 days) | | |
| Long-term (90–180 days) | | |

### Top Findings

1. _______________________________________________
2. _______________________________________________
3. _______________________________________________
4. _______________________________________________
5. _______________________________________________

### Assessor Sign-Off

**Assessor Name:** _______________________________________________
**Signature:** _______________________________________________
**Date Completed:** _______________________________________________

**Client Acknowledgment:** _______________________________________________
**Title:** _______________________________________________
**Date:** _______________________________________________

---

*This assessment was conducted under the Customer Advisory Framework (CAF) baseline assessment methodology. Results reflect point-in-time observations and should be validated during follow-up reviews.*
