# Universal Log Source Checklist

**Version:** 1.0
**Last Updated:** 2026-03-13
**Purpose:** A comprehensive reference for security consultants and SIEM engineers to evaluate, onboard, and tune log sources across enterprise environments. Use this checklist during SIEM assessments, gap analyses, and new client onboarding engagements.

---

## How to Use This Document

Work through each log source category and verify:
1. Is this source present in the environment?
2. Is it currently sending logs to the SIEM?
3. Are the correct log types enabled?
4. Are the relevant security events being alerted on?

Mark each source as: **Active** / **Partially Active** / **Not Onboarded** / **Not Applicable**

---

## Table of Contents

1. [Firewall Logs](#1-firewall-logs)
2. [VPN Logs](#2-vpn-logs)
3. [Active Directory / LDAP](#3-active-directory--ldap)
4. [Endpoint (Windows / Linux / Mac)](#4-endpoint-windows--linux--mac)
5. [Email (Exchange / M365 / Google Workspace)](#5-email-exchange--m365--google-workspace)
6. [Antivirus / EDR](#6-antivirus--edr)
7. [Cloud Services — AWS](#7-cloud-services--aws)
8. [Cloud Services — Microsoft Azure](#8-cloud-services--microsoft-azure)
9. [Cloud Services — GCP](#9-cloud-services--gcp)
10. [Cloud Services — Microsoft 365](#10-cloud-services--microsoft-365)
11. [DNS Logs](#11-dns-logs)
12. [DHCP Logs](#12-dhcp-logs)
13. [Web Proxy / Secure Web Gateway](#13-web-proxy--secure-web-gateway)
14. [Network Flow / NetFlow / IPFIX](#14-network-flow--netflow--ipfix)
15. [Log Source Coverage Matrix](#log-source-coverage-matrix)
16. [Quick Reference: Security Events by MITRE ATT&CK Tactic](#quick-reference-security-events-by-mitre-attck-tactic)

---

## 1. Firewall Logs

### What It Is

A firewall is the primary network perimeter enforcement point that permits or denies traffic based on defined rules. Firewall logs capture every connection attempt, session establishment, and rule evaluation, making them one of the highest-value log sources for detecting both inbound attacks and outbound exfiltration or command-and-control activity. They provide the foundational network visibility that nearly every other detection use case depends on.

### Log Types Generated

- **Traffic/Session logs** — every permitted or denied connection: source IP, destination IP, source port, destination port, protocol, bytes transferred, duration, action (allow/deny/drop), interface
- **Rule hit count logs** — which firewall rules are being triggered and how frequently
- **NAT translation logs** — mapping of internal private IPs to external public IPs (critical for attribution)
- **IPS/IDS inline alert logs** — threat signature matches, protocol anomalies, exploit attempts detected by the integrated intrusion prevention engine
- **Application identification logs** — (next-gen firewalls) application identified on the session (e.g., BitTorrent on port 443)
- **User identity logs** — (NGFW with user-ID) mapping of session to authenticated domain user
- **SSL/TLS inspection logs** — decrypted session metadata for HTTPS traffic inspection
- **Zone-based policy logs** — traffic crossing defined security zones (DMZ, internal, external, guest)
- **High availability and system events** — failover events, configuration changes, administrator logins
- **URL filtering logs** — (for firewalls with integrated URL filtering) categorized web request decisions

### Security Events to Look For

- **Port scans and network reconnaissance** — a single source IP attempting connections to many destination ports or many destination hosts in a short window; look for high deny counts from a single source
- **Geographic anomalies** — inbound connections from unexpected countries, especially to sensitive services (RDP, SSH, management interfaces); use GeoIP enrichment on source IPs
- **Beaconing patterns** — regular periodic allow sessions to the same external IP or domain at consistent intervals, often with small and consistent byte counts (classic C2 behavior)
- **Large outbound data transfers** — sessions with unusually high byte counts from internal hosts to external destinations, particularly over non-standard ports or to cloud storage providers
- **Repeated denies from the same source** — brute-force or scanning behavior; high deny count from a single IP in a short time window
- **Inbound access to management interfaces** — SSH, HTTPS management, Telnet, or SNMP on WAN-facing interfaces; should never appear in normal traffic
- **Rule violations and policy bypasses** — traffic matching an explicit deny rule that was previously allowed, indicating possible rule misconfiguration or policy change
- **Unusual outbound protocols** — IRC, Telnet, NetBIOS, or RPC outbound to the internet; these should not exist in a normal environment
- **New external IP communications from critical servers** — database servers, domain controllers, or file servers initiating outbound connections to external internet IPs
- **Traffic on unusual high-numbered ports** — common for malware using non-standard ports to evade detection (e.g., C2 on port 8443, 4444, 1337)
- **ICMP anomalies** — unusually large ICMP packets or high volumes of ICMP traffic (potential tunneling or covert channel)
- **Firewall rule change events** — any modification to firewall rules or policies, especially those that open new allow rules to/from the internet

### SIEM Onboarding Steps

**Option A: Syslog (Most Common)**

1. **Enable logging on the firewall.** In the firewall management interface, ensure traffic logging, session logging, and threat/IPS logging are all enabled. Verify that both allow and deny traffic is being logged (many default configs only log denies).
2. **Configure a syslog profile.** Set the destination syslog server to your SIEM syslog listener IP and port (typically UDP 514 or TCP 514/6514 for TLS). Set the log format — prefer **CEF (Common Event Format)** or **LEEF** if supported, as most SIEMs have pre-built parsers for these formats. For raw syslog, you will need a custom parser.
3. **Confirm syslog is reaching the SIEM.** On the SIEM, run a packet capture or check the incoming log queue to verify raw events are arriving before building parsers or alerts.
4. **Apply the correct vendor parser.** Most major SIEMs include out-of-the-box parsers for the major firewall vendors. Select the appropriate one:
   - **Palo Alto Networks (PAN-OS):** Use the official Palo Alto Networks add-on/app. PAN-OS sends logs in comma-separated format with a fixed field order per log type (TRAFFIC, THREAT, CONFIG, SYSTEM, HIPMATCH). Ensure the correct log type discriminator field is used.
   - **Fortinet FortiGate:** FortiGate syslog uses key=value format. Use the Fortinet add-on or configure a CEF output profile in FortiGate. Enable traffic, event, and UTM logs.
   - **Cisco ASA / FTD:** ASA sends syslog with message codes (e.g., %ASA-6-302013 for TCP session built). Use the Cisco ASA add-on. For FTD, configure the eStreamer API or syslog output from Firepower Management Center (FMC).
   - **pfSense / OPNsense:** Configure syslog under System > Advanced > Logging. Use the pfSense/filterlog parser. pfSense outputs filterlog entries for firewall, plus standard syslog for other services.
5. **Normalize critical fields.** Ensure the following fields are parsed and mapped to your SIEM's Common Information Model (CIM) or data model: src_ip, dst_ip, src_port, dst_port, protocol, action, bytes_in, bytes_out, duration, rule_name, interface, zone.
6. **Enable NAT log correlation.** Configure NAT translation logging (if separate from session logs) so that external IPs can be mapped back to internal hosts. This is critical for investigations.
7. **Set up index/storage policy.** Firewall logs are typically very high volume. Set an appropriate retention policy (minimum 90 days online, 1 year cold storage for compliance). Consider summary indexing or aggregation for raw volume management.
8. **Build baseline dashboards and initial alerts.** Start with top denied sources, top allowed destinations, traffic by zone, and geographic distribution before adding high-fidelity detection rules.
9. **Enable threat/IPS log forwarding separately.** IPS/IDS alerts from the firewall are typically a different log stream. Ensure these are also forwarded and parsed, as they are separate from traffic logs.
10. **Test with known traffic patterns.** Generate test traffic (e.g., ping a blocked IP, attempt to SSH to the management interface) and confirm the corresponding events appear in the SIEM within acceptable latency.

---

## 2. VPN Logs

### What It Is

VPN (Virtual Private Network) logs record the authentication, session establishment, and activity of remote access connections into the corporate network. Because VPN is the primary remote access vector for most organizations, it is also the primary target for credential-based attacks. VPN logs are essential for detecting unauthorized remote access, account compromise, and anomalous geographic or temporal patterns in remote user behavior.

### Log Types Generated

- **Authentication success events** — user authenticated, method used (password, MFA, certificate), timestamp, source IP
- **Authentication failure events** — user failed to authenticate, failure reason (bad password, expired account, invalid MFA), source IP, timestamp
- **Session start events** — session established, assigned internal IP, tunnel type, user, client hostname, client version
- **Session end events** — session disconnected, reason (user disconnect, timeout, admin kick), total duration, total bytes in/out
- **Client IP and assigned IP records** — external IP used to connect and the internal IP assigned via DHCP pool or static assignment
- **Bytes transferred per session** — data volume moved inbound and outbound during each session
- **Multi-factor authentication events** — MFA success/failure, method used (push, OTP, hardware token), device ID
- **Split-tunnel vs. full-tunnel session records** — which traffic was routed through the VPN vs. directly to the internet
- **Certificate validation events** — for certificate-based VPN, certificate presented, validation result, certificate serial number
- **Admin and management events** — VPN configuration changes, policy changes, gateway restart events

### Security Events to Look For

- **Failed authentication spikes** — a sudden increase in failed logins for a specific user account or from a specific source IP; classic brute-force or credential stuffing indicator
- **Brute-force from a single source IP** — many failed authentication attempts across multiple accounts from the same source IP within a short timeframe; indicates credential stuffing or password spray
- **Concurrent active sessions for the same user** — the same user account authenticated and active on the VPN from two different source IPs simultaneously; possible account sharing or account compromise
- **Impossible travel** — a user authenticates from City A, disconnects, and then authenticates from City B within a timeframe that would be physically impossible given travel time between the two locations; strong indicator of credential compromise
- **Off-hours VPN access** — user connects at 2 AM when they normally work 9 AM to 5 PM in a specific time zone; particularly suspicious for privileged accounts
- **First-time access from a new country or region** — user has historically always connected from a specific country, and suddenly connects from a different country with no advance notice or travel record
- **Successful login following multiple failures** — successful authentication immediately following a high number of failed attempts on the same account; indicates a successful brute-force
- **Expired or locked account authentication attempts** — indicates either an unmanaged credential being attacked or automated scripts using old credentials
- **New device or new client version connecting for a specific user** — device fingerprint or user-agent for the VPN client has never been seen before for this user
- **Abnormally large data transfer during a session** — a user transfers significantly more data than their typical session baseline (potential staging/exfiltration after compromise)
- **Short-duration sessions with high byte counts** — automated tooling often authenticates, downloads a specific dataset, and disconnects quickly; differs from normal interactive use patterns
- **Access to VPN from known malicious IPs** — source IP matches a threat intelligence feed, Tor exit node list, or known proxy/VPN service

### SIEM Onboarding Steps

**Option A: Syslog (Standard)**

1. **Enable comprehensive authentication and session logging.** In the VPN gateway management interface, ensure both authentication events (success and failure) and session events (start, end, data transfer) are enabled. Do not limit logging to failures only — successful sessions are required for impossible travel and behavioral analytics.
2. **Configure syslog export to SIEM.** Set the syslog destination to your SIEM listener. Use TCP syslog with TLS where supported to prevent log tampering. Configure the appropriate log format for your SIEM parser.
3. **Configure RADIUS/LDAP authentication logging (if applicable).** If the VPN authenticates against a RADIUS server or directly to Active Directory/LDAP, ensure those authentication systems are also forwarding logs to the SIEM. Cross-correlate VPN authentication with directory authentication logs.
4. **Apply the vendor-specific parser:**
   - **Cisco AnyConnect / ASA:** AnyConnect authentication events appear as ASA syslog messages (e.g., %ASA-6-722051, %ASA-4-722041). Use the Cisco ASA add-on. Ensure AnyConnect session events are enabled in the ASA logging config.
   - **Palo Alto GlobalProtect:** GlobalProtect logs are part of PAN-OS system and authentication logs. Enable GlobalProtect logging in PAN-OS, configure syslog profile, and use the Palo Alto add-on.
   - **Fortinet SSL-VPN:** FortiGate SSL-VPN events appear in the event log (vpn subtype). Ensure FortiGate event logging is enabled and forwarded via syslog.
   - **Pulse Secure / Ivanti:** Enable syslog under System > Log/Monitoring > Events > Syslog. User access events include authentication, session, and data transfer fields.
   - **OpenVPN / WireGuard:** These produce flat log files. Use a log shipping agent (Filebeat, Fluentd, or NXLog) to tail the log file and forward to the SIEM.
5. **Normalize key fields.** Map: user, src_ip (external client IP), assigned_ip (internal tunnel IP), session_start, session_end, duration, bytes_in, bytes_out, authentication_result, failure_reason, mfa_result, client_hostname.
6. **Integrate GeoIP enrichment.** Ensure the src_ip field is enriched with GeoIP data (country, city, latitude/longitude, ASN) at ingest time. This is required for impossible travel detection.
7. **Build a user baseline.** Where the SIEM supports behavioral analytics (UEBA), configure a baseline for each user: typical login times, typical source countries, typical session duration and data volume. Deviations from these baselines should trigger alerts.
8. **Correlate with Active Directory account status.** Build correlation rules that fire when a VPN authentication attempt is made for an account that is disabled or locked in Active Directory.
9. **Set up impossible travel detection logic.** Write a rule that tracks login events per user, calculates the minimum travel time between two consecutive logins based on geographic distance (roughly: distance in km / 900 for air travel), and alerts when the elapsed time is less than the minimum travel time.
10. **Test with known-bad scenarios.** Simulate a failed login, a successful login, and a long-duration session. Confirm all three event types appear in the SIEM with all required fields populated correctly.

---

## 3. Active Directory / LDAP

### What It Is

Active Directory (AD) is the centralized identity and access management system in most Windows enterprise environments, handling authentication, authorization, and directory services for all domain-joined assets. Because virtually every user action in a Windows environment generates an AD event, and because compromising Active Directory means compromising the entire organization, AD logs are arguably the single most important log source in a Windows-centric enterprise. LDAP (Lightweight Directory Access Protocol) is the underlying protocol used by many non-Windows systems to authenticate against a directory.

### Log Types Generated

**Authentication Events:**
- **Event ID 4624** — successful logon (includes logon type: interactive, network, service, batch, unlock)
- **Event ID 4625** — failed logon (includes failure reason: bad password, account locked, account disabled, clock skew)
- **Event ID 4634** — logoff event (account logged off)
- **Event ID 4647** — user-initiated logoff
- **Event ID 4648** — logon with explicit credentials (RunAs, pass-the-hash indicator)
- **Event ID 4768** — Kerberos TGT request (authentication service request, AS-REQ)
- **Event ID 4769** — Kerberos service ticket request (TGS-REQ; high volume may indicate Kerberoasting)
- **Event ID 4771** — Kerberos pre-authentication failed (bad password for Kerberos)
- **Event ID 4776** — NTLM authentication attempt

**Account Management Events:**
- **Event ID 4720** — user account created
- **Event ID 4722** — user account enabled
- **Event ID 4723** — user changed their own password
- **Event ID 4724** — administrator reset a user's password
- **Event ID 4725** — user account disabled
- **Event ID 4726** — user account deleted
- **Event ID 4740** — user account locked out
- **Event ID 4767** — user account unlocked

**Group Membership Events:**
- **Event ID 4728** — member added to a security-enabled global group
- **Event ID 4729** — member removed from a security-enabled global group
- **Event ID 4732** — member added to a security-enabled local group
- **Event ID 4733** — member removed from a security-enabled local group
- **Event ID 4756** — member added to a security-enabled universal group
- **Event ID 4757** — member removed from a security-enabled universal group

**Privilege and Policy Events:**
- **Event ID 4672** — special privileges assigned to new logon (admin-level rights used)
- **Event ID 4673** — privileged service called
- **Event ID 4674** — operation attempted on privileged object
- **Event ID 4739** — domain policy changed

**Directory Service Events:**
- **Event ID 4662** — operation performed on directory object (access to AD objects; used for DCSync detection)
- **Event ID 5136** — directory service object was modified
- **Event ID 4742** — computer account changed (potential domain join/leave)

### Security Events to Look For

- **Authentication failure spikes** — sudden increase in Event ID 4625 events for a specific account or from a specific source machine; brute-force or password spray indicator; for password spray, look for many 4625s across many accounts from the same source in a short window with few attempts per account
- **Pass-the-Hash indicators** — Event ID 4624 with Logon Type 3 (network) and Authentication Package = NTLM and no corresponding interactive logon from that source; especially suspicious for privileged accounts
- **Kerberoasting** — large number of Event ID 4769 requests (service ticket requests) in a short time from a single account, particularly requesting tickets for service accounts with SPNs; attackers request Kerberos tickets to crack offline
- **AS-REP Roasting** — Event ID 4768 with result code 0x17 (pre-authentication not required) indicates accounts vulnerable to AS-REP Roasting
- **DCSync attack** — Event ID 4662 with access rights including "DS-Replication-Get-Changes" and "DS-Replication-Get-Changes-All" from a non-domain-controller source; indicates an attacker using mimikatz DCSync to extract password hashes
- **Account created outside change window** — Event ID 4720 occurring outside of normal business hours or outside an approved change management window; especially concerning for accounts with admin-level names
- **User added to privileged groups** — Event ID 4728, 4732, or 4756 where the target group is Domain Admins, Enterprise Admins, Schema Admins, or other high-value groups; any such change should be reviewed
- **Admin account creation followed by immediate privileged action** — Event ID 4720 followed quickly by Event ID 4728 (added to admin group) followed by Event ID 4624 (logon) in rapid succession; indicates automated attacker tooling
- **Password resets by non-IT accounts** — Event ID 4724 (admin password reset) from a Subject Account that is not a known IT administrator; could indicate a compromised IT account or unauthorized password reset
- **Stale or dormant account activity** — logon event from an account that has been inactive for 90+ days; these accounts often represent forgotten service accounts or former employees whose credentials were compromised
- **Lateral movement via network logons** — Event ID 4624 with Logon Type 3 (network logon) spreading across multiple systems in sequence; especially with admin shares (C$, ADMIN$) as the target
- **Multiple 4740 lockouts for the same account** — repeated lockouts suggest an automated attack or a password spray in progress
- **Golden/Silver Ticket indicators** — Kerberos tickets with abnormally long lifetimes (> 10 hours), tickets for non-existent accounts, or tickets being presented from sources that never performed a 4768 TGT request

### SIEM Onboarding Steps

1. **Enable the correct audit policies on all domain controllers.** The default Windows audit policy does not log all required events. Use Group Policy to enable: Account Logon (success + failure), Account Management (success + failure), Directory Service Access (success + failure), Logon/Logoff (success + failure), Privilege Use (success + failure). Apply to the Domain Controllers OU.
2. **Configure Windows Event Forwarding (WEF) — Option A (agentless).** WEF uses the native Windows Remote Management (WinRM) service to forward events from DCs to a Windows Event Collector (WEC) server. Configure a subscription on the WEC server specifying the event channels (Security, System, Application) and the event IDs to forward. This requires no installed agent but requires WinRM enabled on all DCs.
3. **Deploy a log shipping agent — Option B (agent-based).** Install Winlogbeat or NXLog on each domain controller. Configure the agent to read the Windows Security event log and forward to the SIEM (Elasticsearch, Splunk, or a syslog receiver). Agent-based collection is more reliable and supports filtering at the source.
4. **Ensure ALL domain controllers are covered.** In environments with multiple DCs, authentication events may land on any DC. If you only collect from one DC, you will miss events. Enumerate all DCs in the environment and confirm each one is in scope for log collection.
5. **Configure the Security event log with sufficient buffer size.** The default Security event log size (20 MB) will be overwritten quickly on a busy DC. Increase the maximum log size to at least 1 GB on each DC to prevent event loss before forwarding.
6. **Enable PowerShell Script Block Logging via GPO.** Apply Group Policy to enable: Computer Configuration > Administrative Templates > Windows Components > Windows PowerShell > Turn on Script Block Logging. This generates Event ID 4104 and is critical for detecting malicious PowerShell.
7. **Enable command line process creation auditing via GPO.** Apply Group Policy: Computer Configuration > Administrative Templates > System > Audit Process Creation > Include command line in process creation events. This enriches Event ID 4688 with the full command line of the created process.
8. **Install and configure Sysmon on domain controllers.** Microsoft Sysinternals Sysmon provides far richer endpoint telemetry than native Windows event logging. Use a community-maintained Sysmon configuration (e.g., SwiftOnSecurity or olafhartong/sysmon-modular) to capture process creation, network connections, registry changes, and file creation events on DCs.
9. **Normalize and map fields in the SIEM.** Ensure the following fields are parsed and accessible: EventID, SubjectUserName, TargetUserName, LogonType, IpAddress, WorkstationName, AuthPackage, FailureReason, MemberName, GroupName, ComputerName, timestamp.
10. **Build privileged group membership monitoring.** Create a real-time alert that fires any time EventID 4728, 4732, or 4756 is logged and the group is in a predefined list of sensitive groups (Domain Admins, Enterprise Admins, Backup Operators, Account Operators, Schema Admins).
11. **Integrate with an asset inventory or CMDB.** Correlate AD computer objects with your asset inventory so that logon events from unknown or unregistered computer accounts can be flagged.
12. **Test with known event triggers.** Create a test account, fail a login, lock it out, reset the password, add it to a group, delete it. Confirm all corresponding Event IDs appear in the SIEM within acceptable latency before going live with detection rules.

---

## 4. Endpoint (Windows / Linux / Mac)

### What It Is

Endpoint logs capture activity occurring directly on workstations and servers — process execution, file system changes, registry modifications, network connections, and user activity. Because attackers spend the majority of their time operating on endpoints after an initial foothold, endpoint telemetry is the most rich and actionable source of data for detecting post-exploitation activity. Without endpoint visibility, most modern attack techniques (living-off-the-land, fileless malware, lateral movement) are invisible to network-based detection.

### Log Types Generated

**Windows (Native):**
- **Event ID 4688** — process creation (process name, parent process, command line if auditing enabled, user context)
- **Event ID 4689** — process termination
- **Event ID 7045** — new service installed
- **Event ID 4698** — scheduled task created
- **Event ID 4702** — scheduled task modified
- **Event ID 4699** — scheduled task deleted
- **Event ID 4104** — PowerShell script block executed
- **Event ID 4103** — PowerShell module logging
- **Event ID 1102** — audit log cleared (Security log wiped)
- **Event ID 104** — System log cleared

**Sysmon Events (Recommended):**
- **Sysmon Event ID 1** — process creation with full command line, hashes, parent process, and PPID
- **Sysmon Event ID 2** — file creation time changed (timestomping indicator)
- **Sysmon Event ID 3** — network connection (process making outbound connection, destination IP/port)
- **Sysmon Event ID 7** — image loaded (DLL loaded into process — detect DLL injection)
- **Sysmon Event ID 8** — CreateRemoteThread (process injection technique)
- **Sysmon Event ID 10** — process access (process opening another process's memory — lsass.exe access)
- **Sysmon Event ID 11** — file created (new file creation with path and hash)
- **Sysmon Event ID 12/13/14** — registry object added/deleted/renamed, registry value set
- **Sysmon Event ID 15** — file create stream hash (alternate data stream creation)
- **Sysmon Event ID 22** — DNS query (process making DNS lookup)
- **Sysmon Event ID 25** — process tampering (hollowing, herpaderping)

**Linux (auditd):**
- **Syscall events** — execve (process execution), open/read/write/close (file access), connect (network), socket, bind
- **File integrity events** — file modification, creation, deletion in watched directories (/etc, /bin, /sbin, /usr/bin, home directories)
- **User authentication events** — PAM events, sudo usage, su events, SSH login/logout
- **Privileged command execution** — sudo, su, cron job execution, setuid/setgid execution

**macOS:**
- **Unified Log (OSLog)** — system-wide structured log capturing application, kernel, and security events
- **OpenBSM audit log** — file system access, process execution, network connections, authentication (BSM token format)
- **Endpoint Security Framework (ESF) events** — used by EDR agents; process exec, file operations, network events
- **LaunchAgent/LaunchDaemon plist changes** — persistence mechanism monitoring
- **TCC (Transparency Consent and Control) events** — access to camera, microphone, full disk access, screen recording

### Security Events to Look For

- **Living-off-the-land (LOLBin) abuse** — legitimate Windows binaries used maliciously: certutil.exe (download files), mshta.exe (execute HTA), regsvr32.exe (AppLocker bypass), wscript.exe/cscript.exe (script execution), msiexec.exe (payload delivery), bitsadmin.exe (download), rundll32.exe (DLL execution), expand.exe (file extraction)
- **Malicious PowerShell patterns** — encoded commands (base64 decoded strings), obfuscation (character substitution, string concatenation), bypass flags (-ExecutionPolicy Bypass, -EncodedCommand, -WindowStyle Hidden, -NonInteractive), download cradles (IEX + WebClient/Invoke-WebRequest), AMSI bypass attempts
- **Credential dumping from LSASS** — Sysmon Event ID 10 showing a process (other than lsass.exe, services.exe) opening lsass.exe with access rights including 0x1010, 0x1038, 0x001FFFFF; process names like procdump.exe, taskmgr.exe, rundll32.exe, mimikatz.exe
- **Lateral movement via PsExec** — creation of PSEXESVC service (Event ID 7045), executable dropped in ADMIN$ share, execution of cmd.exe or powershell.exe as a child of services.exe from a remote source
- **WMI lateral movement** — wmic.exe or WmiPrvSE.exe spawning unusual child processes, WMI subscriptions created (Win32_EventFilter, Win32_EventConsumer, CommandLineEventConsumer)
- **DCOM lateral movement** — mmc.exe, msbuild.exe, or other COM hosts spawning cmd.exe or powershell.exe with network connections preceding the execution
- **Unusual parent-child process relationships** — word.exe or excel.exe spawning cmd.exe, powershell.exe, or wscript.exe; explorer.exe spawning net.exe or nltest.exe; svchost.exe spawning powershell.exe
- **Defense evasion — process injection** — Sysmon Event ID 8 (CreateRemoteThread) or Event ID 10 (process access) targeting common host processes (explorer.exe, svchost.exe, notepad.exe); rundll32.exe or regsvr32.exe running without expected command-line arguments
- **Defense evasion — DLL hijacking** — Sysmon Event ID 7 showing a DLL loaded from an unusual path (AppData, Temp, user-writable directory) by a trusted process, when the legitimate DLL lives in System32
- **Persistence — scheduled tasks** — Event ID 4698 (task created) or Sysmon process creation showing schtasks.exe with /create argument, especially if the task runs from Temp, AppData, or a web cache directory
- **Persistence — registry run keys** — Sysmon Event ID 13 (registry value set) targeting HKCU or HKLM Run keys (SOFTWARE\Microsoft\Windows\CurrentVersion\Run and RunOnce)
- **Persistence — startup folder** — Sysmon Event ID 11 (file created) in the Windows Startup folder paths (%APPDATA%\Microsoft\Windows\Start Menu\Programs\Startup)
- **Audit log cleared** — Event ID 1102 (Security log cleared) or Event ID 104 (System log cleared); a strong indicator of an attacker covering tracks
- **Linux privilege escalation** — sudo to root for unusual commands, new SUID binary created, cron job added by non-root user, /etc/passwd or /etc/shadow modified

### SIEM Onboarding Steps

**Windows Endpoints:**

1. **Deploy Sysmon.** Sysmon is the most impactful single action for improving Windows endpoint visibility. Download from Microsoft Sysinternals. Deploy using a GPO, SCCM, Ansible, or your EDR's software deployment feature. Use a hardened community config (olafhartong/sysmon-modular or SwiftOnSecurity/sysmon-config). Configure the Sysmon service to auto-start and set hash algorithms to MD5, SHA256, IMPHASH for threat intel matching.
2. **Enable critical audit policies via GPO.** At minimum enable: Audit Process Creation (success), Audit Logon (success + failure), Audit Privilege Use (failure), Audit Object Access (failure), Audit Policy Change (success + failure), Audit Account Management (success + failure).
3. **Enable PowerShell Script Block Logging via GPO.** Computer Configuration > Administrative Templates > Windows Components > Windows PowerShell > Turn on Script Block Logging (Enabled) and Turn on Module Logging (Enabled).
4. **Enable command line process auditing via GPO.** Computer Configuration > Administrative Templates > System > Audit Process Creation > Include command line in process creation events.
5. **Deploy Winlogbeat or NXLog as the log shipping agent.** Configure the agent to collect from Windows Event Log channels: Security, System, Application, Microsoft-Windows-Sysmon/Operational, Microsoft-Windows-PowerShell/Operational, Microsoft-Windows-TaskScheduler/Operational. Forward to the SIEM via the configured output (Elasticsearch, Splunk HEC, syslog).
6. **Configure agent watchdog / service monitoring.** Ensure the log shipping agent itself is monitored. If the agent service stops, the SIEM should alert. This prevents blind spots from agent failures.

**Linux Endpoints:**

7. **Install and configure auditd.** Install the audit daemon (auditd) and the audit rules package. Configure /etc/audit/audit.rules or /etc/audit/rules.d/ with rules covering: all execve syscalls, writes to /etc and /bin, privilege escalation (sudo, su), SSH events, and cron modifications. Use a community ruleset (bfuzzy1/auditd-attack or Neo23x0/auditd) as a starting point.
8. **Configure auditd output for SIEM forwarding.** Use audisp-remote or audisp-syslog plugin to forward auditd events to the SIEM syslog receiver, or deploy Filebeat with the auditd module to ship /var/log/audit/audit.log directly.
9. **Ship /var/log/auth.log and /var/log/secure.** These files contain PAM authentication events, sudo usage, and SSH logins. Use Filebeat, Fluentd, or Logstash to tail and forward these files.

**macOS Endpoints:**

10. **Deploy an EDR agent with macOS support.** Native macOS logging for SIEM integration is complex. The most practical approach is to deploy an EDR agent (CrowdStrike Falcon, SentinelOne, Microsoft Defender for Endpoint) that uses the Apple Endpoint Security Framework (ESF) and forwards telemetry to the SIEM via the vendor's API or syslog integration.
11. **Enable macOS Unified Logging export.** For environments without a commercial EDR, use a log shipping agent that reads the unified log stream (log stream command) or exports unified log archives for shipping.
12. **Monitor LaunchAgent and LaunchDaemon directories.** Configure file integrity monitoring on /Library/LaunchAgents, /Library/LaunchDaemons, ~/Library/LaunchAgents as these are the primary persistence locations on macOS.

---

## 5. Email (Exchange / M365 / Google Workspace)

### What It Is

Email logs capture the full lifecycle of email messages — delivery, filtering, and user interactions — across the organization's mail infrastructure. Email remains the primary initial access vector for attackers (phishing, malicious attachments, credential harvesting links), and email systems are also a target for post-compromise actions like setting up forwarding rules for persistent access and conducting Business Email Compromise (BEC) fraud. Email log integration provides detection for both the initial phishing attempt and the post-compromise mailbox manipulation that often follows.

### Log Types Generated

- **Message delivery logs** — sender, recipient, subject, timestamp, message size, delivery status, source IP, message ID
- **Spam and phishing filtering decisions** — message disposition (delivered, quarantined, blocked, junk), spam confidence level (SCL), phish confidence level (PCL), filter rule matched
- **Attachment scanning results** — attachment filename, hash, scan result (clean, malicious, suspicious), sandboxing verdict
- **URL click events** — (M365 Safe Links, Proofpoint URL Defense) user clicked a URL, URL rewritten status, click timestamp, destination URL, click result (blocked/allowed)
- **Inbox rule creation and changes** — rule name, conditions (from, subject keywords), actions (forward to, delete, move to folder), user who created the rule, timestamp
- **Mailbox delegation and permission changes** — user granted Full Access or Send As permission on another mailbox, distribution group changes
- **External auto-forwarding rules** — rules that forward email to external addresses; often created by attackers for persistent mail access
- **Mass email delete events** — large volume of messages deleted from inbox or all folders in a short timeframe
- **OAuth application grant events** — user granted a third-party OAuth application access to their mailbox; permissions granted, app name, app ID
- **Mail flow statistics and anomalies** — unusual volume of outbound email, new sending domains, high bounce rates (potential spam campaign)
- **Administrative actions** — eDiscovery searches, mailbox export, audit log access, message trace operations

### Security Events to Look For

- **Phishing emails delivered to internal users** — messages where sender display name does not match sender email domain, lookalike domains (micros0ft.com vs. microsoft.com), messages with Subject keywords matching known phishing patterns ("invoice", "urgent action required", "verify your account"), messages from free email providers claiming to be internal executives
- **Malicious attachment delivery** — attachments with double extensions (document.pdf.exe), macro-enabled Office documents (.xlsm, .docm, .xlsb), password-protected ZIP files (common malware delivery), ISO or IMG files containing executables (common AV bypass)
- **Auto-forwarding rule to external address** — an inbox rule or transport rule configured to forward all or specific email to an external (non-corporate) email address; this is a high-confidence BEC indicator and should be treated as a critical alert
- **Mass email deletion** — a user or a process deletes hundreds or thousands of email messages in a short timeframe; may indicate an attacker covering tracks or a compromised account attempting to hide phishing replies
- **Unusual login to mail account from new location** — a mailbox access event (via OWA, IMAP, ActiveSync) from a country or IP that the user has never accessed from before; correlate with VPN/authentication logs
- **BEC indicators** — reply-to header different from sender, email thread injection (attacker replies to an existing thread with a forged From address), change of payment instructions in email threads involving finance department
- **OAuth application with excessive permissions** — a third-party app was granted Mail.ReadWrite, Mail.Send, or MailboxSettings.ReadWrite permissions via OAuth consent; these permissions allow full mailbox access without the user's password
- **Large attachment exfiltration** — user sending emails with large attachments to personal email accounts (Gmail, Hotmail) or external cloud storage domains
- **Executive impersonation** — inbound email where the Display Name matches a C-level executive but the actual email domain is external; common Business Email Compromise precursor
- **Legacy protocol authentication to mail** — IMAP or POP3 authentication from a location where the user does not use those protocols; legacy protocols bypass MFA and are frequently exploited
- **Spike in outbound email volume** — a user's account suddenly sending 10x-100x their normal outbound email volume; indicates compromised account sending spam or phishing campaigns

### SIEM Onboarding Steps

**Microsoft Exchange Online / M365:**

1. **Enable the Unified Audit Log (UAL).** In the M365 Security & Compliance Center (now Microsoft Purview), go to Audit > Start recording user and admin activity. Without this enabled, no audit events are generated. Note: UAL must be enabled before events accumulate — it is not retroactive.
2. **Set the UAL retention period.** Default retention for most licenses is 90 days. For E5 licenses, this can be extended to 1 year. Verify the retention meets your compliance requirements. For longer retention, export to a storage account or the SIEM.
3. **Connect via Microsoft Graph API or O365 Management Activity API.** Most SIEMs connect to M365 audit logs via the Office 365 Management Activity API. Configure the API connector with an Azure AD app registration with the following permissions: ActivityFeed.Read and ActivityFeed.ReadDlp (application permissions). Authenticate with client credentials (client ID + secret or certificate).
4. **Use Microsoft Sentinel's M365 Defender connector (if using Sentinel).** The Microsoft Sentinel data connectors blade includes native connectors for Microsoft 365 Defender, Microsoft Defender for Office 365, and Exchange Online. These are the simplest integration path if Sentinel is the SIEM.
5. **Enable Defender for Office 365 (if licensed).** Defender for Office 365 Plan 1 adds Safe Attachments and Safe Links. Plan 2 adds Attack Simulator and Threat Explorer. Both generate additional detection events that enrich SIEM alerts. Enable extended email event streaming to the SIEM.
6. **Configure message trace log export.** Exchange Online Message Trace provides delivery logs for all messages. Use the Exchange Online PowerShell cmdlet Get-MessageTrace for historical lookups and the Reporting API for ongoing streaming.
7. **Apply the correct UAL event workloads in your parser.** The UAL includes events from many different M365 services under different RecordType values. Key record types for email security: ExchangeItemGroup (mailbox events), ExchangeAdmin (admin actions), ComplianceDLPExchange (DLP), PowerBIAudit is irrelevant — focus on RecordType 2 (ExchangeItem), 1 (ExchangeAdmin), 28 (ThreatIntelligence).

**Google Workspace:**

8. **Enable Google Workspace Admin Audit Logging.** In the Google Admin Console, go to Reports > Audit to review available audit events. Ensure audit logging is enabled for Gmail, Admin, Login, and Drive.
9. **Connect via Google Workspace Admin SDK Reports API.** Use a Google Cloud service account with domain-wide delegation and the scope https://www.googleapis.com/auth/admin.reports.audit.readonly. Configure the SIEM's Google Workspace connector with the service account credentials.
10. **Configure alert policies for high-priority email events.** In Google Workspace Alert Center, enable alerts for: Government-backed attacks, Suspicious login activity, Phishing in Gmail. Forward Alert Center notifications via the Alert Center API to the SIEM.

**Email Security Gateways (Proofpoint, Mimecast, Barracuda):**

11. **Configure API or syslog export from the email gateway.** Proofpoint Email Protection and Mimecast both offer REST API access to threat log data and syslog export. Configure the SIEM connector or syslog receiver for the gateway's output format. These gateways provide additional context on threats blocked before they reached Exchange/Gmail.

---

## 6. Antivirus / EDR

### What It Is

Antivirus (AV) and Endpoint Detection and Response (EDR) tools monitor endpoints for malicious software, suspicious behavior, and policy violations. While traditional AV relies on signature-based detection, modern EDR platforms use behavioral analytics, machine learning, and threat intelligence to detect threats that bypass signatures. EDR tools are also used for active threat hunting and incident response due to their rich telemetry and real-time visibility. AV/EDR logs in the SIEM serve as a high-confidence signal for confirmed malware activity, but must be correlated with endpoint telemetry logs to provide full context.

### Log Types Generated

- **Malware detection events** — file name, file path, file hash (MD5/SHA256), threat name/family, detection method (signature, behavioral, ML, cloud reputation), action taken (quarantined, blocked, allowed, alert-only)
- **Quarantine events** — file quarantined, quarantine success/failure, original path, quarantine timestamp
- **Scan events** — scheduled scan start/complete, on-demand scan triggered, scan result summary, items scanned, items detected
- **Agent health and connectivity events** — agent checked in, agent version, last policy update, agent service status (running/stopped)
- **Policy violation events** — USB device blocked, application blocked by application control, script blocked
- **Exploit prevention events** — exploit technique blocked (stack pivot, ROP chain, heap spray, reflective DLL injection, process injection attempt), process name, technique name
- **Behavioral detection events** — suspicious behavior chain flagged by the ML engine (e.g., Office document spawning PowerShell, browser spawning cmd.exe), alert with parent and child process context
- **Incident/alert records** — high-level incident grouping related alerts and detections into a single investigation record (CrowdStrike Incidents, SentinelOne Threats)
- **Threat hunting results** — queries run, results returned, hunting rule matches (for EDR platforms with built-in hunting)
- **Network connection blocks** — outbound connections blocked by the EDR's network control module (e.g., known malware C2 domain blocked)
- **Tamper protection events** — attempt to disable, uninstall, or modify the EDR agent detected

### Security Events to Look For

- **Malware detection on critical servers** — any detection on a domain controller, critical database server, or financial system should be treated as a critical incident regardless of the reported threat name; malware on a DC is almost always a serious breach
- **Recurring detections on the same endpoint** — the same threat (or variant) detected multiple times on the same host after remediation; indicates incomplete remediation, a persistent mechanism re-dropping the payload, or a reinfection vector still active
- **EDR agent offline or tampered** — an EDR agent that stops checking in, is disabled, or is uninstalled is a high-priority alert; attackers frequently attempt to disable security tooling as a defense evasion step
- **Detection of dual-use tools** — detection or execution of tools commonly used by attackers but not by normal users: Mimikatz (credential theft), Cobalt Strike (post-exploitation framework), PsExec (lateral movement), BloodHound/SharpHound (AD reconnaissance), Impacket tools (wmiexec, secretsdump, psexec), Responder (NTLM capture), PowerView (AD enumeration)
- **Behavioral anomalies from ML engine** — even if the severity is "medium" or "low", ML-based behavioral detections from EDR should be reviewed; these often represent novel or fileless techniques that signature-based detection missed
- **Detections in temp or AppData paths** — malware landing in %TEMP%, %APPDATA%, %LOCALAPPDATA%, or C:\Users\Public\ is a strong indicator of a phishing or drive-by-download delivery; these are writable locations commonly abused by malware to avoid requiring admin rights
- **Process injection detections** — EDR blocking a process injection attempt (CreateRemoteThread, WriteProcessMemory + CreateRemoteThread, process hollowing) is a high-confidence indicator of in-memory malware execution
- **Exploit prevention triggered** — an exploit prevention event on a browser, Office application, or PDF reader indicates an active exploitation attempt; investigate the URL or document that triggered the exploit
- **Mass file rename detection** — EDR behavioral engines often detect ransomware early via rapid file rename or encryption patterns; even a "suspicious" verdict on this behavior pattern should trigger an immediate investigation
- **Agent version outdated across multiple endpoints** — a large number of agents that are significantly out of date may indicate a gap in patch management or a managed agent that is failing to update, leaving those endpoints less protected

### SIEM Onboarding Steps

**CrowdStrike Falcon:**

1. **Configure the CrowdStrike Event Stream API.** CrowdStrike offers a Streaming API (FalconStream) that pushes events in real time. Create an API client in the Falcon console with Event Streams scope (read). Configure your SIEM's CrowdStrike connector or use the Falcon SIEM connector tool provided by CrowdStrike to receive events.
2. **Alternatively, use the Falcon Data Replicator (FDR).** FDR replicates all raw sensor events to an AWS S3 bucket in near real time. Configure your SIEM to poll the S3 bucket and ingest the raw events. This provides the richest telemetry but at higher volume.
3. **Use the CrowdStrike Alerts API for high-priority alert streaming.** In addition to raw events, configure a separate feed for Falcon Alerts (Detections and Incidents) which are already triaged and prioritized by CrowdStrike's AI. Map CrowdStrike severity levels to your SIEM's severity taxonomy.

**Microsoft Defender for Endpoint:**

4. **Configure MDE Streaming API.** In the Microsoft 365 Defender portal, go to Settings > Microsoft 365 Defender > Streaming API. Configure raw event streaming to Azure Event Hub or Azure Blob Storage. From there, use your SIEM's Event Hub connector to ingest.
5. **Use Microsoft Sentinel's MDE connector (if using Sentinel).** The native Microsoft Defender for Endpoint connector in Sentinel ingests all MDE alerts and incidents directly with no additional configuration beyond enabling the connector.

**SentinelOne:**

6. **Configure SentinelOne Syslog output.** In the SentinelOne Management Console, go to Settings > Integrations > Syslog. Add a syslog server pointing to your SIEM receiver. Configure the event types to forward: Threats, Alerts, Activities, and Agent Status. Choose CEF format for widest SIEM compatibility.
7. **Alternatively, use the SentinelOne API for richer data.** The SentinelOne REST API provides access to threats, alerts, activities, and agent telemetry. Use the SIEM's SentinelOne app or build a custom API poller.

**General AV (Symantec, McAfee/Trellix, Trend Micro):**

8. **Configure syslog output from the management server.** Most enterprise AV platforms have a central management server (Symantec Endpoint Security Manager, McAfee ePO, Trend Micro Apex Central). Configure syslog forwarding from the management server rather than individual agents. This reduces collection points.
9. **Normalize severity levels.** Different AV vendors use different severity scales. Create a normalization mapping in the SIEM to translate vendor-specific severity names (e.g., CrowdStrike "critical" vs. SentinelOne "S1_ALERT_SEVERITY_CRITICAL" vs. Defender "High") to a consistent internal severity scale.
10. **Correlate AV/EDR detections with endpoint telemetry.** Configure the SIEM to automatically correlate an AV detection event with the corresponding endpoint's recent process creation, network connection, and file creation events from Sysmon or the EDR telemetry. This enriches the detection context and speeds up triage.

---

## 7. Cloud Services — AWS

### What It Is

Amazon Web Services generates extensive audit and operational logs across its service catalog. AWS CloudTrail is the primary audit mechanism, capturing every API call made to AWS services by users, roles, and services. Combined with VPC Flow Logs for network visibility and GuardDuty for managed threat detection, AWS logs provide comprehensive visibility into cloud infrastructure activity. Given that AWS environments contain data stores, compute resources, and often privileged access paths into on-premises networks, AWS log sources are critical for detecting both cloud-specific attacks and the cloud leg of hybrid infrastructure attacks.

### Log Types Generated

- **AWS CloudTrail — Management Events** — every control plane API call: IAM changes, EC2 operations, S3 bucket operations, VPC changes, security group modifications, KMS key operations, Lambda deployments; who called what API, from where, and with what result
- **AWS CloudTrail — Data Events** — object-level API calls: S3 GetObject, PutObject, DeleteObject; Lambda function invocations; DynamoDB GetItem/PutItem; must be explicitly enabled (not enabled by default due to volume)
- **VPC Flow Logs** — network traffic metadata for all ENIs in a VPC: src IP, dst IP, src port, dst port, protocol, bytes, packets, action (ACCEPT/REJECT); does not include packet payload
- **Amazon GuardDuty findings** — managed threat detection results: finding type, severity, affected resources, threat intelligence matches, anomaly indicators, description; findings delivered to EventBridge and/or S3
- **AWS Security Hub findings** — aggregated security findings from GuardDuty, Inspector, Macie, Config, and third-party integrations; normalized to ASFF (AWS Security Finding Format)
- **AWS Config change records** — configuration snapshots and change notifications for all monitored resources; tracks resource attribute changes over time
- **S3 Server Access Logs** — HTTP requests to S3 buckets: requester, bucket, key, operation, status code, error code, bytes sent, request time; separate from CloudTrail data events
- **Amazon CloudWatch Logs** — application logs, system logs, and custom metrics from EC2 instances, Lambda functions, ECS tasks, and other services; also the destination for many other AWS service logs
- **AWS IAM Credential Reports** — periodic export of all IAM users, their credentials status (password age, access key age, MFA enabled), and last-used information
- **EKS / ECS Audit Logs** — Kubernetes audit logs for EKS clusters: every API call to the Kubernetes API server; container start/stop events for ECS tasks
- **Route 53 Resolver Query Logs** — DNS queries made from within the VPC to Route 53 Resolver; captures domain queried, query type, response, and source IP

### Security Events to Look For

- **Root account usage** — any API call made with root account credentials is a high-priority alert; the root account should never be used for routine operations; look for CloudTrail events where userIdentity.type = "Root"
- **IAM policy changes** — CreatePolicy, PutUserPolicy, PutRolePolicy, AttachUserPolicy, AttachRolePolicy API calls; especially when granting AdministratorAccess or * permissions; changes outside change windows are suspicious
- **MFA disabled for an IAM user** — DeleteVirtualMFADevice or DeactivateMFADevice API calls; removing MFA from an account weakens its security posture and may indicate account compromise
- **New IAM user or access key created** — CreateUser, CreateAccessKey events; attackers often create new IAM users or access keys for persistence after an initial compromise
- **Overly permissive S3 bucket policy (public access)** — PutBucketPolicy or PutBucketAcl where the policy grants s3:GetObject to principal "*" or AWS: "*"; public S3 buckets are a leading cause of data breaches
- **Unusual API call patterns** — an IAM user or role calling APIs they have never called before, especially in new regions; or a spike in DescribeInstances, ListBuckets, or other discovery API calls (reconnaissance)
- **Access key usage from unexpected locations** — CloudTrail sourceIPAddress field showing API calls from a country or IP range that the key owner has never used before; may indicate stolen access keys
- **Disabling CloudTrail or GuardDuty** — StopLogging, DeleteTrail, DisableOrganizationAdminAccount, SuspendDataSource events; attackers disable logging to cover tracks; these should be critical alerts
- **Security group rule allowing 0.0.0.0/0** — AuthorizeSecurityGroupIngress with a rule that opens any port or a sensitive port (22, 3389, 5432) to 0.0.0.0/0; opens the resource to the entire internet
- **EC2 instance creation in an unusual region** — RunInstances in a region the organization does not normally use; common indicator of cryptomining or unauthorized resource provisioning
- **Data exfiltration via S3** — abnormally high S3 GetObject or SyncBuckets API call volume, or large data transferred to an external account; look for CloudTrail events with an unusual requester account ID in S3 data events
- **IAM role assumption by unusual service or account** — AssumeRole calls from unexpected principals, especially cross-account role assumptions; may indicate privilege escalation or lateral movement between AWS accounts

### SIEM Onboarding Steps

1. **Enable CloudTrail in all regions with multi-region trail.** By default, CloudTrail must be enabled per region. Create a multi-region trail that captures all regions and delivers to a central S3 bucket. Enable CloudTrail log file validation to detect log tampering.
2. **Configure S3 bucket for log delivery with appropriate policy.** The CloudTrail log S3 bucket should have: server-side encryption (SSE-S3 or SSE-KMS), versioning enabled, public access blocked, and a bucket policy that denies delete operations from non-admin principals.
3. **Enable CloudTrail data events for high-value resources.** By default, CloudTrail only captures management events. Enable data events for S3 (GetObject, PutObject, DeleteObject) on buckets containing sensitive data, and Lambda invocation events for critical functions.
4. **Connect CloudTrail S3 bucket to the SIEM.** Most SIEMs support S3 bucket ingestion via SQS notification (S3 sends an SQS notification on each new object, SIEM polls SQS and downloads the file) or via SNS topic subscription. Configure the SIEM's AWS S3 or CloudTrail add-on with an IAM role (using cross-account assume role or an access key) with GetObject permission on the CloudTrail bucket.
5. **Create an IAM role for SIEM collection.** Create a dedicated IAM role with minimum necessary permissions: s3:GetObject on the CloudTrail/log buckets, sqs:ReceiveMessage/DeleteMessage on the notification queue, and security-hub:GetFindings, guardduty:ListFindings for managed service data. Use role assumption from the SIEM's AWS account to avoid storing static access keys.
6. **Enable Amazon GuardDuty across all accounts and regions.** Enable GuardDuty in every region and account (use Organizations for delegated admin). Configure GuardDuty findings to publish to EventBridge, then route via an SNS topic or Lambda function to the SIEM's HTTP endpoint, or export findings to S3 for batch ingestion.
7. **Enable AWS Security Hub.** Security Hub aggregates findings from GuardDuty, Inspector, Macie, Firewall Manager, and third-party integrations. Enable Security Hub with AWS Foundational Security Best Practices standard. Configure findings export to S3 or EventBridge for SIEM ingestion.
8. **Enable VPC Flow Logs and route to SIEM.** Enable VPC Flow Logs for all VPCs in all regions. Deliver logs to CloudWatch Logs. Use a Kinesis Data Firehose or Lambda function to forward CloudWatch Logs to the SIEM in near real time. Alternatively, deliver directly to S3 and use S3 ingestion.
9. **Enable Route 53 Resolver Query Logs.** Enable DNS query logging for all VPCs. This captures all DNS lookups made from within the VPC and is essential for detecting C2 beaconing, DGA domains, and DNS tunneling.
10. **Normalize CloudTrail fields in the SIEM.** Key fields to parse and map: eventTime, eventSource, eventName, userIdentity.type, userIdentity.arn, userIdentity.accountId, sourceIPAddress, awsRegion, requestParameters, responseElements, errorCode, errorMessage.
11. **Configure IAM Credential Report export automation.** Schedule a Lambda function to run daily and export the IAM credential report, then ship to the SIEM. Use this data to maintain an accurate picture of IAM user MFA status, key age, and last used dates for reporting and alerting.
12. **Enable organization-level CloudTrail (if using AWS Organizations).** Configure a delegated admin account for CloudTrail that creates an organization trail capturing events from all member accounts. This is far more scalable than configuring CloudTrail in each account individually.

---

## 8. Cloud Services — Microsoft Azure

### What It Is

Microsoft Azure generates a wide range of audit and diagnostic logs covering infrastructure operations, identity management, network activity, and security findings. Azure Activity Logs provide the equivalent of AWS CloudTrail — a record of every management-plane operation. Azure Active Directory (AAD) generates sign-in and audit logs that are critical for detecting identity-based attacks in hybrid and cloud-only Microsoft environments. As Microsoft's cloud platform underpins both infrastructure and the entire M365 productivity suite, Azure logs are critical for any organization running on the Microsoft stack.

### Log Types Generated

- **Azure Activity Log** — resource-level management operations: VM create/delete, network security group changes, policy assignments, role assignments; equivalent to CloudTrail management events
- **Azure AD Sign-in Logs** — every interactive and non-interactive sign-in to Azure AD-protected resources: user, application, timestamp, IP, location, MFA result, Conditional Access policy result, risk level
- **Azure AD Audit Logs** — administrative actions in Azure AD: user creation, group changes, role assignments, application registration, password resets, MFA enrollment
- **Azure AD Risk Events / Identity Protection** — risky sign-ins flagged by Microsoft Identity Protection: anonymous IP, atypical travel, malware-linked IP, leaked credentials, password spray
- **Azure Defender for Cloud (Defender for Cloud) Alerts** — security alerts from CSPM and workload protection: VM-level threats, container threats, DNS anomalies, key vault threats, storage anomalies
- **NSG (Network Security Group) Flow Logs** — network traffic metadata similar to VPC Flow Logs: src/dst IP and port, protocol, flow direction, traffic decision (allowed/denied), bytes/packets; delivered to Storage Account
- **Azure Key Vault Audit Logs** — access and operations on Key Vault secrets, keys, and certificates: who accessed what secret, create/delete/update operations, policy changes
- **Azure Storage Account Access Logs** — HTTP request logs for blob, queue, and table storage: requester, operation, object accessed, status code, bytes transferred
- **Microsoft Graph API Activity Logs** — API calls made to Microsoft Graph; useful for detecting unauthorized access to directory data or mailboxes via Graph
- **Azure Firewall Logs** — application rule hits, network rule hits, DNS proxy logs, threat intelligence hits, IDPS (intrusion detection and prevention) alerts
- **Azure Monitor Metrics and Diagnostic Logs** — per-resource diagnostic data: VM performance metrics, SQL database logs, App Service logs, AKS cluster logs, Function App invocation logs
- **Microsoft Sentinel Analytics Alerts** — if Sentinel is the SIEM, its own detection rule alerts are a log source for correlation and case management

### Security Events to Look For

- **Privileged role assignment in Azure AD** — any addition of a user to Global Administrator, Privileged Role Administrator, Security Administrator, Exchange Administrator, or other high-privilege roles; look in Azure AD Audit Logs for "Add member to role" events
- **Guest account creation and elevated permissions** — creation of a B2B guest account followed by role assignment; external users with high-privilege roles are a persistent access risk
- **Conditional Access policy disabled or modified** — changes to Conditional Access policies that weaken security posture (removing MFA requirement, expanding allowed networks/locations); look in Azure AD Audit Logs for policy changes
- **Legacy authentication protocol usage** — sign-ins using Basic Authentication, SMTP AUTH, POP3, IMAP4, or legacy Exchange ActiveSync; these protocols bypass Conditional Access and MFA; look in Sign-in Logs where ClientAppUsed != "Modern Authentication Client"
- **Azure AD Connect server changes** — any configuration changes to AD Connect (the synchronization tool between on-prem AD and Azure AD); a compromised AD Connect server gives an attacker cloud admin access
- **Service principal secret or certificate creation** — creation of new credentials (client secrets or certificates) for service principals; attackers add credentials to existing service principals for persistent access; look in Azure AD Audit Logs for "Update application - Add client secret"
- **MFA fatigue attack indicators** — a user receiving a high volume of MFA push notifications in a short time (attackers repeatedly attempt login hoping the user approves a push out of annoyance); look in Sign-in Logs for many MFA prompts with result "MFA denied" or "MFA notification not answered" in quick succession for the same user
- **Unusual VM creation or deployment** — large numbers of VMs created in a short time, VMs created in unusual regions, or VM creation by accounts that don't normally deploy infrastructure; may indicate cryptomining or preparation for DDoS
- **Storage account key access or SAS token generation** — access to storage account keys via the portal or API; key compromise provides full access to storage without Azure AD authentication; SAS tokens with excessive permissions or duration
- **Password spray indicators in Sign-in Logs** — many failed sign-in attempts across multiple accounts from the same IP, with each account receiving only one or two attempts (to avoid lockout); look for high volume of sign-in failures from a single IP with Result = "Invalid username or password"
- **Azure Key Vault secret access by unusual identity** — a service principal or user accessing Key Vault secrets that they have not accessed before, or accessing many secrets in rapid succession (bulk secret dumping)
- **NSG rule change allowing inbound RDP/SSH** — an NSG inbound rule added that allows TCP/3389 or TCP/22 from source 0.0.0.0/0 or Internet; exposes Azure VMs to direct internet attack

### SIEM Onboarding Steps

1. **Configure Diagnostic Settings to stream logs to a central destination.** For Azure Activity Logs and resource-level diagnostic logs, go to Azure Monitor > Diagnostic Settings. Create a Diagnostic Setting at the subscription level to export the Activity Log to either: (a) Log Analytics Workspace, (b) Azure Event Hub (for third-party SIEMs), or (c) Storage Account (for archival). For Log Analytics, use Microsoft Sentinel. For third-party SIEMs (Splunk, IBM QRadar, etc.), use Azure Event Hub.
2. **Configure Azure AD Diagnostic Settings.** In Azure Active Directory > Diagnostic Settings, enable streaming of Sign-in Logs, Audit Logs, Risky Sign-ins, and Risk Events to the same Event Hub or Log Analytics Workspace configured above. This is a separate setting from the Azure Activity Log.
3. **Set up Azure Event Hub as a SIEM relay (for non-Sentinel SIEMs).** Create an Event Hub namespace and Event Hub instance. Configure all Diagnostic Settings to target this Event Hub. In the SIEM, configure the Azure Event Hub input (Splunk Add-on for Azure, QRadar Azure DSM, etc.) using an Event Hub SAS policy with Listen permission.
4. **Use Microsoft Sentinel built-in connectors (if using Sentinel).** In the Microsoft Sentinel Data Connectors blade, enable: Azure Active Directory (Sign-in and Audit Logs), Azure Activity, Microsoft Defender for Cloud, Azure Key Vault, Azure Network Security Groups, Azure Firewall. Most connectors require only a checkbox to enable; no custom configuration.
5. **Enable NSG Flow Logs and configure Traffic Analytics.** In Azure Network Watcher > Flow Logs, enable flow logs for all NSGs. Choose version 2 (includes bytes and packets). Send to a Storage Account. Optionally enable Traffic Analytics (sends to Log Analytics for structured querying). For the SIEM, either ingest from the Storage Account or use Log Analytics as the source.
6. **Enable Microsoft Defender for Cloud Standard Tier.** The free tier provides only security recommendations. The Standard/Defender plans provide security alerts for VMs, storage, containers, databases, and app services. Enable Defender plans for all resource types in all subscriptions. Configure Defender for Cloud to export alerts to the SIEM via the Continuous Export feature (exports to Event Hub or Log Analytics).
7. **Enable Azure Key Vault diagnostic logging.** For each Key Vault, configure a Diagnostic Setting to send AuditEvent logs to Log Analytics or Event Hub. This is not enabled by default and must be set per Key Vault.
8. **Configure Microsoft Entra ID Protection (formerly Azure AD Identity Protection) alerts.** In the Azure portal, Identity Protection > Export alerts to your SIEM via Diagnostic Settings or via the Microsoft Graph risky users/sign-ins API.
9. **Verify log retention settings.** Azure AD Sign-in Logs are retained for 30 days (P1/P2 license) or 7 days (free). Azure Activity Logs are retained for 90 days. For compliance requirements, ensure logs are exported to long-term storage (Log Analytics with workspace retention set to 90-365 days, or Storage Account for archival).
10. **Normalize Azure-specific field names.** Map: OperationName, Caller (Azure Activity), UserPrincipalName, IPAddress, Location, AppDisplayName, ResourceId, ResultType, ConditionalAccessStatus (Azure AD Sign-in) to your SIEM's common data model.
11. **Validate connectivity and test known event patterns.** Trigger test events: make an Azure portal login from a new browser (generates a sign-in log), create and delete a resource group (generates activity log), perform a failed login (generates failed sign-in). Confirm all three appear in the SIEM within acceptable latency.

---

## 9. Cloud Services — GCP

### What It Is

Google Cloud Platform generates structured, high-fidelity audit logs through its Cloud Audit Logs service and routes them via the Cloud Logging infrastructure. GCP's log architecture differs from AWS and Azure in that it uses a centralized log router with configurable sinks to export logs to BigQuery, Cloud Storage, or Pub/Sub. For security monitoring, Pub/Sub is the primary mechanism for streaming logs to an external SIEM. Google's Security Command Center (SCC) provides aggregated security findings across all GCP services, similar to AWS Security Hub.

### Log Types Generated

- **Cloud Audit Logs — Admin Activity** — every administrative API call that creates, modifies, or deletes GCP resources: VM instance operations, IAM binding changes, Cloud Storage bucket creation, network changes; always enabled, cannot be disabled
- **Cloud Audit Logs — Data Access** — read and write operations on data stored in GCP services (BigQuery queries, Cloud Storage reads, Firestore reads/writes); must be explicitly enabled per service (high volume, disabled by default)
- **Cloud Audit Logs — System Event** — GCP-generated events (not user-triggered): live migration of VM instances, automatic restarts; always enabled, cannot be disabled
- **Cloud Audit Logs — Policy Denied** — when a request is denied by a VPC Service Controls or IAM policy; indicates unauthorized access attempts
- **VPC Flow Logs** — network metadata for flows within a VPC: src/dst IP and port, protocol, bytes, packets, direction; must be enabled per subnet
- **Cloud IDS (Intrusion Detection System) Findings** — network-based threat detection findings from Google's managed IDS: malware communication, exploits, command-and-control, vulnerabilities; delivered via Pub/Sub
- **Security Command Center Findings** — aggregated security findings from Event Threat Detection, Security Health Analytics, Container Threat Detection, Web Security Scanner, and third-party sources
- **Cloud DNS Logs** — DNS queries made from within GCP VPCs to Cloud DNS; must be enabled per network policy
- **GCS (Cloud Storage) Access Logs** — HTTP access logs for Cloud Storage buckets: requester, bucket, object, operation, status, bytes; delivered to a designated GCS bucket
- **Cloud Armor Security Logs** — WAF and DDoS protection logs: matched rules, blocked requests, allowed requests, IP reputation matches
- **Google Kubernetes Engine (GKE) Audit Logs** — Kubernetes API server audit logs for GKE clusters: every API call, user, resource, verb, response code
- **Firebase and App Engine Logs** — application-level logs from Firebase services and App Engine applications; forwarded through Cloud Logging

### Security Events to Look For

- **IAM binding changes with overly permissive roles** — projects.setIamPolicy or organizations.setIamPolicy calls adding the "roles/owner", "roles/editor", or "roles/iam.securityAdmin" role to a user or service account, especially if the subject is external to the organization or a newly created service account
- **Service account key creation or export** — iam.serviceAccounts.keys.create API call; service account keys are long-lived credentials that, if exported and stolen, provide persistent access outside GCP's federated authentication; should trigger an alert for any production service account
- **Project-level IAM policy changes** — any change to a project's IAM policy binding (setIamPolicy) that adds new members or expands permissions; particularly for bindings that include "allUsers" or "allAuthenticatedUsers" (public access)
- **Public bucket exposure** — storage.buckets.setIamPolicy adding allUsers:roles/storage.objectViewer or allAuthenticatedUsers:roles/storage.objectViewer binding to a Cloud Storage bucket; makes bucket contents publicly accessible
- **Privilege escalation via service account impersonation** — iam.serviceAccounts.actAs or iamcredentials.serviceAccounts.generateAccessToken called by an account that impersonates a higher-privileged service account; a common GCP privilege escalation path
- **Unusual API access patterns** — a service account or user calling APIs (iam.serviceAccounts.list, compute.instances.list, storage.buckets.list) that represent broad reconnaissance of the environment; especially from unexpected source IPs
- **GCP organization policy violation** — actions that violate an organization policy constraint being denied (recorded in Policy Denied audit logs); may indicate an attempted bypass of security guardrails
- **Resource creation in new or unusual regions** — compute.instances.insert or similar resource creation calls in regions the organization does not typically use; potential cryptomining
- **Security Command Center — high severity findings** — SCC Event Threat Detection findings such as "Malware: Bad Domain", "Persistence: New API Method", "Exfiltration: BigQuery Data Extraction", "Initial Access: Compromised Credentials" should be high-priority alerts in the SIEM
- **Cloud Functions or Cloud Run deployment from unexpected source** — cloudfunctions.functions.create or run.services.create from a principal that does not normally deploy serverless resources; attackers use serverless functions for C2 relay or persistence
- **Logging sink deleted or modified** — logging.sinks.delete or logging.sinks.update events; attackers may attempt to disable log export to prevent SIEM detection

### SIEM Onboarding Steps

1. **Verify Cloud Audit Logs are enabled at the organization level.** Admin Activity and System Event logs are always enabled. Navigate to Cloud Logging > Log Router and verify organization-level audit logging is configured. For Data Access logs, navigate to IAM & Admin > Audit Logs and enable relevant services (Storage, BigQuery, IAM).
2. **Create a Log Router Sink for security-relevant logs.** In Cloud Logging > Log Router, create a new sink with a filter that captures: cloudaudit.googleapis.com, security-related log names, and VPC Flow Logs. Use an inclusion filter such as: `logName =~ "cloudaudit.googleapis.com" OR logName =~ "compute.googleapis.com/vpc_flows"`. Set the sink destination to a Pub/Sub topic.
3. **Create a Pub/Sub topic and subscription for SIEM consumption.** Create a Pub/Sub topic as the sink destination. Create a Pub/Sub pull subscription that the SIEM will use to consume messages. Grant the log sink service account the roles/pubsub.publisher permission on the topic.
4. **Configure the SIEM to subscribe to the Pub/Sub subscription.** Most SIEMs with GCP support use a Pub/Sub pull subscription. Create a Google Cloud service account with roles/pubsub.subscriber and roles/pubsub.viewer on the subscription. Download the service account JSON key (or use Workload Identity Federation where supported). Configure the SIEM's GCP input with the project ID, subscription ID, and credentials.
5. **Enable Security Command Center and configure findings export.** In Security Command Center, ensure Event Threat Detection and Security Health Analytics are enabled. Navigate to SCC Settings > Continuous Exports and create an export to the same Pub/Sub topic (or a dedicated SCC Pub/Sub topic) used for SIEM ingestion.
6. **Enable VPC Flow Logs for all subnets.** In VPC Network > VPC networks, click each subnet and enable Flow Logs. Set the aggregation interval to 1 minute (minimum) and include metadata fields. This generates significant volume; use a sampling rate (0.5 recommended) to control costs while maintaining visibility.
7. **Enable Cloud DNS logging.** In Cloud DNS > DNS policies, create or modify a DNS policy to enable DNS logging for each VPC network. This creates DNS query logs in Cloud Logging that are automatically captured by the log sink.
8. **Configure IAM for least-privilege collection.** The service account used by the SIEM should have only: roles/pubsub.subscriber on the Pub/Sub subscription, and optionally roles/securitycenter.findingsViewer if using the SCC API directly. Do not grant broader roles.
9. **Parse GCP Cloud Audit Log fields in the SIEM.** Key fields to extract: logName, timestamp, protoPayload.methodName, protoPayload.authenticationInfo.principalEmail, protoPayload.requestMetadata.callerIp, protoPayload.resourceName, protoPayload.serviceName, severity, resource.type, resource.labels.project_id.
10. **Test the pipeline with known audit events.** Create a Cloud Storage bucket, modify an IAM binding, and delete the bucket. Confirm all three operations appear in the SIEM within 5 minutes. Check that all required fields are parsed correctly before deploying detection rules.

---

## 10. Cloud Services — Microsoft 365

### What It Is

Microsoft 365 (M365) is Microsoft's cloud-based productivity suite encompassing Exchange Online, SharePoint, OneDrive, Teams, and many additional services. M365 logs via the Unified Audit Log (UAL) capture user and administrator activity across all M365 services in a single, centralized log stream. Because M365 environments contain the most sensitive business data (email, documents, collaboration) and are authenticated via Azure Active Directory, they are a high-value target for attackers — especially for Business Email Compromise, data theft, and OAuth-based persistence. M365 logs complement Azure AD logs (covered in Section 8) with application-layer visibility.

### Log Types Generated

- **Unified Audit Log (UAL)** — the central log stream for all M365 user and admin activity; RecordTypes include Exchange (email operations), SharePoint (document operations), Teams (messaging/meetings), Azure AD (directory changes), OneDrive (file operations), Power Platform, and more
- **Azure AD Sign-in Logs** — covered in Section 8; accessible from both Azure AD portal and M365 Security Center
- **Exchange Online mailbox audit logs** — mailbox-level operations: message read, message sent, item deleted, folder created, folder permission change, message move; subject to mailbox audit logging being enabled per-mailbox (enabled by default in E3/E5 since 2019)
- **SharePoint / OneDrive access and sharing logs** — file viewed, downloaded, shared, deleted; external sharing link creation; folder operations; access by external users
- **Microsoft Teams activity logs** — messages sent (Teams/channels), meetings created/joined, file shared in Teams, external guest added to team, Teams app installed
- **Power Automate / Power Apps activity logs** — flow created/modified/run, connector used, data accessed via Power Platform; relevant for detecting shadow IT automation and data access via connectors
- **DLP (Data Loss Prevention) policy match logs** — content containing sensitive data patterns (credit card numbers, SSNs, health information) matched a DLP policy; policy action taken (audit, block, override with justification)
- **Microsoft Secure Score change events** — changes to the organization's security configuration that affect Secure Score; administrator disabled a recommended control
- **Microsoft Defender for Office 365 alerts** — phishing campaign alerts, malware detections in email/SharePoint, zero-hour auto purge (ZAP) actions, attack simulation results

### Security Events to Look For

- **Auto-forwarding rule to external domain** — a user's mailbox is configured with an inbox rule (RecordType: ExchangeItem, Operation: New-InboxRule or Set-InboxRule) that forwards email to an external address; or a transport rule added that redirects email to external addresses; this is a critical BEC indicator
- **OAuth app consent to suspicious permissions** — a user granted consent to a third-party OAuth application with permissions including Mail.ReadWrite, Mail.Send, Files.ReadWrite.All, Contacts.ReadWrite; look in UAL for Operation "Add OAuth2PermissionGrant" with sensitive resource permissions; especially if the app is not in the approved app catalog
- **Mass download from SharePoint or OneDrive** — a user downloads a large number of files (hundreds or thousands) in a short time window; look in UAL for high volume FileDownloaded events from a single user account; may indicate data theft
- **External sharing link created for large volume of files** — a user creates external sharing links (AnonymousLinkCreated or SecureLinkCreated) for a large number of documents in a short time; potential data exfiltration preparation
- **Admin role assignment in M365** — a user is assigned a high-privilege M365 admin role (Global Administrator, Exchange Administrator, SharePoint Administrator, Security Administrator) via the M365 Admin Center; look in UAL for "Add member to role" with a high-privilege role
- **Teams external guest added with unusual patterns** — external users added as guests to Teams at high volume, or an external guest from an unusual domain added to a sensitive Team; look in UAL for TeamsUserAddedToTeam events with external user UPNs
- **Legacy authentication sign-in** — sign-ins to M365 using basic authentication (IMAP, POP3, SMTP AUTH, Exchange ActiveSync with legacy clients) that bypass Conditional Access and MFA; look in Azure AD Sign-in Logs for ClientAppUsed values that indicate legacy protocols
- **DLP policy violation — sensitive data exfiltration** — a DLP policy match where the action was "Override" (user overrode the DLP block with a business justification) or "Allow" (audit-only policy); especially for sensitive content categories (financial, health, PII) being shared externally
- **Bulk email send from potentially compromised account** — a user's Exchange Online account sends a significantly higher volume of email than their historical baseline, especially to external recipients; look in Exchange message trace logs or UAL MailSent events with high volume in a short window
- **Power Automate flow accessing sensitive data** — a Power Automate flow created by a non-IT user that uses the SharePoint, Exchange, or SQL Server connector to access sensitive data and potentially exfiltrate it to an external service (Dropbox, HTTP webhook, email)
- **MFA bypass via legacy authentication or Conditional Access gap** — a sign-in that would normally require MFA but succeeded without it; look for sign-in events where MFA is not marked as satisfied but the account policy requires MFA — this could indicate a Conditional Access policy gap or legacy auth bypass

### SIEM Onboarding Steps

1. **Verify the Unified Audit Log is enabled.** In the Microsoft Purview compliance portal (compliance.microsoft.com), navigate to Audit > Start recording user and admin activity. This must be explicitly enabled and is a prerequisite for all M365 log collection. Verify with the PowerShell command: `Get-AdminAuditLogConfig | Select-Object UnifiedAuditLogIngestionEnabled`.
2. **Set UAL retention to the maximum for the license tier.** E3 licenses provide 90-day retention; E5 provides 1-year retention (10-year with the audit add-on). For longer retention, export logs to Azure Blob Storage or the SIEM's own storage. Verify retention via the Purview Audit retention policies.
3. **Configure the Microsoft 365 connector in the SIEM.** Use the Office 365 Management Activity API. Register an Azure AD application with Application permissions: ActivityFeed.Read, ActivityFeed.ReadDlp, ServiceHealth.Read. Grant admin consent for the application. Configure the SIEM's M365 input with the tenant ID, client ID, and client secret.
4. **Subscribe to UAL content types.** The Management Activity API requires subscribing to content types before events are available. Subscribe to: Audit.General, Audit.Exchange, Audit.SharePoint, Audit.AzureActiveDirectory, DLP.All. Use the API endpoint: `POST /api/v1.0/{tenantId}/activity/feed/subscriptions/start?contentType={contentType}`.
5. **Configure Microsoft Sentinel M365 Defender connector (if using Sentinel).** In Sentinel Data Connectors, enable the "Microsoft 365 Defender" connector. This ingests MDE, MDO, MCAS, and Defender for Identity alerts and raw telemetry (DeviceEvents, DeviceProcessEvents, etc.) directly into Sentinel with no additional API configuration.
6. **Enable mailbox audit logging verification.** Since 2019, mailbox audit logging is enabled by default for E3/E5 users. Verify with PowerShell: `Get-Mailbox -ResultSize Unlimited | Select-Object UserPrincipalName, AuditEnabled`. Ensure AuditEnabled = True for all mailboxes. Enable for any that show False.
7. **Enable Defender for Office 365 alert streaming.** In the Microsoft 365 Defender portal, go to Settings > Microsoft 365 Defender > Streaming API (if licensed). Configure alert and event streaming to Azure Event Hub for near-real-time ingestion into the SIEM.
8. **Integrate Azure AD Sign-in Logs alongside UAL.** M365 authentication events appear in Azure AD Sign-in Logs (see Section 8 for onboarding steps), not in the UAL. Configure both sources to get complete coverage of authentication + activity.
9. **Configure DLP alert integration.** In the Microsoft Purview compliance portal, set up alert policies for DLP policy matches at high or medium severity. Configure these alerts to forward to the SIEM via Logic App, Power Automate, or the Purview Activity API.
10. **Validate the log pipeline with test events.** Log in to M365 from an incognito window (generates sign-in event), create a test inbox rule (generates inbox rule event), share a file in SharePoint (generates sharing event). Confirm all three events appear in the SIEM within 15 minutes (UAL has a typical 15-30 minute delay from event to availability in the API).

---

## 11. DNS Logs

### What It Is

DNS (Domain Name System) logs capture every domain name lookup made from hosts within the network, along with the response received. Because DNS is a foundational protocol that is almost universally allowed through network controls (even in restricted environments), it is frequently abused by attackers for command-and-control communication, data exfiltration, and reconnaissance. DNS logs provide visibility into what external domains endpoints are communicating with, and are one of the most valuable sources for detecting both known-bad indicators (threat intelligence matches) and behavioral anomalies (DGA, tunneling, beaconing).

### Log Types Generated

- **Query logs** — every DNS query: source IP (client), queried domain name (FQDN), query type (A, AAAA, MX, TXT, NS, CNAME, PTR, SRV), timestamp, resolver IP
- **Response logs** — DNS response to the query: response code (NOERROR, NXDOMAIN, SERVFAIL, REFUSED, NOTIMP), resolved IP address(es), TTL, authoritative/non-authoritative
- **NXDOMAIN events** — queries for domains that do not exist; high volume NXDOMAIN responses are a key DGA and C2 indicator
- **Zone transfer logs** — AXFR or IXFR requests (requests for full or incremental zone transfers); should only come from authorized secondary DNS servers
- **DNSSEC validation events** — DNSSEC signature validation results (validated, bogus, insecure); bogus results may indicate DNS spoofing attempts
- **Recursive query events** — DNS server performing recursive resolution on behalf of a client; logs the full resolution chain
- **Dynamic DNS update events** — DDNS updates (clients updating their own DNS records); unexpected DDNS updates may indicate a compromised host attempting to establish a callback mechanism
- **RPZ (Response Policy Zone) hit logs** — when a DNS firewall or RPZ blocks a query based on a threat intelligence feed, the block event is logged

### Security Events to Look For

- **DGA (Domain Generation Algorithm) detection** — malware uses DGA to generate large numbers of random-looking domain names, querying them until the active C2 domain responds; look for: high entropy domain names (random-looking character strings), domains with very short TTLs, NXDOMAIN responses for many similar-pattern domains, queries to domains with no prior history or Alexa ranking
- **DNS tunneling** — attackers encode data in DNS queries and responses to bypass firewalls; look for: abnormally long subdomain labels (> 50 characters), high volume of queries to a single parent domain (e.g., 100+ queries/minute to evil.com), TXT record queries (TXT records carry arbitrary text data), high-entropy subdomain names, base32/base64 encoded subdomains, unusually large DNS response sizes (> 512 bytes)
- **C2 beaconing via DNS** — malware that uses DNS as a covert channel will make periodic, regular queries to a C2 domain; look for: consistent query intervals to the same domain, small request/response sizes, queries continuing even when there is no other network activity from the host
- **Newly registered domains** — domains registered within the last 30 days are high-risk; attackers register fresh domains to avoid reputation-based blocking; enrich DNS logs with domain age from threat intelligence feeds and alert when a query resolves a domain < 30 days old
- **Typosquatting and homoglyph domains** — domains designed to look like legitimate brands: micros0ft.com, paypa1.com, arnazon.com; use string distance algorithms (Levenshtein distance) to detect domains similar to known legitimate domains in your watchlist
- **NXDOMAIN spike from a single host** — a single endpoint generating hundreds of NXDOMAIN responses in a short time indicates DGA malware actively looking for its active C2 domain; this is a high-confidence malware indicator
- **Internal host querying unusual TLDs** — queries to .onion (Tor), .bit (Namecoin), or unusual country-code TLDs from internal hosts that have no business reason to access such domains
- **DNS queries bypassing the corporate resolver** — internal hosts making DNS queries directly to external resolvers (8.8.8.8, 1.1.1.1, 9.9.9.9) rather than the internal DNS server; may indicate an attempt to bypass DNS-based filtering or logging
- **Zone transfer attempts from unauthorized IPs** — an AXFR or IXFR request from an IP that is not an authorized secondary DNS server; indicates DNS reconnaissance by an attacker
- **Reverse lookup (PTR) anomalies** — a host performing many PTR record lookups against an IP range; indicates network scanning and host enumeration

### SIEM Onboarding Steps

1. **Enable DNS query logging on Windows DNS Servers.** Windows DNS Server debug logging is not enabled by default. Enable it via DNS Manager > Server Properties > Debug Logging > Log Packets for Debugging. Select: Query/Response, Details, Full Packets. Note: debug logging writes to a local text file (dns.log) which must then be forwarded. Alternative: enable DNS Audit Events in the Windows Server 2016+ DNS Server Operational event log (less verbose but structured).
2. **Enable DNS logging via PowerShell (Windows).** Run: `Set-DnsServerDiagnostics -All $true` on each DNS server. This enables all diagnostic logging categories. Combine with Winlogbeat to tail the DNS debug log file and forward to the SIEM.
3. **Enable BIND query logging (Linux).** Edit /etc/named.conf and add a logging clause: `channel query_log { file "/var/log/named/query.log" versions 3 size 5m; severity dynamic; print-time yes; }; category queries { query_log; };`. Restart named and use Filebeat to forward the log file.
4. **Deploy Zeek (formerly Bro) for network-based DNS log collection.** Zeek passively sniffs network traffic and generates structured DNS logs (dns.log) with rich fields: query, qtype, qclass, rcode, answers, TTL, rejected. Deploy Zeek on a network tap or SPAN port that sees DNS traffic. Zeek logs are natively supported by many SIEMs and provide passive collection that does not require changes to DNS server configurations.
5. **Integrate Infoblox or BlueCat DDI (if present).** Enterprise DNS/DHCP/IPAM platforms like Infoblox provide syslog output or REST API access for DNS query logs. Configure the Infoblox reporting server to forward logs via syslog/CEF to the SIEM. Infoblox also provides RPZ (Response Policy Zone) threat feed integration with corresponding block event logs.
6. **Configure DNS query log forwarding for cloud DNS.** For AWS Route 53 Resolver query logging, see Section 7. For Azure DNS: configure Azure Private Resolver diagnostic logs. For GCP Cloud DNS: enable DNS logging policy (see Section 9). For Cisco Umbrella: use the Umbrella reporting API or log management export to forward query logs to the SIEM.
7. **Integrate with threat intelligence for domain reputation enrichment.** Configure the SIEM to enrich DNS query events with threat intelligence lookups: domain age (passive DNS data), domain reputation (VirusTotal, Cisco Talos, AlienVault OTX), DGA classification (Umbrella, ProtectWise). Most SIEMs support lookup tables or automated threat intel enrichment.
8. **Build a NXDOMAIN baseline and threshold alert.** Establish a baseline of NXDOMAIN responses per host per hour. Alert when a single host exceeds 3x the baseline in any 60-minute window. This is a reliable DGA detection heuristic.
9. **Configure Shannon entropy calculation for subdomain analysis.** Implement a SIEM search or scheduled rule that calculates the Shannon entropy of the subdomain component of queried domains. Domains with entropy > 3.5 bits per character warrant investigation for DGA or DNS tunneling.
10. **Test DNS log collection with known-good queries.** From a monitored host, query: a known-bad domain (from a public blocklist), a newly-registered domain, and a non-existent domain (NXDOMAIN). Confirm all three appear in the SIEM with the expected response codes and proper field parsing.

---

## 12. DHCP Logs

### What It Is

DHCP (Dynamic Host Configuration Protocol) logs record IP address assignments, renewals, and releases for all network-connected devices. While DHCP logs are often overlooked in security programs, they serve a critical supporting function: they provide the IP address-to-hostname and IP address-to-MAC address mappings that are essential for attributing network activity logged by firewalls, NetFlow, and proxy logs to specific physical devices and users. Without DHCP logs, it is often impossible to determine which device was responsible for a network-based security event that occurred in the past.

### Log Types Generated

- **DHCP ACK events** — IP address lease granted: client MAC address, client hostname, assigned IP address, lease start time, lease duration, DHCP server IP, subnet
- **DHCP NACK events** — IP address request refused by the DHCP server: client MAC, requested IP, reason for refusal
- **DHCP DISCOVER events** — client broadcasting request for an IP address: client MAC, client hostname (if sent), timestamp
- **DHCP OFFER events** — server offering an IP address to a client: offered IP, lease duration, options
- **DHCP REQUEST events** — client requesting a specific offered IP: client MAC, requested IP
- **DHCP RELEASE events** — client releasing its IP address lease: client MAC, released IP, timestamp
- **DHCP RENEW events** — client renewing its existing lease before expiration: client MAC, IP being renewed, new lease duration
- **DHCP DECLINE events** — client declining an offered IP (e.g., because it detected a conflict): client MAC, declined IP
- **DHCP lease database exports** — full exports of the current lease table: all active IP-to-MAC-to-hostname mappings at a point in time

### Security Events to Look For

- **Rogue DHCP server detection** — a DHCP OFFER or DHCP ACK originating from an IP that is not the authorized DHCP server on that subnet; indicates a rogue DHCP server that could poison client routing and DNS, enabling man-in-the-middle attacks
- **New or unknown MAC addresses on sensitive VLANs** — a DHCP request from a MAC address that has not previously been seen on a sensitive VLAN (e.g., a server VLAN, a SCADA/OT network, a payments network); indicates a new and potentially unauthorized device
- **MAC address spoofing indicators** — the same IP address being assigned to rapidly changing MAC addresses, or the same MAC address appearing on different subnets at the same time; may indicate MAC spoofing to bypass MAC-based access controls
- **DHCP starvation attack** — a flood of DHCP DISCOVER packets from rapidly changing or spoofed MAC addresses (often incrementing); the attack exhausts the DHCP pool, preventing legitimate clients from obtaining IP addresses (DoS)
- **Unauthorized devices on restricted segments** — a DHCP request on a restricted VLAN (e.g., a guest VLAN, IoT VLAN) from a MAC address belonging to a corporate asset type, or vice versa; indicates VLAN mislabeling or unauthorized network access
- **IP/MAC mapping changes for critical servers** — a server that previously had a static or consistent DHCP-assigned IP has had its MAC address change; may indicate the server was replaced or a VM was migrated, but could also indicate hardware manipulation
- **Rapid lease cycling** — a device requesting and releasing IP addresses in rapid succession; may indicate reconnaissance tooling or network automation that is not properly configured
- **DHCP requests from known-malicious MAC vendor prefixes** — if the OUI (first 3 bytes of MAC address) does not match any known hardware vendor in the environment, the device may be from an unknown or suspicious manufacturer

### SIEM Onboarding Steps

1. **Enable DHCP Server logging on Windows DHCP Server.** Windows DHCP Server logs are enabled by default and written to: `C:\Windows\System32\dhcp\DhcpSrvLog-*.log` (one file per day of the week). Deploy Winlogbeat or NXLog to tail these files and forward to the SIEM. The Windows DHCP log format is CSV-like with defined field positions.
2. **Configure ISC DHCP (Linux) syslog output.** ISC DHCP daemon logs to syslog by default (facility daemon, or dhcpd if configured). Ensure rsyslog or syslog-ng is configured to forward dhcpd messages to the SIEM syslog receiver. Key log entries begin with: DHCPDISCOVER, DHCPOFFER, DHCPREQUEST, DHCPACK, DHCPNAK, DHCPRELEASE.
3. **Configure Kea DHCP (modern Linux replacement for ISC DHCP).** Kea DHCP supports syslog output and a database backend (MySQL, PostgreSQL). Configure the kea-dhcp-lease-cmds hook library and the JSON log output to forward to the SIEM.
4. **Integrate Infoblox DHCP log collection.** If using Infoblox DDI, configure the Infoblox reporting server to forward DHCP events via syslog/CEF. Infoblox provides structured DHCP logs that include additional metadata not available in standard DHCP server logs.
5. **Build an IP-to-MAC-to-hostname lookup table in the SIEM.** Configure a scheduled task or a real-time lookup that processes DHCP ACK events and maintains a lookup table mapping IP address → MAC address → hostname → last-seen timestamp. This table is used to enrich other log sources (firewall, proxy, NetFlow) with device identity.
6. **Set up MAC address OUI enrichment.** Enrich MAC addresses with their OUI vendor name using the IEEE OUI database. Build a lookup table or use a SIEM enrichment function to map the first 3 bytes of each MAC to a vendor name. Flag MAC addresses with no matching OUI entry.
7. **Correlate DHCP with asset inventory.** Configure the SIEM to compare DHCP ACK events against the organization's CMDB or asset inventory. Alert when a DHCP request comes from a MAC address that is not in the asset inventory for that subnet.
8. **Configure rogue DHCP detection.** Build a lookup table of authorized DHCP server IPs per subnet. Alert when any DHCP OFFER or DHCP ACK is observed on the network (via passive monitoring or firewall logs) originating from an IP that is not in the authorized DHCP server list.
9. **Set up DHCP starvation detection threshold.** Alert when more than 100 DHCP DISCOVER events are received from unique MAC addresses within a 60-second window on the same subnet.
10. **Test DHCP log collection.** Connect a test device to the network, allow it to obtain a DHCP lease, and disconnect it. Confirm the DHCPDISCOVER, DHCPOFFER, DHCPREQUEST, DHCPACK, and DHCPRELEASE events all appear in the SIEM with the correct MAC address, hostname, and IP address.

---

## 13. Web Proxy / Secure Web Gateway

### What It Is

A web proxy or Secure Web Gateway (SWG) sits between internal users and the internet, inspecting and logging all web traffic. Web proxy logs provide user-level visibility into which websites and web services are being accessed, which is critical for detecting malware communications, data exfiltration, and policy violations. Combined with threat intelligence enrichment, web proxy logs are one of the highest-value sources for detecting command-and-control (C2) beaconing, drive-by downloads, and access to phishing sites. Many modern SWG products (Zscaler, Netskope, Cisco Umbrella) are cloud-delivered and include built-in threat intelligence.

### Log Types Generated

- **URL request logs** — full URL requested (or at minimum, domain + path), timestamp, client IP, username (if authenticated), HTTP method (GET, POST, PUT, DELETE), HTTP status code (200, 301, 404, 403, etc.), content type, response size, response time
- **Category classification** — URL category assigned by the proxy (e.g., Business, Social Media, Malware, Phishing, Botnets, Anonymizers, Adult Content, Cloud Storage), action taken (allowed, blocked, alerted)
- **Bandwidth usage** — bytes uploaded (request body size) and bytes downloaded (response size) per request; essential for detecting data exfiltration
- **MIME type filtering logs** — content type of the response (application/exe, application/zip, application/pdf), action taken (allowed, blocked, sandboxed)
- **SSL/TLS inspection logs** — for proxies performing SSL inspection, the decrypted request details (previously encrypted HTTPS traffic now visible as plaintext URL and content); certificate details of the destination
- **User identity mapping** — mapping of client IP to username via AD authentication integration (NTLM, Kerberos, or explicit proxy authentication); critical for attributing web activity to individual users
- **Blocked request logs** — requests denied by the proxy due to category policy, threat intelligence, or content inspection; includes the reason for the block
- **Application identification logs** — (cloud SWG) identifies which SaaS application was accessed (Salesforce, Box, Dropbox, Google Drive) for shadow IT discovery
- **Policy override/bypass logs** — when a user bypasses a policy block with a business justification; the justification text and the bypassed category are logged

### Security Events to Look For

- **Known malicious URL or domain requests** — requests to URLs or domains that match threat intelligence indicators (malware C2, phishing, malware distribution); look for requests to categories classified as Malware, Phishing, Botnets, or Command-and-Control
- **C2 beaconing via HTTP/HTTPS** — a client making highly regular periodic HTTP or HTTPS requests to the same external host; look for requests at consistent intervals (every 60 seconds, every 5 minutes), consistent request sizes, and consistent URL patterns; the regularity distinguishes beaconing from normal browsing
- **Malware download indicators** — requests that result in a download of an executable, script, or archive file type (application/exe, application/x-msdownload, application/zip, application/gzip) from a non-business domain, especially if the URL was accessed for the first time or the domain is newly registered
- **Unusual data upload volume** — HTTP POST requests with unusually large request body sizes to external services; indicates potential data exfiltration via web upload; look for total upload bytes per user exceeding a threshold (e.g., > 100 MB) in a day, especially to cloud storage or personal email services
- **Access to newly registered domains** — requests to domains registered within the last 30 days; attackers register fresh domains for phishing, C2, and malware distribution to avoid reputation-based blocking; enrich with domain age data
- **Credential phishing site access** — a user accessing a URL that is classified as a phishing page or where the certificate subject matches a typosquatted or brand-impersonation domain; indicates a user may have clicked a phishing link
- **Tor exit node / VPN / anonymizer usage** — requests routed through Tor exit nodes, commercial VPN services, or web anonymizers; indicates an attempt to bypass monitoring and may indicate data exfiltration or policy violation
- **Policy bypass and override abuse** — high volume of user-initiated policy overrides (clicking "continue to site" past a warning); indicates either poor policy calibration or a user repeatedly accessing suspicious content
- **Shadow IT SaaS discovery** — access to unapproved SaaS applications (personal Dropbox, personal Google Drive, unauthorized collaboration tools); indicates data governance risk
- **SSL certificate anomalies** — SSL inspection detecting self-signed certificates, expired certificates, certificate CN/SAN mismatches, or certificates issued by untrusted CAs; may indicate an adversary-controlled server or a misconfigured application
- **DNS-over-HTTPS (DoH) usage** — access to known DoH resolvers (cloudflare-dns.com, dns.google, dns.nextdns.io) via HTTPS; indicates an endpoint is attempting to bypass the corporate DNS resolver and proxy DNS monitoring

### SIEM Onboarding Steps

1. **Configure syslog export from the proxy/SWG.** Most web proxies support syslog output (UDP/TCP). Configure the syslog destination to point to your SIEM listener. For large-volume environments, use TCP syslog with connection-oriented delivery to prevent log loss. Configure the log format — W3C Extended Log Format or Blue Coat Access Log Format are common; prefer CEF if available as most SIEMs have pre-built parsers.
2. **Apply the vendor-specific parser:**
   - **Zscaler Internet Access (ZIA):** Zscaler supports log streaming via Nanolog Streaming Service (NSS). Deploy a Zscaler NSS virtual appliance or configure cloud NSS (if available in your tier). NSS streams logs to the SIEM in real time. Use the Zscaler add-on for your SIEM.
   - **Cisco Umbrella (cloud proxy):** Configure Umbrella Log Management in the Umbrella dashboard to store logs in an AWS S3 bucket provided by Cisco. Configure your SIEM to poll the S3 bucket. Logs are in CSV format with a defined schema.
   - **Blue Coat / Symantec ProxySG:** Configure the ProxySG access log in W3C or Squid format and forward via syslog. Use the Symantec ProxySG add-on.
   - **Forcepoint Web Security:** Configure the Forcepoint policy server to forward logs via syslog in CEF format.
3. **Enable user identity enrichment.** For the SIEM to attribute web activity to named users (rather than IP addresses), the proxy must be integrated with Active Directory for authentication (NTLM, Kerberos, or explicit proxy). Verify the username field is populated in the logs. If not, set up the proxy's AD authentication integration.
4. **Normalize critical fields.** Map: timestamp, username (or src_ip for unauthenticated), dst_domain, dst_url, http_method, http_status_code, bytes_in, bytes_out, category, action (allowed/blocked), user_agent, content_type, threat_name (if detected).
5. **Integrate threat intelligence for URL and domain enrichment.** Configure the SIEM to enrich the destination domain from proxy logs with threat intelligence lookups: VirusTotal, Cisco Talos, AlienVault OTX, or your preferred TI platform. Build lookup tables for known-bad indicators that trigger alerts without requiring external API calls for every event.
6. **Build a daily bandwidth baseline per user.** Calculate average daily upload and download volume per user over a 30-day baseline period. Alert when a user's daily upload exceeds 3x their baseline or exceeds an absolute threshold (e.g., 500 MB upload in a day).
7. **Configure SSL inspection (if not already enabled).** Web proxy SSL inspection decrypts HTTPS traffic for inspection. This is necessary for detecting C2 over HTTPS and malware downloads via HTTPS. Configure SSL inspection with appropriate certificate pinning exceptions and privacy exclusions (banking sites, healthcare portals).
8. **Enable application identification / CASB integration.** If the SWG includes CASB (Cloud Access Security Broker) functionality, enable application identification to log which SaaS applications are being accessed. This is the foundation for shadow IT discovery and cloud data governance alerts.
9. **Set up C2 beaconing detection logic.** Build a scheduled search or correlation rule that: groups proxy log events by client IP and destination domain, counts events per time window (e.g., per hour), identifies destinations that receive requests at regular intervals with low variance in request timing. Flag hosts where a single external destination receives > 10 requests/hour with timing regularity > 80%.
10. **Test with known-blocked and known-allowed URLs.** Request a URL from a test device that should be blocked (use a known-bad domain from a public blocklist). Confirm the block appears in the SIEM with the correct category and action. Then request a legitimate site and confirm it appears as an allowed event with the correct user attribution.

---

## 14. Network Flow / NetFlow / IPFIX

### What It Is

Network flow data (NetFlow, IPFIX, sFlow, jFlow) provides a metadata summary of every network conversation occurring across monitored network infrastructure — routers, switches, firewalls, and dedicated flow probes. Unlike full packet capture (PCAP), flow data does not contain payload content, but it records the key attributes of every conversation: who talked to whom, on which port and protocol, how much data was transferred, and for how long. This makes flow data the highest-volume but most scalable source of network-wide visibility, and is critical for detecting lateral movement, east-west traffic anomalies, and large-scale data exfiltration that may not be visible to perimeter-only monitoring.

### Log Types Generated

- **Flow records (per-conversation)** — source IP, destination IP, source port, destination port, IP protocol (TCP/UDP/ICMP), input interface, output interface, bytes transferred (total), packets transferred (total), start time, end time, duration, TCP flags, DSCP marking
- **Aggregated flow summaries** — top talkers by volume, top conversations by bytes, top ports by connection count; useful for capacity planning and anomaly baselining
- **Bidirectional flow records (IPFIX)** — IPFIX extends NetFlow with bidirectional flows (both directions captured in a single record) and extensible information elements for additional metadata
- **sFlow samples** — statistical packet samples (not all packets; typically 1 in N where N = sample rate) with partial packet header data; provides approximate traffic statistics at lower overhead than NetFlow on high-speed links
- **Application-layer metadata (enriched flow)** — when flow collection is combined with deep packet inspection (nDPI, Zeek), application protocol and application name are added to flow records (e.g., TLS, HTTP/2, BitTorrent, Kerberos)
- **Zeek (network metadata logs)** — Zeek produces structured log files from full packet inspection: conn.log (connection metadata), http.log (HTTP requests/responses), dns.log (DNS queries), ssl.log (TLS handshake details), files.log (file transfers), x509.log (certificate details), dpd.log (protocol detection anomalies)

### Security Events to Look For

- **East-west lateral movement** — unusual internal-to-internal traffic flows; a workstation communicating directly with another workstation, especially on administrative ports (TCP/445 SMB, TCP/135 WMI, TCP/3389 RDP, TCP/5985 WinRM); network flows that cross subnet boundaries where inter-subnet traffic is normally minimal
- **Data exfiltration by volume** — a single internal host transferring a significantly higher-than-baseline volume of data to an external destination in a short time window; particularly if the destination is not a recognized CDN, cloud provider endpoint, or business-related SaaS service
- **Port scanning / network reconnaissance** — a single source IP making short-duration connections (often 0 bytes transferred, SYN only or SYN+RST) to many destination IPs on the same port, or to many ports on the same destination IP; look for flows with zero byte counts and high connection counts
- **Beaconing patterns in flow data** — a host making connections to the same external IP at regular intervals; flow data beaconing analysis requires looking at connection timing regularity, consistent byte counts, and consistent port; can indicate C2 even when the payload is encrypted
- **New communication paths to critical assets** — a host that has never previously communicated with a database server suddenly initiating a TCP connection to port 5432 (PostgreSQL) or 1433 (MSSQL); lateral movement and privilege escalation often show up as new internal communication paths
- **Protocol anomalies** — HTTP or HTTPS traffic on non-standard ports (port 80 traffic to a non-web server, HTTPS on port 8443 to an unusual server); DNS traffic on a port other than UDP/53; SSH traffic on a port other than TCP/22; these indicate either misconfiguration or deliberate protocol obfuscation
- **Non-standard or unusual outbound services** — outbound connections on IRC ports (6667, 6697), Telnet (23), old P2P protocols; any of these from a corporate workstation to the internet indicate policy violations at minimum and possible malware
- **Large numbers of connections to a single external IP** — high connection count to a single external IP from many internal hosts may indicate a DDoS amplification attack, a botnet C2 server, or a widespread phishing campaign delivery infrastructure
- **Asymmetric flow ratios** — large outbound byte counts compared to inbound bytes; for most user traffic, inbound (downloads) is much larger than outbound (uploads); a reversed ratio for a significant volume of traffic indicates data exfiltration
- **Unusual use of ICMP** — large ICMP packets (> 1500 bytes), high-frequency ICMP traffic, ICMP type 8 (echo request) to many destinations; may indicate ICMP tunneling (used by tools like icmpsh, ptunnel) or network mapping

### SIEM Onboarding Steps

1. **Enable NetFlow/IPFIX export on all network devices.** On Cisco IOS/IOS-XE routers and switches: configure flexible NetFlow with a flow record, flow exporter (pointing to the SIEM or a flow collector), and flow monitor. Apply the flow monitor to each interface in both input and output directions. On Juniper: configure cflowd or JFlow. On Palo Alto: enable NetFlow via Device > Server Profiles > NetFlow.
2. **Deploy a dedicated flow collector if needed.** For high-volume environments, a dedicated flow collector (nProbe, ntopng, Elastic Flow, or a hardware appliance) should receive NetFlow from all network devices and then forward processed/normalized flow data to the SIEM. This reduces the load on the SIEM and allows for flow enrichment (GeoIP, threat intel, application identification) at the collection layer.
3. **Configure sampling rates appropriately.** For high-speed interfaces (10 Gbps+), configure a sampling rate (e.g., 1 in 1000) to reduce volume to a manageable level. For security monitoring, prefer lower sampling rates (1 in 100 or no sampling) on critical segments (DMZ, server farms). Document the sampling rates so that byte counts can be correctly interpreted.
4. **Configure SIEM NetFlow input.** Most SIEMs support UDP input for NetFlow (port 2055, 9996) or IPFIX (port 4739). Configure the SIEM to listen on the appropriate port and apply the NetFlow/IPFIX decoder. For Splunk, use the Splunk Stream or Splunk NetFlow add-on. For Elastic, use the Elastic Flow input (Packetbeat or the Elastic Agent Network Packet Monitor).
5. **Deploy Zeek for deep packet metadata (recommended for high-security environments).** Zeek runs on a dedicated server receiving a network tap or SPAN port that mirrors traffic. Zeek produces structured JSON or TSV log files for each protocol. Deploy Filebeat with the Zeek module to forward Zeek logs to the SIEM. Zeek provides significantly richer metadata than pure flow data (HTTP headers, TLS certificate details, DNS content, file hashes from network transfers).
6. **Normalize flow fields in the SIEM.** Map: src_ip, dst_ip, src_port, dst_port, protocol (TCP/UDP/ICMP), bytes_in, bytes_out, packets_in, packets_out, duration, tcp_flags, start_time, end_time, input_interface, output_interface. Create derived fields: connection_rate (connections per minute per source), bytes_ratio (out/in), flow_direction (internal-to-external, internal-to-internal, external-to-internal).
7. **Integrate GeoIP enrichment.** Enrich src_ip and dst_ip with GeoIP data (country, ASN, organization name) at ingest or query time. Create separate fields for src_country and dst_country. This enables geographic-based detection rules.
8. **Build traffic baselines by source IP and asset type.** For each internal IP (or subnet), establish a rolling 30-day baseline of: average daily bytes transferred, typical external destination countries, typical port usage, typical connection count per hour. Use these baselines for anomaly detection alerts rather than static thresholds.
9. **Integrate with asset inventory.** Map IP addresses to asset records (hostname, owner, business unit, criticality) so that flow-based alerts include device context. Build a lookup table that maps IP ranges to network segments (DMZ, server VLAN, workstation VLAN, IoT network).
10. **Configure top-N alert for large transfers.** Set up a scheduled search (running every 15 minutes) that identifies the top 10 source IPs by outbound bytes transferred in the last 60 minutes. Alert when any single internal IP exceeds a threshold (e.g., 1 GB outbound in 60 minutes to a single external destination) or when the top talker list includes an IP from a critical server segment.

---

## Log Source Coverage Matrix

| Log Source | Detection Value | Compliance Coverage (CIS Controls) | Typical Onboarding Effort | Priority Tier |
|---|---|---|---|---|
| Firewall Logs | High | CIS 12, 13 | Medium (2-5 days) | Tier 1 — Required |
| VPN Logs | High | CIS 12, 6 | Medium (2-3 days) | Tier 1 — Required |
| Active Directory / LDAP | High | CIS 4, 5, 6 | High (3-7 days) | Tier 1 — Required |
| Endpoint (Windows/Linux/Mac) | High | CIS 2, 4, 8, 10 | High (5-10 days) | Tier 1 — Required |
| Email (Exchange/M365/Google) | High | CIS 7, 9 | Medium (2-5 days) | Tier 1 — Required |
| Antivirus / EDR | High | CIS 10 | Low-Medium (1-3 days) | Tier 1 — Required |
| Cloud Services — AWS | High | CIS 1, 4, 5, 12, 16 | High (3-7 days) | Tier 1 (if AWS used) |
| Cloud Services — Microsoft Azure | High | CIS 1, 4, 5, 6, 12 | High (3-7 days) | Tier 1 (if Azure used) |
| Cloud Services — GCP | High | CIS 1, 4, 5, 12, 16 | High (3-7 days) | Tier 1 (if GCP used) |
| Cloud Services — Microsoft 365 | High | CIS 4, 9, 13 | Medium (2-5 days) | Tier 1 (if M365 used) |
| DNS Logs | High | CIS 9, 12 | Medium (2-4 days) | Tier 1 — Required |
| DHCP Logs | Medium | CIS 1, 12 | Low (1-2 days) | Tier 2 — Recommended |
| Web Proxy / SWG | High | CIS 9, 12, 13 | Medium (2-4 days) | Tier 1 — Required |
| Network Flow / NetFlow / IPFIX | Medium-High | CIS 12, 13 | Medium-High (3-5 days) | Tier 2 — Recommended |

**Tier Definitions:**
- **Tier 1 — Required:** Essential for baseline detection capability. A SIEM without these sources has significant detection gaps.
- **Tier 2 — Recommended:** Substantially enhances detection depth. Should be onboarded after all Tier 1 sources.
- **Tier 3 — Enhanced (not in this list):** Niche sources that add specific detection capability (e.g., ICS/OT logs, badge access logs, application-specific logs).

---

## Quick Reference: Security Events by MITRE ATT&CK Tactic

| MITRE ATT&CK Tactic | Key Techniques | Best Log Sources | What to Look For |
|---|---|---|---|
| **Initial Access** (TA0001) | Phishing (T1566), Valid Accounts (T1078), External Remote Services (T1133), Exploit Public-Facing Application (T1190) | Email, VPN, Firewall, Web Proxy | Phishing email delivery, credential-based VPN access from new locations, inbound exploitation attempts on public services, web shell activity |
| **Execution** (TA0002) | PowerShell (T1059.001), WMI (T1047), Scheduled Task (T1053), Command and Scripting Interpreter (T1059) | Endpoint (Sysmon), Active Directory, EDR | Encoded/obfuscated PowerShell, WmiPrvSE spawning child processes, schtasks.exe with /create, cmd.exe or script interpreters spawned by unusual parents |
| **Persistence** (TA0003) | Registry Run Keys (T1547.001), Scheduled Task (T1053), Create Account (T1136), Boot/Logon Autostart (T1547) | Endpoint (Sysmon), Active Directory, DNS | Registry run key writes, new scheduled task creation, new user account creation outside change windows, new DNS records for callback domains |
| **Privilege Escalation** (TA0004) | Abuse Elevation Control Mechanism (T1548), Valid Accounts (T1078), Domain Policy Modification (T1484) | Active Directory, Endpoint, Cloud IAM | User added to admin groups, privileged token usage, domain policy changes, cloud IAM role escalation, sudo to root on Linux |
| **Defense Evasion** (TA0005) | Indicator Removal (T1070), Masquerading (T1036), Disable or Modify Tools (T1562), Process Injection (T1055) | Endpoint (Sysmon), Active Directory, EDR, AV/EDR | Audit log cleared (Event 1102/104), AV/EDR agent disabled, process injection (CreateRemoteThread), renamed system binaries, timestomping |
| **Credential Access** (TA0006) | OS Credential Dumping (T1003), Kerberoasting (T1558.003), Brute Force (T1110), Network Sniffing (T1040) | Active Directory, Endpoint (Sysmon), VPN, DNS | LSASS access events, high volume TGS requests (4769), authentication failure spikes, NTLM downgrade indicators, credential reuse patterns |
| **Discovery** (TA0007) | Network Scanning (T1046), Account Discovery (T1087), Permission Groups Discovery (T1069), System Information Discovery (T1082) | Endpoint, DNS, NetFlow, Active Directory | Net.exe / nltest.exe execution, LDAP queries to enumerate AD groups, port scan patterns in flow data, high NXDOMAIN rates, DNS PTR record queries |
| **Lateral Movement** (TA0008) | Remote Services (T1021), SMB/Windows Admin Shares (T1021.002), Pass-the-Hash (T1550.002), WMI (T1047) | Active Directory, Endpoint, NetFlow, Firewall | Network logons (Type 3) spreading across hosts, PSEXESVC service creation, WMI remote execution, Pass-the-Hash indicators in NTLM auth logs, new east-west flows on administrative ports |
| **Collection** (TA0009) | Data from Local System (T1005), Email Collection (T1114), Clipboard Data (T1115), Screen Capture (T1113) | Endpoint, Email, Web Proxy, Cloud (M365/SharePoint) | Bulk file access events, inbox rule changes, auto-forwarding rules, mass download from SharePoint/OneDrive, unusual access to file shares |
| **Exfiltration** (TA0010) | Exfiltration Over Web Service (T1567), Exfiltration Over C2 Channel (T1041), Exfiltration Over Alternative Protocol (T1048), Data Transfer Size Limits (T1030) | NetFlow, Web Proxy, Firewall, DNS, Cloud | Large outbound transfers on firewall/NetFlow, high upload volume on web proxy, DNS tunneling indicators, unusual cloud API data access, data staged in cloud storage for exfiltration |
| **Command and Control** (TA0011) | Application Layer Protocol (T1071), DNS (T1071.004), Encrypted Channel (T1573), Web Service (T1102), Ingress Tool Transfer (T1105) | DNS, Web Proxy, Firewall, NetFlow | Beaconing patterns (regular periodic connections), DGA domains, DNS tunneling (high-entropy subdomains, TXT queries), C2 over HTTPS (JA3 fingerprints), connection to known C2 infrastructure |

---

*This document is a living reference. Update the onboarding steps as vendor products release new versions, and update the security events list as new attack techniques emerge. Cross-reference with the detection use case library for the corresponding detection rules for each log source.*
