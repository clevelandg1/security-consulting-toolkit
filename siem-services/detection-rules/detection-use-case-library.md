# Universal Detection Use Case Library
## Top 20 Must-Have Detection Rules

**Purpose:** This library defines the minimum viable detection coverage every client should have regardless of SIEM platform. Each rule is platform-agnostic and written in plain English so it can be implemented in Splunk SPL, Microsoft Sentinel KQL, QRadar AQL, Elastic DSL, or Rapid7 IDR.

**Alignment:** All rules map to MITRE ATT&CK and CIS Controls v8.

---

## How to Use This Library

Each rule entry contains:
- **Rule Name** — Short, descriptive identifier
- **Description** — What the rule detects and why it matters
- **Log Sources Required** — What must be onboarded before this rule fires
- **Detection Logic (Plain English)** — What the query looks for
- **MITRE ATT&CK Mapping** — Tactic and Technique IDs
- **CIS Control Alignment** — Which CIS Control this supports
- **Severity** — Critical / High / Medium / Low
- **Recommended Response Action** — First steps when this alert fires

---

## Rule 1: Brute Force Login Attempt

**Description:**
Detects repeated failed authentication attempts against a single account or from a single source IP within a short time window. Brute force is one of the most common initial access techniques and a strong early indicator of targeted credential attacks.

**Log Sources Required:**
- Active Directory / Windows Security Event Logs (Event ID 4625)
- VPN authentication logs
- Cloud IAM logs (AWS CloudTrail, Azure AD Sign-in logs, GCP Cloud Audit)

**Detection Logic (Plain English):**
Alert when the same username OR the same source IP generates 10 or more failed login events (Event ID 4625 or equivalent) within a 5-minute window. Exclude known service accounts and internal monitoring IPs from the baseline.

**MITRE ATT&CK Mapping:**
- Tactic: Initial Access, Credential Access
- Technique: T1110 — Brute Force
- Sub-techniques: T1110.001 (Password Guessing), T1110.003 (Password Spraying)

**CIS Control Alignment:** CIS Control 6 — Access Control Management

**Severity:** High

**Recommended Response Action:**
1. Identify source IP and geolocate
2. Determine if the targeted account is a privileged account
3. Check if any login succeeded following the failures
4. Lock the source IP at the firewall or WAF if external
5. Notify the account owner and reset credentials if compromise is suspected

---

## Rule 2: Password Spray Attack

**Description:**
Detects a single source IP attempting authentication against many different usernames with a low failure count per account — the hallmark of a password spray designed to avoid per-account lockout thresholds.

**Log Sources Required:**
- Active Directory / Windows Security Event Logs (Event ID 4625)
- Azure AD Sign-in Logs
- Okta / SSO platform logs

**Detection Logic (Plain English):**
Alert when a single source IP generates failed login attempts against 20 or more distinct usernames within a 10-minute window, with fewer than 3 failures per individual account. This differentiates spraying from targeted brute force.

**MITRE ATT&CK Mapping:**
- Tactic: Credential Access
- Technique: T1110.003 — Password Spraying

**CIS Control Alignment:** CIS Control 6 — Access Control Management

**Severity:** Critical

**Recommended Response Action:**
1. Immediately block the source IP at the perimeter
2. Run a full audit of all targeted accounts for successful logins
3. Force password reset for any account that successfully authenticated from that IP
4. Escalate to incident response if successful logins are identified
5. Review MFA enrollment status for all targeted accounts

---

## Rule 3: Impossible Travel / Geographic Anomaly

**Description:**
Detects a user account authenticating from two geographically distant locations within a timeframe that makes physical travel impossible. A strong indicator of credential theft or account sharing.

**Log Sources Required:**
- Active Directory with source IP logging
- VPN authentication logs
- Azure AD Sign-in Logs / Okta / other SSO platforms
- Cloud console login logs

**Detection Logic (Plain English):**
Alert when the same user account logs in successfully from two different source IPs that resolve to countries or regions more than 500 miles apart, and the time between logins is less than 2 hours. Apply a known VPN/proxy exclusion list to reduce false positives.

