# SIEM Health Check Checklist
**Client:** [Client Name]
**Platform:** [SIEM Platform]
**Check Date:** [Check Date]
**Performed By:** [Analyst Name / Consultant Name]
**Check Type:** [ ] Monthly (Critical Items Only) | [ ] Quarterly (Full Review)

---

## How to Use This Checklist

This checklist is designed to be completed on a regular schedule to ensure the SIEM platform remains healthy, log sources are operating correctly, and detection rules are functioning as expected.

**Recommended Check Frequency:**

| Check Type | Frequency | Audience | Time Required |
|---|---|---|---|
| Critical items only (Sections 1 and 3) | Monthly | Security analyst or SIEM administrator | 30–60 minutes |
| Full health check (all sections) | Quarterly | Security lead + SIEM administrator | 2–4 hours |
| Log ingestion spot-check | Weekly (automated where possible) | Automated alert or on-call analyst | 10–15 minutes |
| Annual full audit (including access review and DR test) | Annually | Security lead + IT lead | 4–8 hours |

**How to Complete:**
1. Work through each section in order, checking each item against the current state of the SIEM
2. Mark each item as Pass, Fail, or N/A
3. For any Fail, document the issue in the Notes column and add it to the Recommended Actions table in Section 8
4. Complete the Health Score in Section 8 and record the overall status
5. Distribute the completed checklist to [Client Security Lead] and [Consulting Point of Contact]

---

## Health Check Summary Dashboard

Complete this table last, after all sections are reviewed. Use it as the at-a-glance status for leadership reporting.