**MITRE ATT&CK Mapping:**
- Tactic: Initial Access
- Technique: T1078 — Valid Accounts

**CIS Control Alignment:** CIS Control 6 — Access Control Management; CIS Control 13 — Network Monitoring

**Severity:** High

**Recommended Response Action:**
1. Contact the user immediately via out-of-band channel (phone, not email)
2. Confirm which session is legitimate
3. Terminate the unauthorized session
4. Force MFA re-enrollment and password reset
5. Review all activity from both sessions for data access or exfiltration indicators

---

## Rule 4: Privileged Account Created Outside Change Window

**Description:**
Detects the creation of new privileged accounts (local admins, domain admins, service accounts with elevated rights) outside of approved change windows. Attackers frequently create backdoor accounts after gaining initial access.

**Log Sources Required:**
- Active Directory (Event ID 4720 — account created, Event ID 4728/4732/4756 — member added to privileged group)
- Windows Security Event Logs
- Cloud IAM logs

**Detection Logic (Plain English):**
Alert when Event ID 4720 (new account created) or Event IDs 4728/4732/4756 (user added to Domain Admins, Administrators, or other privileged groups) fires outside defined change windows (typically weekdays 8AM–6PM local time). Alert immediately if the creating account is not in the approved provisioning team.

**MITRE ATT&CK Mapping:**
- Tactic: Persistence, Privilege Escalation
- Technique: T1136 — Create Account; T1098 — Account Manipulation

**CIS Control Alignment:** CIS Control 5 — Account Management; CIS Control 6 — Access Control Management

**Severity:** Critical

**Recommended Response Action:**
1. Immediately disable the newly created account
2. Identify the account that performed the creation
3. Determine if the creating account itself has been compromised
4. Open a P1 incident ticket
5. Review all activity from the newly created account before disabling

---

## Rule 5: Lateral Movement via Pass-the-Hash / Pass-the-Ticket

**Description:**
Detects credential relay attacks where an attacker uses stolen NTLM hashes or Kerberos tickets to authenticate to remote systems without knowing the plaintext password. Common post-exploitation technique.

**Log Sources Required:**
- Windows Security Event Logs (Event ID 4624 — logon type 3 or 9, Event ID 4648)
- Active Directory
- EDR telemetry (process-level authentication events)

**Detection Logic (Plain English):**
Alert when a successful network logon (Event ID 4624, Logon Type 3) occurs using NTLM authentication from a workstation-class machine to another workstation-class machine (lateral workstation-to-workstation movement). Also alert on Event ID 4648 (explicit credential use) where the initiating process is lsass.exe or a known credential dumping tool. Supplement with EDR alerts for known PtH/PtT tool names (Mimikatz, Rubeus, Impacket).

**MITRE ATT&CK Mapping:**
- Tactic: Lateral Movement, Credential Access
- Technique: T1550.002 — Pass the Hash; T1550.003 — Pass the Ticket

**CIS Control Alignment:** CIS Control 5 — Account Management; CIS Control 13 — Network Monitoring

**Severity:** Critical

**Recommended Response Action:**
1. Isolate source and destination hosts immediately
2. Revoke all active sessions for accounts used in the logon events
3. Rotate KRBTGT account password twice (for Kerberos events)
4. Initiate full IR process — this indicates active hands-on-keyboard attacker
5. Collect memory dump from affected hosts for forensic analysis

---

## Rule 6: Suspicious PowerShell Execution

**Description:**
Detects PowerShell invocations with flags and patterns commonly used by attackers for download cradles, encoded commands, and AMSI bypass. Legitimate administrative PowerShell usage typically does not use these flags.

**Log Sources Required:**
- Windows Security Event Logs
- PowerShell Script Block Logging (Event ID 4104)
- PowerShell Module Logging (Event ID 4103)
- EDR process execution telemetry

**Detection Logic (Plain English):**
Alert when powershell.exe or pwsh.exe is executed with any combination of: `-EncodedCommand`, `-WindowStyle Hidden`, `-NonInteractive`, `-ExecutionPolicy Bypass`, `-NoProfile`, or when the command line contains `IEX`, `Invoke-Expression`, `DownloadString`, `WebClient`, `Base64`, or `FromBase64String`. Also alert on PowerShell spawned by Office applications (winword.exe, excel.exe, outlook.exe).

**MITRE ATT&CK Mapping:**
- Tactic: Execution, Defense Evasion
- Technique: T1059.001 — PowerShell; T1027 — Obfuscated Files or Information

**CIS Control Alignment:** CIS Control 10 — Malware Defenses; CIS Control 8 — Audit Log Management

**Severity:** High

**Recommended Response Action:**
1. Capture and decode the Base64 command if present
2. Identify the parent process that launched PowerShell
3. Check for network connections established during or after execution
4. Quarantine the endpoint via EDR if malicious payload confirmed
5. Review user's recent email for phishing indicators if Office application was parent

---

## Rule 7: Ransomware Indicator — Mass File Rename or Extension Change

**Description:**
Detects the rapid renaming or extension modification of large numbers of files, which is characteristic of ransomware encryption activity. Early detection at this stage can limit the blast radius significantly.

**Log Sources Required:**
- Endpoint file system audit logs (Windows Event ID 4663 — file access/modification)
- EDR file activity telemetry
- File server access logs (SMB audit logs if applicable)

**Detection Logic (Plain English):**
Alert when a single user or process modifies the file extension on more than 100 files within a 60-second window, OR when file rename events from a single process exceed 200 events per minute. Prioritize detection on file servers, shared drives, and backup locations. Common ransomware extensions to baseline against: `.locked`, `.encrypted`, `.enc`, `.crypted`, `.pay`, `.ransom`.

**MITRE ATT&CK Mapping:**
- Tactic: Impact
- Technique: T1486 — Data Encrypted for Impact

**CIS Control Alignment:** CIS Control 11 — Data Recovery; CIS Control 10 — Malware Defenses

**Severity:** Critical

**Recommended Response Action:**
1. Immediately isolate the affected endpoint from the network
2. Identify the process responsible and kill it
3. Do NOT attempt to decrypt files yet — preserve evidence
4. Activate the IR plan and identify patient zero
5. Check backup integrity before announcing recovery timeline
6. Engage legal/executive team immediately — ransomware is a reportable event in most jurisdictions

---

## Rule 8: Data Exfiltration via Large Outbound Transfer

**Description:**
Detects unusually large volumes of data being sent from internal hosts to external destinations, which may indicate data theft via exfiltration tools, cloud uploads, or command-and-control channels.

**Log Sources Required:**
- Firewall traffic logs with byte counts
- Proxy / web filtering logs
- NetFlow / network flow data
- Cloud storage audit logs (S3, Azure Blob, GCS)

**Detection Logic (Plain English):**
Alert when a single internal host transfers more than 500MB to a single external IP or domain within a 1-hour window outside of known backup or CDN IP ranges. Also alert when outbound traffic volume for a host exceeds 3x its 30-day baseline during off-hours (6PM–6AM or weekends). Tune thresholds per environment based on baseline profiling during onboarding.

**MITRE ATT&CK Mapping:**
- Tactic: Exfiltration
- Technique: T1048 — Exfiltration Over Alternative Protocol; T1041 — Exfiltration Over C2 Channel

**CIS Control Alignment:** CIS Control 13 — Network Monitoring and Defense

**Severity:** High

**Recommended Response Action:**
1. Identify destination IP/domain and check threat intelligence reputation
2. Capture packet samples if available (PCAP)
3. Identify the process responsible for the transfer
4. Check the user's activity logs for signs of insider threat vs. external compromise
5. Block destination at firewall while investigation proceeds

---

## Rule 9: New Persistence Mechanism — Registry Run Key or Scheduled Task

**Description:**
Detects creation of new autorun entries in commonly abused registry keys or new scheduled tasks, which attackers use to maintain persistence across reboots.

**Log Sources Required:**
- Windows Security Event Logs (Event ID 4698 — scheduled task created)
- Windows Registry audit logs (Sysmon Event ID 13 — registry value set)
- EDR telemetry
- Sysmon (if deployed)