| Area | Status | Last Checked | Issues Found | Priority of Issues |
|---|---|---|---|---|
| 1. Log Ingestion Health | [ ] Green / [ ] Yellow / [ ] Red | [Date] | [# issues] | [ ] Critical / [ ] High / [ ] Medium / [ ] None |
| 2. Parser and Normalization Accuracy | [ ] Green / [ ] Yellow / [ ] Red | [Date] | [# issues] | [ ] Critical / [ ] High / [ ] Medium / [ ] None |
| 3. Alert Health | [ ] Green / [ ] Yellow / [ ] Red | [Date] | [# issues] | [ ] Critical / [ ] High / [ ] Medium / [ ] None |
| 4. Storage, Retention, and Performance | [ ] Green / [ ] Yellow / [ ] Red | [Date] | [# issues] | [ ] Critical / [ ] High / [ ] Medium / [ ] None |
| 5. User Access and Security | [ ] Green / [ ] Yellow / [ ] Red | [Date] | [# issues] | [ ] Critical / [ ] High / [ ] Medium / [ ] None |
| 6. Backup and Redundancy | [ ] Green / [ ] Yellow / [ ] Red | [Date] | [# issues] | [ ] Critical / [ ] High / [ ] Medium / [ ] None |
| 7. Threat Intelligence Integration | [ ] Green / [ ] Yellow / [ ] Red | [Date] | [# issues] | [ ] Critical / [ ] High / [ ] Medium / [ ] None |
| **Overall** | [ ] Green / [ ] Yellow / [ ] Red | [Date] | **[Total issues]** | |

**Overall Health Score:** [  ] / 80
**Status:** [ ] Green (64–80) | [ ] Yellow (40–63) | [ ] Red (0–39)

---

## Section 1: Log Ingestion Health

**Section Score: [  ] / 10**

### 1.1 Per Log Source Status Table

Review each connected log source. Compare actual event volume for the last 24 hours against the expected baseline established during onboarding.

| Source | Expected Volume | Actual Volume (Last 24h) | Status | Last Successful Event | Notes |
|---|---|---|---|---|---|
| [Log Source 1] | [X GB/day or X EPS] | [Actual volume] | [ ] Pass / [ ] Fail / [ ] Warning | [Timestamp] | |
| [Log Source 2] | | | [ ] Pass / [ ] Fail / [ ] Warning | | |
| [Log Source 3] | | | [ ] Pass / [ ] Fail / [ ] Warning | | |
| [Log Source 4] | | | [ ] Pass / [ ] Fail / [ ] Warning | | |
| [Log Source 5] | | | [ ] Pass / [ ] Fail / [ ] Warning | | |
| [Log Source 6] | | | [ ] Pass / [ ] Fail / [ ] Warning | | |
| [Log Source 7] | | | [ ] Pass / [ ] Fail / [ ] Warning | | |
| [Log Source 8] | | | [ ] Pass / [ ] Fail / [ ] Warning | | |
| [Log Source 9] | | | [ ] Pass / [ ] Fail / [ ] Warning | | |
| [Log Source 10] | | | [ ] Pass / [ ] Fail / [ ] Warning | | |

**Volume deviation thresholds:**
- **Warning:** Actual volume < 75% or > 200% of expected baseline
- **Fail:** Actual volume = 0 events in last 24 hours (complete loss of source)

### 1.2 Log Ingestion Checks

| # | Check | Result | Notes |
|---|---|---|---|
| 1.1 | Are any log sources showing 0 events in the last 24 hours? | [ ] Pass / [ ] Fail | [List sources with 0 events] |
| 1.2 | Are any log sources showing volume significantly below baseline (< 75%)? | [ ] Pass / [ ] Warning | [List sources below threshold] |
| 1.3 | Are any log sources showing volume significantly above baseline (> 200%)? | [ ] Pass / [ ] Warning | [List sources above threshold] |
| 1.4 | Are there any duplicate events detected (same event ingested multiple times)? | [ ] Pass / [ ] Fail | [Document duplication pattern if present] |
| 1.5 | Are there any log source connectivity errors visible in the SIEM management console? | [ ] Pass / [ ] Fail | [List error messages] |
| 1.6 | Have any TLS certificates on log forwarding sources expired or will they expire within 30 days? | [ ] Pass / [ ] Fail | [List affected sources and cert expiry dates] |
| 1.7 | Are any syslog listeners on the SIEM collector showing error states? | [ ] Pass / [ ] Fail | [List listener issues] |
| 1.8 | Are cloud connector API credentials (API keys, OAuth tokens) still valid and not approaching expiry? | [ ] Pass / [ ] Warning | [List any expiring credentials] |
| 1.9 | Have any new systems been added to the environment that should be sending logs but are not yet connected? | [ ] Pass / [ ] Warning | [List new uncovered systems] |
| 1.10 | Is total ingestion volume within the platform's licensed quota? | [ ] Pass / [ ] Warning | [Current usage vs. quota] |

**Section 1 Issues Summary:** [Document all failed or warning items]

---

## Section 2: Parser and Normalization Accuracy

**Section Score: [  ] / 10**

### 2.1 Random Sample Review Process

For each major log source type, retrieve 10 random events from the last 24 hours and manually inspect them. This spot-check validates that parsers are correctly extracting fields and that log format changes have not broken parsing.

**How to retrieve samples:**
- Splunk: `index=[source_index] | head 10 | table _time, src_ip, dest_ip, user, action, _raw`
- Sentinel: Use Log Analytics workspace query, retrieve 10 random events per table
- InsightIDR: Use the Investigation query builder for each log source
- Elastic: Use Kibana Discover, filter by data stream/index pattern

| Log Source | Sample Count Reviewed | Key Fields Present | Timestamp Correct | Parsing Errors Found | Parser Version | Notes |
|---|---|---|---|---|---|---|
| [Log Source 1] | 10 | [ ] Yes / [ ] No | [ ] Yes / [ ] No | [ ] None / [ ] Found | [Version] | |
| [Log Source 2] | 10 | [ ] Yes / [ ] No | [ ] Yes / [ ] No | [ ] None / [ ] Found | [Version] | |
| [Log Source 3] | 10 | [ ] Yes / [ ] No | [ ] Yes / [ ] No | [ ] None / [ ] Found | [Version] | |
| [Log Source 4] | 10 | [ ] Yes / [ ] No | [ ] Yes / [ ] No | [ ] None / [ ] Found | [Version] | |
| [Log Source 5] | 10 | [ ] Yes / [ ] No | [ ] Yes / [ ] No | [ ] None / [ ] Found | [Version] | |

### 2.2 Field Extraction Validation

For each source type, confirm the following key fields are correctly populated on the majority (> 90%) of events:

| # | Check | Result | Notes |
|---|---|---|---|
| 2.1 | Source IP address (src_ip / source.ip) correctly extracted on network log sources | [ ] Pass / [ ] Fail | |
| 2.2 | Destination IP address (dest_ip / destination.ip) correctly extracted | [ ] Pass / [ ] Fail | |
| 2.3 | Username / user field correctly extracted on authentication log sources | [ ] Pass / [ ] Fail | |
| 2.4 | Timestamp correctly parsed — events showing accurate event time (not ingest time) | [ ] Pass / [ ] Fail | |
| 2.5 | Event type / action field correctly extracted (allow/deny, success/failure, login/logout) | [ ] Pass / [ ] Fail | |
| 2.6 | Hostname correctly extracted on endpoint and server logs | [ ] Pass / [ ] Fail | |
| 2.7 | Severity or criticality fields correctly extracted on alert-type sources (EDR, IDS) | [ ] Pass / [ ] Fail / [ ] N/A | |
| 2.8 | All timestamps are in UTC or correctly converted per platform timezone setting | [ ] Pass / [ ] Fail | |

### 2.3 Parser Currency Check

| # | Check | Result | Notes |
|---|---|---|---|
| 2.9 | Are any vendor-provided parsers running on outdated versions (check SIEM vendor parser release notes)? | [ ] Pass / [ ] Warning | [List outdated parsers and available versions] |
| 2.10 | Have any monitored vendor products (firewalls, EDR, cloud services) released software updates that may have changed log formats? | [ ] Pass / [ ] Warning | [List any format change notifications] |
| 2.11 | Are there any events appearing in the "unparsed" or "unknown" source category? | [ ] Pass / [ ] Fail | [Document volume and source of unparsed events] |

**Section 2 Issues Summary:** [Document all failed or warning items]

---

## Section 3: Alert Health

**Section Score: [  ] / 10**

### 3.1 Rule Count and Status Check

| # | Check | Result | Notes |
|---|---|---|---|
| 3.1 | Total active detection rules currently enabled | [Count] | Expected: [X] rules |
| 3.2 | Are the number of active rules at or above the expected count established at go-live? | [ ] Pass / [ ] Fail | [Note any rules missing vs. baseline] |
| 3.3 | Are there any rules that have been disabled since the last health check without documentation? | [ ] Pass / [ ] Fail | [List undocumented disabled rules] |
| 3.4 | Are there any rules that have been modified since the last health check without a change record? | [ ] Pass / [ ] Fail | [List unauthorized modifications] |

### 3.2 Alert Firing Rate Table

Review the alert firing rate for each key detection rule over the last 7 days. Flag rules firing at 0 (potential data gap) or firing at a rate significantly above expected (tuning needed).

| Rule Name | Expected Fire Rate | Actual Fire Rate (Last 7 Days) | Status | Action Needed |
|---|---|---|---|---|
| Brute Force — Multiple Failed Logins | [X/week] | [Actual] | [ ] Normal / [ ] Investigate / [ ] Tune | |
| Successful Login After Multiple Failures | [X/week] | [Actual] | [ ] Normal / [ ] Investigate / [ ] Tune | |
| Impossible Travel Login | [X/week] | [Actual] | [ ] Normal / [ ] Investigate / [ ] Tune | |
| Privileged Account Use After Hours | [X/week] | [Actual] | [ ] Normal / [ ] Investigate / [ ] Tune | |
| New Admin Account Created | [X/week] | [Actual] | [ ] Normal / [ ] Investigate / [ ] Tune | |
| Mass File Deletion / Encryption Activity | [X/week] | [Actual] | [ ] Normal / [ ] Investigate / [ ] Tune | |
| Known Malware Hash Execution | [X/week] | [Actual] | [ ] Normal / [ ] Investigate / [ ] Tune | |
| Outbound Connection to Known Malicious IP | [X/week] | [Actual] | [ ] Normal / [ ] Investigate / [ ] Tune | |
| DNS Query to Suspicious Domain | [X/week] | [Actual] | [ ] Normal / [ ] Investigate / [ ] Tune | |
| Large Outbound Data Transfer | [X/week] | [Actual] | [ ] Normal / [ ] Investigate / [ ] Tune | |
| [Custom Rule 1] | | | | |
| [Custom Rule 2] | | | | |
| [Custom Rule 3] | | | | |

**Zero-Firing Rules:** Any rule that fires 0 times in a 7-day window is either correctly tuned (low-frequency event) or indicates a log source problem. For each zero-firing rule, confirm the required log source is active and generating events before concluding the rule is simply not triggered.

### 3.3 Alert Routing and Escalation Checks

| # | Check | Result | Notes |
|---|---|---|---|
| 3.5 | Test alert routed to [Client Security Lead email] — confirm receipt | [ ] Pass / [ ] Fail | [Send test alert and confirm] |
| 3.6 | Ticketing integration functional — test alert creates ticket in [ServiceNow / Jira] | [ ] Pass / [ ] Fail / [ ] N/A | |
| 3.7 | On-call escalation path functional for Critical alerts (PagerDuty / OpsGenie / SMS) | [ ] Pass / [ ] Fail / [ ] N/A | |
| 3.8 | SOAR playbook triggers functional — test trigger executes expected automation | [ ] Pass / [ ] Fail / [ ] N/A | |
| 3.9 | Alert queue size: open unreviewed alerts older than [X hours] at time of check | [Count] | Target: 0 alerts older than [SLA threshold] |
| 3.10 | Are suppression rules and allowlists still appropriate, or do any need to be removed? | [ ] Pass / [ ] Review | [List any allowlist entries due for review] |

**Section 3 Issues Summary:** [Document all failed or warning items]

---

## Section 4: Storage, Retention, and Performance

**Section Score: [  ] / 10**

### 4.1 Storage Utilization

| # | Check | Result | Notes |
|---|---|---|---|
| 4.1 | Current storage utilization: [  ]% of total allocated capacity | [ ] Pass / [ ] Warning / [ ] Fail | Green < 70% / Yellow 70–85% / Red > 85% |
| 4.2 | Storage growth rate: at current growth rate, storage will be exhausted in approximately [  ] months | [ ] Pass / [ ] Warning | Warning if < 6 months remaining |
| 4.3 | Hot storage (searchable/recent) utilization: [  ]% | [ ] Pass / [ ] Warning | |
| 4.4 | Warm/cold storage (archive) utilization: [  ]% | [ ] Pass / [ ] Warning / [ ] N/A | |

### 4.2 Retention Policy Validation

| Log Source Type | Required Retention | Configured Retention | Status |
|---|---|---|---|
| Authentication logs (AD, IAM) | [X months — per compliance requirement] | [Configured] | [ ] Pass / [ ] Fail |
| Firewall logs | [X months] | [Configured] | [ ] Pass / [ ] Fail |
| Endpoint / EDR logs | [X months] | [Configured] | [ ] Pass / [ ] Fail |
| Email gateway logs | [X months] | [Configured] | [ ] Pass / [ ] Fail |
| Cloud service logs | [X months] | [Configured] | [ ] Pass / [ ] Fail |
| Application logs | [X months] | [Configured] | [ ] Pass / [ ] Fail |
| SIEM audit/admin logs | [X months] | [Configured] | [ ] Pass / [ ] Fail |

### 4.3 Performance Checks

| # | Check | Result | Notes |
|---|---|---|---|
| 4.5 | Common search / query: [Standard detection search] completes within acceptable time (< [X seconds]) | [ ] Pass / [ ] Warning | [Record actual execution time] |
| 4.6 | Dashboard load time for primary SOC dashboard: < [X seconds] | [ ] Pass / [ ] Warning | [Record actual load time] |
| 4.7 | No searches or queries currently stuck / running for > [X minutes] in the search queue | [ ] Pass / [ ] Warning | [List stuck searches if present] |
| 4.8 | SIEM platform CPU and memory utilization within acceptable bounds (per vendor guidance) | [ ] Pass / [ ] Warning / [ ] N/A | [Check if on-prem; N/A for most SaaS platforms] |

### 4.4 License and Quota Checks

| # | Check | Result | Notes |
|---|---|---|---|
| 4.9 | Current daily ingestion vs. licensed quota: [  ] GB/day used of [  ] GB/day licensed ([  ]%) | [ ] Pass / [ ] Warning / [ ] Fail | Warning > 80%; Fail > 95% |
| 4.10 | License expiration date: [Date] — more than 90 days remaining? | [ ] Pass / [ ] Warning | Warning if < 90 days; Fail if < 30 days |
| 4.11 | For user-based platforms (InsightIDR): current asset/user count vs. licensed count | [ ] Pass / [ ] Warning / [ ] N/A | |

**Section 4 Issues Summary:** [Document all failed or warning items]

---

## Section 5: User Access and Security

**Section Score: [  ] / 10**

### 5.1 Active User Account Review

| # | Check | Result | Notes |
|---|---|---|---|
| 5.1 | Total active user accounts in SIEM: [Count] | [Number] | Compare to expected count from access matrix |
| 5.2 | Are there any user accounts that have not logged in within the last 90 days? | [ ] Pass / [ ] Fail | [List stale accounts] |
| 5.3 | Have any users left the organization whose SIEM accounts have not been deprovisioned? | [ ] Pass / [ ] Fail | [Cross-reference HR offboarding list] |
| 5.4 | Are there any accounts created since the last health check that are not in the access matrix? | [ ] Pass / [ ] Fail | [List undocumented accounts] |

### 5.2 Privileged Access Review

| # | Check | Result | Notes |
|---|---|---|---|
| 5.5 | Who currently holds SIEM Admin role? | [List users] | Is this appropriate and matches the access matrix? |
| 5.6 | Are there any users with Admin role who should be demoted to a lower-privilege role? | [ ] Pass / [ ] Fail | [List any inappropriate admin accounts] |
| 5.7 | Is the number of Admin accounts minimized (principle of least privilege)? | [ ] Pass / [ ] Warning | Best practice: < 3 admin accounts for most environments |
| 5.8 | Are shared / generic admin accounts in use? | [ ] Pass / [ ] Fail | Fail: shared accounts should not be used; all access must be individual |

### 5.3 API Key and Service Account Audit

| # | Check | Result | Notes |
|---|---|---|---|
| 5.9 | List all API keys / service accounts currently active in the SIEM | [List] | Are all accounted for in the service account register? |
| 5.10 | Are any API keys approaching expiry (within 30 days)? | [ ] Pass / [ ] Warning | [List expiring keys with expiry dates] |
| 5.11 | Are any API keys / service accounts in use for integrations that are no longer active? | [ ] Pass / [ ] Fail | [List orphaned service accounts] |
| 5.12 | Are service account credentials stored securely (secrets manager, vault — NOT in plaintext config files)? | [ ] Pass / [ ] Fail | |

### 5.4 MFA and Authentication Controls

| # | Check | Result | Notes |
|---|---|---|---|
| 5.13 | MFA is enforced for all SIEM user accounts | [ ] Pass / [ ] Fail | [List any accounts without MFA] |
| 5.14 | SSO / SAML integration active and functioning (if configured) | [ ] Pass / [ ] Fail / [ ] N/A | |
| 5.15 | SIEM login from untrusted networks is restricted (IP allowlist, VPN required, zero trust) | [ ] Pass / [ ] Warning / [ ] N/A | |

### 5.5 SIEM Administrative Audit Log Review

| # | Check | Result | Notes |
|---|---|---|---|
| 5.16 | Review SIEM administrative audit log for the past review period — any unexpected admin actions? | [ ] Pass / [ ] Fail | [List unexpected actions: rule modifications, user additions, config changes] |
| 5.17 | Are SIEM admin audit logs being retained for the required period? | [ ] Pass / [ ] Fail | |
| 5.18 | Are SIEM admin actions logged to a separate, read-only audit trail that is itself monitored? | [ ] Pass / [ ] Warning | |

**Section 5 Issues Summary:** [Document all failed or warning items]

---

## Section 6: Backup and Redundancy

**Section Score: [  ] / 10**

### 6.1 Log Backup Status

| # | Check | Result | Notes |
|---|---|---|---|
| 6.1 | Last successful backup completion date and time | [Date/Time] | Within expected schedule? |
| 6.2 | Have any backup jobs failed since the last health check? | [ ] Pass / [ ] Fail | [List failed backup jobs with error messages] |
| 6.3 | Backup destination storage utilization: [  ]% | [ ] Pass / [ ] Warning | Warning > 80% |
| 6.4 | Backup encryption is configured and encryption keys are accessible | [ ] Pass / [ ] Fail | |
| 6.5 | Are backups stored off-site or in a separate cloud region/account? | [ ] Pass / [ ] Fail | Best practice: 3-2-1 backup rule |

### 6.2 Backup Restoration Testing

| # | Check | Result | Notes |
|---|---|---|---|
| 6.6 | Date of last successful backup restoration test | [Date] | Should be performed at least annually; quarterly is better |
| 6.7 | Result of last restoration test | [ ] Pass / [ ] Fail / [ ] Not Yet Performed | [Document restoration test outcome] |
| 6.8 | Restoration test documented and stored in the DR documentation? | [ ] Pass / [ ] Fail / [ ] N/A | |

### 6.3 High Availability Status

| # | Check | Result | Notes |
|---|---|---|---|
| 6.9 | High availability configuration: is HA configured for this SIEM deployment? | [ ] Yes / [ ] No / [ ] N/A (SaaS) | |
| 6.10 | If HA configured: are all HA nodes healthy and synchronized? | [ ] Pass / [ ] Fail / [ ] N/A | |
| 6.11 | If HA configured: when was last HA failover test performed? | [Date or Never] | |

### 6.4 Disaster Recovery Documentation

| # | Check | Result | Notes |
|---|---|---|---|
| 6.12 | SIEM disaster recovery runbook exists and is current | [ ] Pass / [ ] Fail | Last updated: [Date] |
| 6.13 | Recovery Time Objective (RTO) and Recovery Point Objective (RPO) are documented and achievable with current backup schedule | [ ] Pass / [ ] Fail | RTO: [X hours] / RPO: [X hours] |
| 6.14 | DR contacts and escalation path are documented and current | [ ] Pass / [ ] Fail | |

**Section 6 Issues Summary:** [Document all failed or warning items]

---

## Section 7: Threat Intelligence Integration

**Section Score: [  ] / 10**

### 7.1 TI Feed Connectivity and Currency

| TI Feed | Feed Source | Last Successful Update | Update Frequency | Status | Notes |
|---|---|---|---|---|---|
| [TI Feed 1] | [Vendor / TAXII / STIX] | [Timestamp] | [Hourly / Daily / Weekly] | [ ] Pass / [ ] Fail | |
| [TI Feed 2] | | | | [ ] Pass / [ ] Fail | |
| [TI Feed 3] | | | | [ ] Pass / [ ] Fail | |
| [TI Feed 4] | | | | [ ] Pass / [ ] Fail | |
| [TI Feed 5] | | | | [ ] Pass / [ ] Fail | |

### 7.2 TI Integration Checks

| # | Check | Result | Notes |
|---|---|---|---|
| 7.1 | All configured TI feeds have updated within the expected schedule | [ ] Pass / [ ] Fail | [List any feeds that have not updated] |
| 7.2 | Total active IOCs (IPs, domains, hashes) in the TI database: [Count] | [Number] | Is this significantly different from last check? |
| 7.3 | TI feed API credentials are valid and not approaching expiry | [ ] Pass / [ ] Warning | [List any expiring credentials] |
| 7.4 | TI match rate: alerts generated from TI matches in the last 30 days | [Count] | Is this consistent with baseline expectations? 0 matches may indicate TI disconnected from detection engine |
| 7.5 | Are there any TI match alerts that have been generating excessively (TI noise causing alert fatigue)? | [ ] Pass / [ ] Warning | [List noisy TI indicators] |

### 7.3 Expired IOC Cleanup

| # | Check | Result | Notes |
|---|---|---|---|
| 7.6 | Expired IOCs are being automatically purged per the configured TTL (time-to-live) settings | [ ] Pass / [ ] Fail | |
| 7.7 | Manual review: any obviously stale or low-confidence IOCs that should be removed? | [ ] Pass / [ ] Review | [Document any found] |
| 7.8 | Any internal false-positive IOCs (legitimate internal IPs or domains) accidentally in the TI database? | [ ] Pass / [ ] Fail | [List any found — remove immediately] |

**Section 7 Issues Summary:** [Document all failed or warning items]

---

## Section 8: Overall Health Score

### 8.1 Scoring Rubric

Each section is scored from 0 to 10. Score each section based on the results of that section's checks:

| Score | Meaning |
|---|---|
| **10** | All checks pass; no issues found |
| **8–9** | Minor issues found; no critical failures; all warnings have documented remediation plans |
| **5–7** | One or more significant issues; at least one check failed; remediation in progress |
| **3–4** | Multiple failures; critical checks failed; remediation urgently needed |
| **0–2** | Severe failures; section is effectively non-functional; immediate escalation required |

### 8.2 Section Scores

| Section | Section Name | Score (0–10) | Status |
|---|---|---|---|
| 1 | Log Ingestion Health | [  ] | [ ] Green / [ ] Yellow / [ ] Red |
| 2 | Parser and Normalization Accuracy | [  ] | [ ] Green / [ ] Yellow / [ ] Red |
| 3 | Alert Health | [  ] | [ ] Green / [ ] Yellow / [ ] Red |
| 4 | Storage, Retention, and Performance | [  ] | [ ] Green / [ ] Yellow / [ ] Red |
| 5 | User Access and Security | [  ] | [ ] Green / [ ] Yellow / [ ] Red |
| 6 | Backup and Redundancy | [  ] | [ ] Green / [ ] Yellow / [ ] Red |
| 7 | Threat Intelligence Integration | [  ] | [ ] Green / [ ] Yellow / [ ] Red |
| **TOTAL** | | **[  ] / 70** | |

> **Note:** Total is out of 70 (7 sections x 10 points each). For the summary dashboard at the top of this document, convert to a score out of 80 by adding up to 10 points for overall health holistically.

### 8.3 Status Legend

| Status | Score Range | Meaning | Required Action |
|---|---|---|---|
| **Green** | 56–70 (80%+) | SIEM is operating within healthy parameters. Minor issues may exist but are non-critical. | Continue regular monitoring. Address any outstanding items in the next scheduled maintenance window. |
| **Yellow** | 35–55 (50–79%) | SIEM has notable issues that require attention. Detection capability may be degraded in some areas. | Schedule remediation within [14 days]. Escalate to security lead. Review failed items with client at next check-in. |
| **Red** | 0–34 (< 50%) | SIEM is experiencing significant failures. Detection coverage is materially compromised. | Initiate immediate remediation. Escalate to [Client Security Lead] and [Consulting Point of Contact]. Do not wait for scheduled review. |

### 8.4 Recommended Actions Table

Document all failed or warning items here with assigned owner and due date.

| # | Section | Issue Description | Severity | Recommended Action | Owner | Due Date | Status |
|---|---|---|---|---|---|---|---|
| 1 | [Section #] | [Issue description] | [ ] Critical / [ ] High / [ ] Medium / [ ] Low | [Specific remediation steps] | [Name] | [Date] | [ ] Open / [ ] In Progress / [ ] Resolved |
| 2 | | | | | | | |
| 3 | | | | | | | |
| 4 | | | | | | | |
| 5 | | | | | | | |
| 6 | | | | | | | |
| 7 | | | | | | | |
| 8 | | | | | | | |

### 8.5 Next Review Date

| Review Type | Scheduled Date | Assigned To |
|---|---|---|
| Next Monthly Critical Check | [Date] | [Analyst Name] |
| Next Quarterly Full Review | [Date] | [Security Lead + Consulting POC] |
| Next Annual Full Audit | [Date] | [Security Lead + IT Lead + Consulting] |

---

## Health Check Sign-Off

| Role | Name | Signature | Date |
|---|---|---|---|
| Performed By | [Analyst / Consultant] | _____________________________ | [Date] |
| Reviewed By | [Client Security Lead] | _____________________________ | [Date] |

**Certification:** I have reviewed the health check results above and confirm that all identified issues have been entered into the Recommended Actions table and assigned to an owner for remediation.

---

> **Document Control**
> Version: 1.0 | Template Owner: [Practice Lead] | Client: [Client Name]
> Completed copies of this checklist should be retained for at least 12 months as part of the client's security audit record.