**Detection Logic (Plain English):**
Alert on new entries written to `HKLM\Software\Microsoft\Windows\CurrentVersion\Run`, `HKCU\Software\Microsoft\Windows\CurrentVersion\Run`, or `HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon` by any process other than known software installers. Alert on Event ID 4698 (scheduled task created) where the task action contains encoded commands, scripts in temp directories, or invokes PowerShell/cmd with suspicious flags.

**MITRE ATT&CK Mapping:**
- Tactic: Persistence
- Technique: T1053.005 — Scheduled Task; T1547.001 — Registry Run Keys / Startup Folder

**CIS Control Alignment:** CIS Control 10 — Malware Defenses; CIS Control 4 — Secure Configuration

**Severity:** High

**Recommended Response Action:**
1. Identify the process that created the persistence entry
2. Examine the payload or script referenced by the entry
3. Check if the entry was created during or after a suspicious process execution
4. Remove the persistence mechanism and the payload
5. Run a full EDR scan on the affected host

---

## Rule 10: Suspicious DNS Query — Known Malicious Domain or DGA Pattern

**Description:**
Detects DNS queries to known malicious domains (C2 infrastructure, phishing, malware distribution) and algorithmically generated domain names (DGA) that indicate malware beaconing to randomized infrastructure.

**Log Sources Required:**
- Internal DNS server query logs
- Firewall DNS inspection logs
- Recursive DNS resolver logs
- Threat intelligence feed integration (domain reputation)

**Detection Logic (Plain English):**
Alert when any internal host queries a domain present on a threat intelligence blocklist (Abuse.ch, AlienVault OTX, Cisco Talos). Alert on NXDomain (non-existent domain) response rates exceeding 50 per minute from a single host — high NXDomain rates are a strong DGA indicator. Also alert on DNS queries containing more than 50 characters in the subdomain portion (potential DNS tunneling).

**MITRE ATT&CK Mapping:**
- Tactic: Command and Control
- Technique: T1071.004 — DNS; T1568.002 — Domain Generation Algorithms; T1048.003 — DNS Exfiltration

**CIS Control Alignment:** CIS Control 9 — Email and Web Browser Protections; CIS Control 13 — Network Monitoring

**Severity:** High

**Recommended Response Action:**
1. Isolate the querying host
2. Identify the process generating the DNS requests
3. Block the domain at the DNS resolver and firewall immediately
4. Check for any established connections to the resolved IP
5. Initiate EDR scan and review recent process execution history

---

## Rule 11: Admin Tool Executing from Non-Admin Context

**Description:**
Detects legitimate administrative tools being executed by standard user accounts or from non-standard locations, which is a strong indicator of living-off-the-land (LotL) attack techniques.

**Log Sources Required:**
- Windows Security Event Logs (Event ID 4688 — process creation, requires audit policy)
- Sysmon (Event ID 1 — process creation)
- EDR process execution telemetry

**Detection Logic (Plain English):**
Alert when any of the following processes execute from a user account that is NOT a member of Domain Admins or local Administrators group: `psexec.exe`, `wmic.exe`, `net.exe` with `user add` or `localgroup` arguments, `reg.exe` modifying HKLM keys, `vssadmin.exe` (particularly `delete shadows`), `wbadmin.exe`, `bcdedit.exe`. Also alert on these tools executing from temp directories (`%TEMP%`, `%APPDATA%`, `C:\Users\Public`).

**MITRE ATT&CK Mapping:**
- Tactic: Execution, Defense Evasion, Discovery
- Technique: T1569.002 — Service Execution; T1047 — Windows Management Instrumentation; T1490 — Inhibit System Recovery

**CIS Control Alignment:** CIS Control 4 — Secure Configuration; CIS Control 6 — Access Control Management

**Severity:** High

**Recommended Response Action:**
1. Terminate the suspicious process
2. Identify the user account and source of execution
3. Check if this is the result of phishing or malicious document execution
4. Audit the actions taken by the tool before termination
5. Quarantine endpoint and escalate to IR

---

## Rule 12: Unauthorized Cloud Storage Access or Public Bucket Exposure

**Description:**
Detects S3, Azure Blob, or GCS storage buckets being made publicly accessible, accessed from unusual geographic locations, or experiencing mass download events. Cloud storage misconfiguration is a leading cause of data breaches.

**Log Sources Required:**
- AWS CloudTrail (S3 API events: GetObject, PutBucketAcl, PutBucketPolicy)
- Azure Monitor / Storage Analytics logs
- GCP Cloud Audit Logs (Cloud Storage)

**Detection Logic (Plain English):**
Alert on `PutBucketAcl` or `PutBucketPolicy` API calls that set bucket permissions to `AllUsers` or `AuthenticatedUsers` (public access). Alert when a single IAM user or role downloads more than 1,000 objects or 1GB from a storage bucket within 1 hour. Alert on S3 GetObject requests from IP addresses not associated with known corporate IP ranges or approved third-party services.

**MITRE ATT&CK Mapping:**
- Tactic: Collection, Exfiltration
- Technique: T1530 — Data from Cloud Storage Object; T1537 — Transfer Data to Cloud Account

**CIS Control Alignment:** CIS Control 3 — Data Protection; CIS Control 13 — Network Monitoring

**Severity:** Critical

**Recommended Response Action:**
1. Immediately remove public access from the affected bucket
2. Identify what data was exposed or accessed
3. Determine if a data breach notification obligation exists (check state/federal laws)
4. Revoke the IAM credentials used if compromise is suspected
5. Enable S3 Block Public Access at the account level if not already enabled

---

## Rule 13: MFA Disabled or Bypassed for Privileged Account

**Description:**
Detects when MFA is disabled for a user account, especially privileged accounts, or when MFA is being bypassed using legacy authentication protocols. This is a critical control gap that attackers actively exploit.

**Log Sources Required:**
- Azure AD Audit Logs
- Okta System Logs
- AWS CloudTrail (IAM MFA events)
- Active Directory / ADFS logs

**Detection Logic (Plain English):**
Alert when the MFA method is removed, disabled, or updated for any account via admin API or user self-service portal. Specifically alert on Azure AD `Disable Strong Authentication` events or Okta `user.mfa.factor.deactivate` events. Also alert when a user successfully authenticates using a legacy protocol (Basic Auth, SMTP AUTH, IMAP) that bypasses MFA enforcement.

**MITRE ATT&CK Mapping:**
- Tactic: Defense Evasion, Persistence
- Technique: T1556 — Modify Authentication Process; T1078 — Valid Accounts

**CIS Control Alignment:** CIS Control 6 — Access Control Management

**Severity:** High

**Recommended Response Action:**
1. Verify with the account owner if the change was intentional
2. Re-enable MFA immediately if unauthorized
3. Review recent login history for the affected account
4. Identify the admin account that performed the change — verify it wasn't compromised
5. Audit all accounts for MFA compliance and report gaps to leadership

---

## Rule 14: Email Forwarding Rule Created to External Address

**Description:**
Detects inbox rules that automatically forward email to external addresses, a technique used by attackers for persistent email access after initial compromise and by malicious insiders for data exfiltration.

**Log Sources Required:**
- Microsoft 365 Unified Audit Logs (New-InboxRule, Set-InboxRule events)
- Google Workspace Admin Logs
- Exchange Server logs

**Detection Logic (Plain English):**
Alert on any `New-InboxRule` or `Set-InboxRule` audit event where the `ForwardTo` or `ForwardAsAttachmentTo` parameter contains an external email domain (not the organization's own domain). Also alert on rules with `DeleteMessage: True` combined with forwarding — this pattern hides the forwarding from the victim. Suppress for known mail migration or approved delegation scenarios.

**MITRE ATT&CK Mapping:**
- Tactic: Collection, Exfiltration
- Technique: T1114.003 — Email Forwarding Rule

**CIS Control Alignment:** CIS Control 9 — Email and Web Browser Protections; CIS Control 3 — Data Protection

**Severity:** High

**Recommended Response Action:**
1. Disable the forwarding rule immediately
2. Contact the account owner to confirm if rule was self-created or unauthorized
3. Review all email sent to the external forwarding address if accessible
4. Check for Business Email Compromise (BEC) indicators in sent items
5. Reset credentials and review all inbox rules for the affected account

---

## Rule 15: Excessive Failed VPN Logins from Single IP

**Description:**
Detects targeted brute force or credential stuffing attacks against the VPN gateway, which is a primary external attack surface for most organizations and frequently targeted for initial access.

**Log Sources Required:**
- VPN gateway authentication logs (Cisco ASA, Palo Alto GlobalProtect, Fortinet FortiGate, Pulse Secure)
- Firewall logs
- RADIUS/LDAP authentication logs

**Detection Logic (Plain English):**
Alert when a single source IP generates more than 20 failed VPN authentication events within a 10-minute window. Also alert when VPN logins occur during off-hours (10PM–5AM local time) from IP addresses that have not previously connected. Alert separately when a VPN login succeeds from an IP geolocation that is inconsistent with the user's normal country of access.

**MITRE ATT&CK Mapping:**
- Tactic: Initial Access
- Technique: T1133 — External Remote Services; T1110 — Brute Force

**CIS Control Alignment:** CIS Control 6 — Access Control Management; CIS Control 13 — Network Monitoring

**Severity:** High

**Recommended Response Action:**
1. Block the source IP at the firewall perimeter
2. Review whether any attempts succeeded
3. If successful login found, isolate the VPN session
4. Check the user account for concurrent active sessions
5. Enforce MFA on VPN if not already required

---

## Rule 16: Service Account Interactive Logon

**Description:**
Detects service accounts (non-human accounts used by applications and scheduled tasks) being used for interactive logins. Service accounts should never be used for interactive sessions — if they are, it indicates misuse, misconfiguration, or active attacker pivoting.

**Log Sources Required:**
- Active Directory / Windows Security Event Logs (Event ID 4624 — Logon Type 2 or 10)
- PAM/privileged access management platform logs

**Detection Logic (Plain English):**
Maintain a baseline list of known service accounts (accounts with names following service account naming conventions, or accounts explicitly tagged in AD). Alert when any account from this list generates a Logon Type 2 (interactive) or Logon Type 10 (remote interactive/RDP) event. These accounts should only produce Logon Type 5 (service) events under normal circumstances.

**MITRE ATT&CK Mapping:**
- Tactic: Privilege Escalation, Lateral Movement
- Technique: T1078.002 — Domain Accounts; T1021.001 — Remote Desktop Protocol

**CIS Control Alignment:** CIS Control 5 — Account Management; CIS Control 6 — Access Control Management

**Severity:** High

**Recommended Response Action:**
1. Immediately lock the service account
2. Identify where the interactive session originated
3. Determine if the account's credentials were extracted from a config file or secrets store
4. Rotate credentials for the service account
5. Review the application or service that uses the account for signs of compromise

---

## Rule 17: Endpoint Agent or AV Disabled

**Description:**
Detects when endpoint protection software (AV, EDR agents) is disabled, uninstalled, or becomes unresponsive. Attackers frequently disable endpoint security as one of their first actions after gaining access to a host.

**Log Sources Required:**
- EDR management platform (CrowdStrike, SentinelOne, Carbon Black) — agent health events
- Windows Security Event Logs (Event ID 7040 — service state changed; Event ID 7036)
- SCCM / endpoint management logs
- AV management console logs

**Detection Logic (Plain English):**
Alert when an EDR or AV service generates a stop, disable, or uninstall event on any endpoint. Alert when the EDR management console reports an agent as "disconnected" or "not reporting" for more than 4 hours during business hours. Also alert on Windows Security Event ID 4657 where the registry path contains known AV/EDR service names being modified.

**MITRE ATT&CK Mapping:**
- Tactic: Defense Evasion
- Technique: T1562.001 — Disable or Modify Tools; T1562.004 — Disable or Modify System Firewall

**CIS Control Alignment:** CIS Control 10 — Malware Defenses

**Severity:** High

**Recommended Response Action:**
1. Attempt to remotely re-enable the agent via management console
2. If re-enable fails, isolate the host network access
3. Identify the user account or process that disabled the agent
4. Review process execution history just before the agent went offline
5. Dispatch on-site or remote support for forensic review before re-imaging

---

## Rule 18: Cloud Console Login Without MFA from New Location

**Description:**
Detects logins to cloud management consoles (AWS Console, Azure Portal, GCP Console, M365 Admin Center) that do not have MFA recorded and originate from previously unseen IP addresses. Cloud console access is high-value and must be closely monitored.

**Log Sources Required:**
- AWS CloudTrail (ConsoleLogin events)
- Azure AD Sign-in Logs
- GCP Cloud Audit Logs
- M365 Unified Audit Logs

**Detection Logic (Plain English):**
Alert on any successful cloud console login where the MFA field is `False` or absent. Additionally, alert on console logins from IP addresses not seen in the last 30 days for that specific user. Prioritize alerts for IAM admin, billing, and security-role accounts. Correlate with impossible travel logic (Rule 3) for maximum fidelity.

**MITRE ATT&CK Mapping:**
- Tactic: Initial Access
- Technique: T1078.004 — Cloud Accounts; T1556 — Modify Authentication Process

**CIS Control Alignment:** CIS Control 6 — Access Control Management; CIS Control 16 — Application Software Security

**Severity:** Critical

**Recommended Response Action:**
1. Terminate the active cloud console session
2. Force MFA re-enrollment for the account
3. Review all API calls and resource changes made during the session
4. Rotate all access keys and secrets associated with the account
5. Determine root cause of MFA absence — conditional access policy gap or deliberate bypass

---

## Rule 19: Kerberoasting Attack Pattern

**Description:**
Detects Kerberoasting, a technique where attackers request Kerberos service tickets for service accounts in Active Directory and attempt to crack them offline to obtain plaintext credentials. Difficult to prevent but detectable via anomalous ticket request patterns.

**Log Sources Required:**
- Active Directory (Windows Security Event ID 4769 — Kerberos Service Ticket Requested)
- Domain Controller Security Event Logs

**Detection Logic (Plain English):**
Alert when a single user account generates more than 10 Kerberos Service Ticket Requests (Event ID 4769) within a 5-minute window where the ticket encryption type is `0x17` (RC4-HMAC — preferred by attackers because it's faster to crack offline). Normal user behavior generates 1–3 service ticket requests. Alert immediately if any account requests tickets for multiple SPNs in a short window, especially outside business hours.

**MITRE ATT&CK Mapping:**
- Tactic: Credential Access
- Technique: T1558.003 — Kerberoasting

**CIS Control Alignment:** CIS Control 5 — Account Management; CIS Control 6 — Access Control Management

**Severity:** High

**Recommended Response Action:**
1. Identify the requesting account — determine if it is a regular user account or compromised admin
2. Identify all SPNs requested — prioritize any that belong to high-privilege service accounts
3. Immediately rotate passwords for all service accounts whose SPNs were requested
4. Enforce AES encryption for service account Kerberos tickets where possible
5. Review the requesting host for additional compromise indicators

---

## Rule 20: Shadow IT Cloud Service Usage — Unapproved SaaS Upload

**Description:**
Detects large file uploads to consumer or unapproved cloud storage and file sharing services (Dropbox personal, WeTransfer, Google Drive personal, Box personal, Mega.nz), which can indicate data exfiltration disguised as shadow IT usage.

**Log Sources Required:**
- Web proxy / URL filtering logs
- Firewall application-layer inspection logs
- DNS query logs
- DLP platform logs (if deployed)

**Detection Logic (Plain English):**
Alert when any internal host initiates an HTTP POST or PUT request to known consumer cloud storage domains (dropbox.com, wetransfer.com, mega.nz, drive.google.com, sendspace.com, zippyshare.com) where the upload volume exceeds 50MB. Exclude corporate-approved tenants (e.g., company-owned Google Workspace or Box enterprise accounts) from alerting. Flag all uploads to Mega.nz regardless of size due to its reputation for abuse.

**MITRE ATT&CK Mapping:**
- Tactic: Exfiltration
- Technique: T1567.002 — Exfiltration to Cloud Storage; T1048 — Exfiltration Over Alternative Protocol

**CIS Control Alignment:** CIS Control 3 — Data Protection; CIS Control 9 — Email and Web Browser Protections

**Severity:** Medium

**Recommended Response Action:**
1. Identify the user account and workstation responsible
2. Determine if the upload is business-justified through manager confirmation
3. If unauthorized, attempt to identify what was uploaded (file names from proxy logs)
4. Consider whether DLP controls need to be expanded to block these categories
5. Document as policy violation and initiate HR/legal process if insider threat is suspected

---

## Detection Coverage Summary

| # | Rule Name | MITRE Tactic | Severity | Log Source Dependency |
|---|-----------|-------------|----------|-----------------------|
| 1 | Brute Force Login | Initial Access / Credential Access | High | AD, VPN, Cloud IAM |
| 2 | Password Spray | Credential Access | Critical | AD, Azure AD, SSO |
| 3 | Impossible Travel | Initial Access | High | AD, VPN, SSO |
| 4 | Privileged Account Created | Persistence / Privilege Escalation | Critical | AD, Cloud IAM |
| 5 | Pass-the-Hash / Pass-the-Ticket | Lateral Movement | Critical | Windows Events, EDR |
| 6 | Suspicious PowerShell | Execution / Defense Evasion | High | PowerShell Logs, EDR |
| 7 | Ransomware File Rename | Impact | Critical | Endpoint, EDR |
| 8 | Large Outbound Data Transfer | Exfiltration | High | Firewall, NetFlow |
| 9 | Registry / Scheduled Task Persistence | Persistence | High | Sysmon, EDR |
| 10 | Malicious DNS / DGA | Command & Control | High | DNS Logs |
| 11 | Admin Tool Non-Admin Context | Execution / Defense Evasion | High | Sysmon, EDR |
| 12 | Cloud Storage Public Exposure | Collection / Exfiltration | Critical | CloudTrail, Azure Monitor |
| 13 | MFA Disabled | Defense Evasion / Persistence | High | Azure AD, Okta, AWS IAM |
| 14 | Email Forwarding Rule | Collection / Exfiltration | High | M365 Audit, Google Workspace |
| 15 | VPN Brute Force | Initial Access | High | VPN Logs, Firewall |
| 16 | Service Account Interactive Login | Privilege Escalation / Lateral Movement | High | AD Windows Events |
| 17 | Endpoint Agent Disabled | Defense Evasion | High | EDR Console, Windows Events |
| 18 | Cloud Console No-MFA Login | Initial Access | Critical | CloudTrail, Azure AD |
| 19 | Kerberoasting | Credential Access | High | AD, DC Security Events |
| 20 | Shadow IT Cloud Upload | Exfiltration | Medium | Web Proxy, Firewall |

---

## Implementation Notes

### Tuning Priority
Deploy rules in this order for fastest time-to-value:
1. Rules 1, 2, 15 — Brute force and spray (immediate external attack visibility)
2. Rules 3, 18 — Impossible travel and cloud console (account takeover detection)
3. Rules 4, 13 — Privileged account changes and MFA (insider and post-compromise)
4. Rules 7, 8 — Ransomware and exfiltration (impact-stage detection)
5. Remaining rules as log sources are onboarded

### False Positive Management
- Establish 30-day baselines before enabling threshold-based alerts (Rules 8, 10, 19)
- Build exclusion lists for known vulnerability scanners, jump hosts, and monitoring tools
- Review alert fidelity weekly during first 60 days and adjust thresholds accordingly
- Document all suppressions with business justification and review quarterly

### Escalation Path
All Critical alerts → Immediate IR escalation, do not wait for analyst review
All High alerts → Analyst review within 1 hour during business hours, 2 hours after-hours
All Medium alerts → Analyst review within 4 business hours

---

*Detection Use Case Library v1.0 | Aligned to MITRE ATT&CK v14 and CIS Controls v8*
*Review and update rule logic quarterly or when new MITRE techniques are published*
