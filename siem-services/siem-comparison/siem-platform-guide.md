# SIEM Platform Guide
## Comparison, Selection, Positioning, and Expansion Playbook

> **Internal Use — Security Consulting Toolkit**
> Last Updated: 2026-03-13

---

## Table of Contents

1. [SIEM Platform Comparison](#section-1-siem-platform-comparison)
2. [SIEM Recommendation Guide by Client Profile](#section-2-siem-recommendation-guide-by-client-profile)
3. [How to Position Each Platform in Client Conversations](#section-3-how-to-position-each-platform-in-client-conversations)
4. [SIEM Expansion Conversation Guide](#section-4-siem-expansion-conversation-guide)

---

## Section 1: SIEM Platform Comparison

### 1.1 Platform Comparison Table

| Attribute | Splunk Enterprise Security | Microsoft Sentinel | IBM QRadar | Elastic SIEM (Elastic Security) | Rapid7 InsightIDR |
|---|---|---|---|---|---|
| **Deployment Model** | Cloud (Splunk Cloud), On-Prem, Hybrid | Cloud-native (Azure); hybrid via Arc | On-Prem, Cloud (QRadar on Cloud), SaaS (QRadar SIEM SaaS) | Cloud (Elastic Cloud), On-Prem, Hybrid | Cloud-native SaaS only |
| **Pricing Model** | GB/day ingestion (tiered); workload-based pricing available | Pay-as-you-go (GB/day) or Commitment Tiers; Microsoft 365 Defender benefit credits | EPS-based (Events Per Second); appliance or subscription license | GB/day ingestion on Elastic Cloud; self-managed = infrastructure cost only | User-based (per asset/user); predictable flat rate |
| **Best Fit Client Size** | Mid-Market to Enterprise | SMB (M365 shops) to Enterprise | Mid-Market to Enterprise (regulated industries) | SMB to Enterprise (cost-sensitive to large scale) | SMB to Mid-Market |
| **Primary Strengths** | - Unmatched search flexibility (SPL) - Massive app/integration ecosystem - Advanced correlation engine - Best-in-class custom dashboards - Strong professional community and documentation | - Native Azure / M365 / Defender integration - Near-zero infrastructure overhead - Competitive cost for Microsoft shops - Strong built-in analytics and ML - Rapid deployment for cloud-first orgs | - Strong compliance out-of-the-box (financial, gov) - Mature rule engine and offense management - Deep network visibility (QNI/QFlow) - Long-established vendor trust - Strong on-prem deployment story | - Extremely flexible and scalable - Low cost at self-managed scale - Excellent endpoint + SIEM in one platform - Strong ECS normalization - Active open-source community | - Fast time to value (days, not months) - Built-in UEBA (User & Entity Behavior Analytics) - Included threat intelligence (Rapid7 TI) - Guided detection out-of-the-box - Predictable pricing reduces budget surprises |
| **Primary Weaknesses** | - Very high cost at scale - Requires dedicated Splunk expertise - Complex to tune and maintain without experience - Pricing can escalate unpredictably with log growth - Heavy professional services dependency | - Azure-only cloud; limited on-prem story - Cost can rise sharply for non-Microsoft log sources - Requires Azure familiarity - Some features require premium SKUs - Less flexible for non-Microsoft environments | - Aging UI relative to modern competitors - Complex licensing model - Slower innovation cycle - High professional services cost - Cloud offering lags competitors | - Self-managed deployments require strong ops team - Elastic Security as SIEM is less mature than core search - Alert management less polished than Splunk ES - Vendor support can be inconsistent - Compliance reporting requires customization | - Limited customization vs. Splunk - SaaS-only limits deployment flexibility - Less suited for very large enterprises with complex needs - Smaller ecosystem than Splunk or Microsoft - Custom detection development less powerful |
| **CIS Controls Alignment** | Strong: CIS 1, 2, 6, 8, 10, 13, 17, 19 | Strong: CIS 1, 2, 3, 6, 12, 16, 17 (especially with M365 E5) | Strong: CIS 6, 8, 12, 13, 16, 17, 18 | Strong: CIS 1, 2, 6, 8, 13, 16 | Strong: CIS 6, 8, 10, 13, 16, 17 |
| **Time to Value** | 3-6 months (complex environments) | 2-4 weeks (M365 shops); 4-8 weeks (broader) | 2-4 months | 2-6 weeks (cloud); 2-4 months (self-managed) | 1-4 weeks |
| **Typical Total Cost Indicator** | Very High | Medium (M365 shops); High (broad ingestion) | High | Low-Medium (self-managed); Medium (Cloud) | Medium |
| **Native Integrations Highlight** | 2,500+ apps (Splunkbase); AWS, Azure, GCP, Okta, CrowdStrike, ServiceNow, Palo Alto | M365 Defender suite, Azure AD, Azure Sentinel Connectors, AWS, GCP, Palo Alto, Cisco | IBM QRadar DSMs (700+), Cisco, Check Point, Palo Alto, CrowdStrike, AWS | AWS, Azure, GCP, Okta, endpoint agents (Elastic Agent), Beats ecosystem | AWS, Azure, M365, Okta, Active Directory, CrowdStrike, Carbon Black, Rapid7 Nexpose/InsightVM |
| **SOAR Capabilities** | Splunk SOAR (formerly Phantom) — fully featured, separate license | Microsoft Sentinel built-in playbooks (Logic Apps); Microsoft Defender XDR automation | QRadar SOAR (formerly Resilient) — mature, separate product | Elastic built-in rules with response actions; native integration with third-party SOAR | InsightConnect (Rapid7 SOAR) — included in some bundles; strong workflow automation |
| **Threat Intelligence Integration** | Splunk TI Management; TAXII/STIX feeds; third-party TI apps | Microsoft Threat Intelligence (built-in); TAXII/STIX; third-party connectors | IBM X-Force (built-in); TAXII/STIX; QRadar TI app | Elastic Threat Intel module; TAXII/STIX; third-party feeds | Rapid7 Threat Command (built-in); AttackerKB integration; community feeds |
| **Compliance Reporting Capabilities** | Extensive (PCI DSS, HIPAA, SOX, CMMC, NIST); Splunk App for PCI/HIPAA available | Strong (NIST, ISO 27001, SOC 2, CIS, CMMC); Compliance Workbooks native | Very strong (PCI DSS, HIPAA, SOX, FISMA, DISA STIG); designed for regulated industries | Moderate; requires dashboard customization; CIS/NIST mapping available | Moderate; key compliance dashboards included; PCI, HIPAA, SOC 2 coverage |

---

### 1.2 Platform Deep-Dive Narratives

#### Splunk Enterprise Security

Splunk Enterprise Security remains the gold standard for large enterprise security operations centers that require maximum flexibility and analytical depth. Its Search Processing Language (SPL) enables analysts to construct nearly any query or correlation imaginable, and the Splunkbase ecosystem of over 2,500 apps means there is almost always a pre-built integration or content pack available. The trade-off is cost and complexity: Splunk deployments at scale require dedicated engineering resources and can produce sticker shock as data volumes grow, making budget predictability a persistent challenge for clients. Professional services investment is often significant at initial deployment, and ongoing tuning demands SIEM-specialized staff. For clients who already have Splunk expertise in-house or who are willing to invest in building that capability, Splunk ES delivers unmatched depth and is particularly strong in environments where custom detection engineering is a priority.

#### Microsoft Sentinel

Microsoft Sentinel is purpose-built for cloud-native organizations, especially those heavily invested in the Microsoft ecosystem. For clients running M365 E5, Azure AD, and Microsoft Defender, the native data connectors eliminate weeks of integration work, and the consumption-based pricing model can deliver significant cost advantages versus traditional per-GB SIEM pricing when Microsoft data sources qualify for free or reduced-cost ingestion. Sentinel's built-in ML-based analytics, UEBA, and hunting capabilities are strong for cloud workloads, and its Logic Apps-based SOAR makes automation accessible without requiring deep development skills. The platform's reliance on Azure infrastructure means it is less compelling for on-premises-dominant organizations, and costs can climb unexpectedly for clients ingesting large volumes of non-Microsoft log data. However, for a Microsoft-centric client evaluating their first enterprise SIEM, Sentinel frequently wins on total cost of ownership.

#### IBM QRadar

IBM QRadar is one of the most established SIEMs in regulated industries, particularly financial services, government, and healthcare, where compliance reporting depth and vendor reputation carry significant weight. QRadar's offense management model — aggregating correlated events into actionable offense records — provides a structured investigation workflow that many SOC teams find intuitive. The platform's network traffic analysis capabilities via QRadar Network Insights (QNI) and QFlow give it strong east-west visibility that pure log-based SIEMs cannot match. QRadar has faced headwinds from newer cloud-native competitors due to a slower UI modernization pace and a complex licensing model, but IBM's 2023 acquisition of QRadar by Palo Alto Networks (which retained the product as IBM QRadar under continued development) has added uncertainty to the roadmap. It remains the right choice for clients with existing IBM investments, strict on-premises requirements, or compliance mandates that align with QRadar's mature reporting suite.

#### Elastic SIEM (Elastic Security)

Elastic Security delivers exceptional value-to-cost ratio, particularly for organizations that are comfortable with open-source tooling or already use the Elastic Stack for observability. The Elastic Common Schema (ECS) provides strong normalization across diverse log sources, and the combined endpoint agent (Elastic Agent) allows organizations to consolidate EDR and SIEM data collection into a single platform. At self-managed scale, Elastic can ingest and retain data at a fraction of the cost of commercial SIEM platforms, making it a strong choice for cost-sensitive clients with engineering resources to operate it. The trade-off is operational overhead: Elastic self-managed deployments require meaningful engineering investment, and Elastic Security's detection and alert management interfaces, while improving, lag behind the purpose-built SOC workflows of Splunk ES or QRadar. Elastic Cloud reduces the operations burden significantly and is worth serious consideration for mid-market clients seeking a cost-effective scalable SIEM.

#### Rapid7 InsightIDR

Rapid7 InsightIDR is purpose-built for organizations that want rapid deployment, guided outcomes, and predictable pricing without requiring a dedicated SIEM engineer. InsightIDR's user-based pricing model eliminates the log volume anxiety that plagues GB/day-priced SIEMs, and the platform ships with pre-built detection libraries, built-in UEBA, and Rapid7's threat intelligence integrated from day one. Deployment timelines of one to four weeks are realistic for mid-market environments, and the guided investigation workflow makes InsightIDR accessible to analysts without deep SIEM expertise. The platform's trade-off is customization ceiling: organizations that need to write complex custom detection logic, build bespoke dashboards, or handle unusually high log volumes at enterprise scale will find InsightIDR more constrained than Splunk or Elastic. For the right client — mid-market, M&A targets, clients transitioning from no SIEM — InsightIDR is frequently the strongest recommendation.

---

## Section 2: SIEM Recommendation Guide by Client Profile

### 2.1 By Client Size

#### SMB (< 250 Employees, < $50K Annual Security Budget)

**Top Recommendations: Rapid7 InsightIDR, Microsoft Sentinel (if M365), Elastic SIEM (self-managed)**

| Option | Why It Fits | Caution |
|---|---|---|
| **Rapid7 InsightIDR** | Fastest deployment, predictable pricing, minimal SIEM expertise required, built-in UEBA and TI | SaaS-only; requires internet access; customization limits |
| **Microsoft Sentinel** | Excellent if client is already on M365 E5 — many Microsoft logs ingest free; minimal infrastructure overhead | Costs can escalate for non-Microsoft sources; requires Azure familiarity |
| **Elastic SIEM** | Very low cost if client has technical staff; open-source option for the truly budget-constrained | Requires engineering effort to deploy and maintain; not guided |

**Guidance:** For an SMB with limited security staffing, InsightIDR is the default recommendation — it is the platform most likely to be operational and providing value within 30 days. Avoid recommending Splunk to SMBs unless there is a compelling reason; the cost and expertise requirements are mismatched. Sentinel is a natural fit if the client is already in the Microsoft ecosystem and has an M365 E5 license.

---

#### Mid-Market (250–2,500 Employees, $50K–$250K Budget)

**Top Recommendations: Rapid7 InsightIDR, Microsoft Sentinel, Elastic Security (Cloud)**

| Option | Why It Fits | Caution |
|---|---|---|
| **Rapid7 InsightIDR** | Strong fit for 250–1,000-employee range; user-based pricing scales predictably; built-in UEBA and MDR overlay available | Limited for very complex custom detection needs |
| **Microsoft Sentinel** | Excellent for Microsoft-centric mid-market; strong compliance reporting; manageable cost with Defender integration | Cost risk if ingesting many non-Microsoft sources |
| **Elastic Security (Cloud)** | Strong value-to-performance ratio; good for tech-savvy security teams; scales well | Less guided than InsightIDR; alert management less mature |
| **Splunk** | Consider if client has 1,500+ employees and a security team capable of managing it | High cost; may require professional services ongoing |

**Guidance:** Mid-market is the most competitive segment. Lead with InsightIDR for clients without SIEM experience or without dedicated security engineers. Lead with Sentinel for Microsoft-heavy shops. Consider Elastic for clients with technical security teams that are cost-conscious.

---

#### Enterprise (2,500+ Employees, > $250K Budget)

**Top Recommendations: Splunk Enterprise Security, Microsoft Sentinel, IBM QRadar**

| Option | Why It Fits | Caution |
|---|---|---|
| **Splunk Enterprise Security** | Maximum flexibility; supports large, complex SOC operations; unmatched ecosystem | Very high cost; requires dedicated Splunk expertise |
| **Microsoft Sentinel** | Strong for large Microsoft-heavy environments; powerful ML analytics; scales to massive data volumes | Azure lock-in; non-Microsoft source costs |
| **IBM QRadar** | Regulated industries with compliance requirements (financial, healthcare, government) | Slower innovation; complex licensing |
| **Elastic Security** | Large-scale deployments where cost and flexibility are both priorities | Engineering overhead for self-managed; alert management maturity |

**Guidance:** Enterprise clients should be evaluated individually. A large financial institution with on-prem requirements and FISMA obligations is a QRadar conversation. A large technology company in Azure is a Sentinel conversation. A Fortune 500 with a 20-person SOC wanting maximum detection engineering capability is a Splunk conversation.

---

### 2.2 By Existing Tech Stack

#### Microsoft-Heavy Shops (AD, M365, Azure)

**Primary Recommendation: Microsoft Sentinel**

Microsoft Sentinel is the natural fit. Native connectors for Azure Active Directory, M365 Defender, Defender for Endpoint, Defender for Cloud, and Teams eliminate weeks of integration effort. For clients on M365 E5, many of the highest-value log sources (Azure AD sign-in logs, Office 365 audit logs, Defender alerts) ingest at no additional cost or at significantly reduced rates. Position Sentinel as the security control plane that extends investments the client has already made. Secondary recommendation is Splunk if the client has complex cross-platform detection needs beyond the Microsoft estate.

#### AWS-Primary Environments

**Primary Recommendation: Splunk (Splunk Cloud + AWS Add-on) or Elastic Security**

Splunk has the most mature AWS integration story with the Splunk Add-on for AWS supporting CloudTrail, GuardDuty, VPC Flow Logs, S3, Config, and more. Microsoft Sentinel's AWS connectors exist but are secondary to its Azure story. Elastic Security is an excellent alternative given strong AWS marketplace availability and native S3 ingestion. InsightIDR also has solid AWS coverage and is worth recommending for mid-market AWS shops that want fast deployment.

#### Multi-Cloud / Hybrid Environments

**Primary Recommendation: Splunk or Elastic Security**

Multi-cloud environments favor platforms that are equally comfortable across AWS, Azure, and GCP without native bias. Splunk's breadth of integrations makes it the gold standard here. Elastic Security is a strong cost-effective alternative, particularly for organizations that already use Elastic for observability across cloud providers. Microsoft Sentinel can cover multi-cloud but is architecturally Azure-centric. IBM QRadar works in multi-cloud but its cloud connectors lag competitors.

#### Already Have Splunk Infrastructure

**Guidance:** If the client already runs Splunk (even for IT operations or DevOps), the path of least resistance for SIEM is Splunk Enterprise Security layered on top of existing infrastructure. Existing data pipelines, forwarders, and team familiarity dramatically reduce deployment time and cost. Focus the conversation on augmenting their existing Splunk deployment with the ES premium app and security content packs rather than introducing a competing platform.

#### Already Have IBM Infrastructure

**Guidance:** If the client has an existing IBM QRadar deployment, the default position is to optimize and expand the existing investment rather than rip-and-replace. Identify gaps in log source coverage, tune existing rules, and add QRadar SOAR (Resilient) if not already in place. Only consider migration away from QRadar if the client explicitly identifies platform limitations that cannot be addressed through expansion — migration projects are expensive and disruptive.

#### Open to Open-Source / Cost-Sensitive

**Primary Recommendation: Elastic SIEM (self-managed or Elastic Cloud Basic/Standard)**

For clients with tight budgets and engineering capability, the Elastic Stack (Elasticsearch + Kibana + Elastic Security) provides enterprise-grade log management and SIEM capability at dramatically lower cost than commercial alternatives. The open-source Elastic distribution includes basic SIEM features; a paid subscription adds advanced detection, endpoint security, and support. Wazuh (open-source, Elastic-based) is also worth mentioning for the smallest organizations. Caution: self-managed Elastic requires meaningful DevOps capability — this is not a recommendation for clients without technical staff.

---

### 2.3 By Use Case Priority

#### Compliance-Driven (SOC 2, PCI, HIPAA, CMMC)

| Compliance Framework | Best Fit Platform | Why |
|---|---|---|
| **PCI DSS** | Splunk ES or IBM QRadar | Deep out-of-the-box PCI reporting; mature cardholder data environment coverage |
| **HIPAA** | Splunk ES, Microsoft Sentinel, or IBM QRadar | Strong PHI access logging, audit trails, and breach detection rules |
| **SOC 2** | Microsoft Sentinel (M365 shops) or Splunk ES | Comprehensive audit logging, change management tracking, access reviews |
| **CMMC / NIST 800-171** | Splunk ES, Microsoft Sentinel (GCC), or IBM QRadar | CMMC-mapped content available; GCC sovereign cloud required for some contractors |
| **FISMA / FedRAMP** | IBM QRadar (on-prem), Microsoft Sentinel (FedRAMP-authorized) | Government compliance pedigree; authorized deployment options available |

**Guidance:** Lead with compliance coverage in regulated industry conversations. All major platforms have compliance content, but the depth varies. Ask the client: "Which specific framework are you audited against, and what evidence collection is most painful today?" This surfaces the reporting automation upsell opportunity.

#### Threat Detection and Response Focus

**Primary Recommendation: Splunk Enterprise Security or Rapid7 InsightIDR + InsightConnect**

For clients whose primary driver is "find threats faster and respond more effectively," the SIEM-to-SOAR workflow is the critical capability. Splunk ES with Splunk SOAR delivers the most powerful custom detection-to-response automation. InsightIDR with InsightConnect is the faster-to-value option for mid-market clients. Microsoft Sentinel with Defender XDR integration is strong for cloud-native threat scenarios. Ensure UEBA capability is present regardless of platform — insider threat and compromised credential scenarios require behavioral baselines.

#### Cloud Security Monitoring Focus

**Primary Recommendation: Microsoft Sentinel (Azure-primary) or Splunk Cloud (multi-cloud)**

Cloud security monitoring requires deep integration with cloud provider control planes (CloudTrail, Azure Monitor, GCP Audit Logs) and cloud-native services (IAM, serverless, containers). Microsoft Sentinel leads for Azure-primary environments. Splunk Cloud with its AWS and GCP add-ons leads for multi-cloud. Elastic Security with cloud-native integrations is a strong cost-effective alternative. InsightIDR covers cloud basics but is not the strongest choice for clients with complex cloud-native architectures.

#### Cost Optimization Primary Driver

**Primary Recommendation: Elastic SIEM (self-managed) or Microsoft Sentinel (M365 shops)**

| Client Type | Recommendation | Why |
|---|---|---|
| Technical team, any cloud | Elastic self-managed | Near-zero licensing cost; infrastructure cost only |
| M365 E5 shop | Microsoft Sentinel | Significant Microsoft source free-ingestion credits |
| Mid-market, no technical SIEM staff | Rapid7 InsightIDR | Predictable user-based pricing; avoids log volume bill shock |
| Any client avoiding Splunk costs | Elastic Cloud Basic | Managed service; substantially lower than Splunk GB/day |

#### Fastest Time to Deployment

**Primary Recommendation: Rapid7 InsightIDR (1–2 weeks) or Microsoft Sentinel (2–3 weeks for M365 shops)**

InsightIDR holds the strongest time-to-value story for most environments. Cloud-native, no infrastructure to provision, guided onboarding, and pre-built detections mean a client can be running with active alerts in under two weeks. Microsoft Sentinel is nearly as fast for Microsoft-centric shops. Avoid recommending Splunk, QRadar, or self-managed Elastic when speed-to-deployment is the top criterion — all three require meaningful setup time.

---

## Section 3: How to Position Each Platform in Client Conversations

### 3.1 Rapid7 InsightIDR vs. Splunk

#### When to Lead with InsightIDR

- Client is mid-market (250–2,000 employees) with limited dedicated security engineering resources
- Client does not have (and cannot hire) a full-time SIEM engineer or Splunk administrator
- Client has experienced SIEM sticker shock or failed Splunk deployments in the past
- Client values predictable pricing over maximum customization
- Client wants to be operational quickly — a 90-day deployment timeline is too long
- Client is evaluating MDR overlay and wants a platform that integrates cleanly with managed services
- Client has an existing Rapid7 relationship (InsightVM, Nexpose) — upsell path is natural

**Talking Points for InsightIDR:**

- "InsightIDR deploys in days, not months. Your team will be investigating real alerts within two weeks of kickoff."
- "The pricing is per asset, not per gigabyte. You can add log sources without worrying about bill surprises."
- "UEBA is built in — you don't need a separate product to detect compromised credentials or insider threats."
- "Rapid7's threat intelligence comes pre-loaded. You're detecting against current IOCs from day one."
- "This is a SIEM designed to be operated by your security team, not just by Splunk specialists."

#### When Splunk Wins

- Client runs a mature SOC with dedicated Splunk-trained analysts and engineers
- Environment is complex (multi-cloud, multiple business units, 5,000+ assets)
- Client needs custom detection logic that goes beyond pre-built rule libraries
- Client requires bespoke dashboards and reporting that are not available as templates
- Client has a large existing Splunk investment (infrastructure, licenses, content) already in place
- Client's use cases require advanced correlation across disparate, non-standard data sources
- Client is in a data-intensive industry (telco, large financial institution) where SPL power is a genuine differentiator

**Talking Points for Splunk:**

- "Splunk gives your analysts a query language that can answer almost any question about your environment — it's the most powerful analytical tool in security operations."
- "With 2,500+ apps on Splunkbase, there is almost certainly a pre-built integration for every data source and vendor in your stack."
- "For a SOC at your scale, you need a platform that grows with your use cases, not one that constrains them."
- "Splunk SOAR can automate response workflows at a level of sophistication that most platforms cannot match."

---

### 3.2 Splunk vs. Microsoft Sentinel

#### When Sentinel Wins

- Client is Microsoft-heavy: Azure AD, M365 E5, Microsoft Defender suite already deployed
- Client wants cloud-native SIEM with zero infrastructure management
- Pay-per-use / consumption pricing is attractive (client has variable or uncertain data volumes)
- Client has a cost-reduction mandate — Sentinel's Microsoft-source free ingestion credits are significant
- Client's security use cases are predominantly identity, cloud, and email (Microsoft's core strengths)
- Client wants rapid deployment without Splunk expertise
- Client already uses Azure Monitor and wants a unified security + observability pane

**Key Talking Point:** "If you're already paying for M365 E5, Sentinel dramatically reduces your total SIEM cost. Azure AD, Defender for Endpoint, and Office 365 audit logs all ingest at no additional charge. For a client of your size on M365 E5, we're often looking at 40–60% lower total SIEM cost compared to a comparable Splunk deployment."

#### When Splunk Wins Over Sentinel

- Client has a mixed or non-Microsoft environment (Linux-heavy, AWS-primary, diverse on-prem)
- Client needs cross-platform correlation that extends well beyond the Microsoft ecosystem
- Client requires complex custom detection use cases that demand SPL-level query power
- Client has established Splunk SOAR automation workflows they are not willing to migrate
- Client's security team is Splunk-trained and change management risk is real
- Client has governance or data residency requirements that conflict with Azure cloud hosting

**Positioning Note:** Never position Sentinel as inferior — rather, position it as the right tool for the right environment. "Sentinel is purpose-built for Microsoft ecosystems. If that describes your environment, it is the best choice. If you're in a multi-cloud, multi-vendor world, Splunk's breadth becomes a genuine advantage."

---

### 3.3 IBM QRadar Positioning

#### When QRadar Is the Right Choice

- Client is in a regulated industry with deep compliance requirements: financial services (PCI DSS, SOX), healthcare (HIPAA), government / defense (FISMA, CMMC, DISA STIG)
- Client has an on-premises deployment requirement (air-gapped networks, data sovereignty)
- Client has an existing IBM security investment (IBM Security Verify, IBM Guardium, IBM MaaS360) — the integration story is compelling
- Client has network-centric security requirements where QRadar Network Insights (QNI) and QFlow add unique visibility
- Client's procurement team is IBM-relationship-driven and prefers established enterprise vendors
- Client needs a SIEM with a long track record in government or financial sector audits

**Talking Points for QRadar:**

- "QRadar has been deployed in some of the most demanding regulated environments in the world — financial institutions, government agencies, and healthcare networks where compliance depth is non-negotiable."
- "QRadar's offense management model is purpose-built for SOC workflows — correlated events aggregate into offenses with risk scores, giving your analysts a structured queue rather than a flood of individual alerts."
- "If your network visibility is as important as log analysis, QRadar's network traffic analysis capabilities provide context that log-only SIEMs simply cannot."

#### Positioning QRadar in Competitive Situations

**vs. Splunk:** "QRadar delivers a structured, compliance-ready SIEM without requiring your team to build everything from scratch in SPL. The offense management workflow and pre-built compliance reports reduce implementation time significantly for regulated environments."

**vs. Microsoft Sentinel:** "For clients with on-premises requirements or non-Azure infrastructure, QRadar provides the enterprise-grade compliance depth that Sentinel — as an Azure-native service — cannot match in air-gapped or sovereign environments."

**vs. InsightIDR:** "For enterprise compliance environments and organizations with complex network environments, QRadar's depth and regulatory pedigree outweigh InsightIDR's deployment speed advantage."

**Caution:** Be transparent about QRadar's innovation trajectory. The IBM/Palo Alto acquisition has created some market uncertainty. If a client raises this, acknowledge it and focus the conversation on the current product's strengths, the active support commitment, and the regulatory community's continued trust in the platform.

---

## Section 4: SIEM Expansion Conversation Guide

The following section maps SIEM service expansion opportunities to specific conversation frameworks. Use these paths during quarterly business reviews, security posture assessments, and advisory conversations.

---

### 4.1 Additional Log Sources → SIEM Expansion

**Core Message:** Frame log source expansion as closing security blind spots, not adding line items.

**Discovery Questions:**
- "What percentage of your environment is currently sending logs to your SIEM?"
- "If an attacker moved laterally from [uncovered system] to [covered system], would you detect the initial compromise?"
- "Have there been any security incidents in the past year where you wished you had more log context?"

**Value Framing:**

"You currently have approximately [X]% of your environment monitored. The [Y] systems not sending logs represent blind spots where an attacker could operate undetected. Adding [specific log source] to your SIEM would enable detection of [specific threat scenario — e.g., lateral movement using compromised service accounts, data exfiltration via cloud storage, privilege escalation in Linux systems]."

**Common Expansion Targets and Their Detection Value:**

| Log Source to Add | Threat Scenarios Unlocked |
|---|---|
| DNS logs | Command-and-control (C2) beaconing, DNS tunneling, newly registered domain access |
| Web proxy / CASB | Data exfiltration detection, malware download, unauthorized SaaS usage |
| Cloud IAM (AWS, Azure, GCP) | Privilege escalation, credential compromise, misconfigured access |
| Linux/Unix syslog | Lateral movement, privilege escalation, cron-based persistence |
| Database audit logs | SQL injection detection, unauthorized data access, insider threat |
| Email gateway | Phishing delivery, malicious attachment analysis, BEC indicators |

**Pricing Framing:** For GB/day-priced SIEMs (Splunk, Sentinel), be transparent: "Adding DNS logs will increase your ingestion by approximately [X] GB/day at a monthly cost of approximately [Y]. The detection value — particularly for C2 and exfiltration — is significant relative to that cost." For InsightIDR (user-based pricing): "Adding these log sources has no additional per-source cost — it's included in your existing subscription."

---

### 4.2 Cloud Workload Visibility → Cloud SIEM Connector Expansion

**Core Message:** Cloud infrastructure is where modern attacks happen; SIEM coverage must follow workloads to the cloud.

#### AWS CloudTrail and GuardDuty Integration Conversation

"Your SIEM currently monitors your on-premises environment effectively. However, [X]% of your workloads are in AWS, and those represent a growing attack surface. AWS CloudTrail logs every API call — creating IAM users, modifying security groups, accessing S3 buckets — and without it in your SIEM, you would not detect an attacker operating within your AWS environment."

**Key AWS sources to connect:**
- CloudTrail (IAM and API activity) — highest value, connect first
- GuardDuty findings — pre-processed threat detection, easy to ingest
- VPC Flow Logs — network visibility in cloud
- S3 access logs — data exfiltration detection
- AWS Config — configuration drift and compliance tracking

#### Azure Sentinel Native / Splunk Cloud Connector

For clients running Splunk or another SIEM but with Azure workloads: "We can connect your Azure environment to [SIEM Platform] using [Splunk Add-on for Microsoft Azure / the Azure Monitor API connector]. This gives your existing SIEM visibility into Azure AD sign-ins, Azure resource changes, and Defender for Cloud alerts — without requiring a second SIEM platform."

#### Multi-Cloud Coverage Narrative

"Modern attackers don't respect cloud boundaries — they'll follow the path of least resistance across AWS, Azure, and GCP. Today your SIEM has good coverage of [primary cloud]. Your [secondary cloud] workloads are currently a blind spot. A multi-cloud connector expansion closes that gap and gives your SOC a unified view of your entire estate."

---

### 4.3 Application Security Testing → AppSec Finding Integration

**Core Message:** SAST and DAST findings are not just development artifacts — they are pre-crime intelligence for your SIEM.

**Conversation Approach:**

"Your application security testing program is generating valuable data about vulnerabilities in your codebase. Right now, those findings live in [Veracode/Checkmarx/Burp/etc.] and your development team's ticketing system. By feeding those findings into your SIEM, we can do two things: first, track whether known vulnerable endpoints are being targeted in production logs; second, alert your SOC when traffic patterns match exploitation attempts against vulnerabilities that are already on your radar."

**Specific Integration Value:**
- SAST findings → Create SIEM watchlists for vulnerable API endpoints; alert on exploitation signatures
- DAST findings → Correlate web application firewall logs against discovered attack surfaces
- Dependency vulnerability data (SCA) → Alert when known-vulnerable components are accessed in unusual ways
- Application-layer detection rules: authentication bypass patterns, SQL injection in app logs, unusual API call sequences

**Upsell Path:** AppSec findings integration creates a natural bridge conversation into application log onboarding (web server logs, application-layer access logs), which increases SIEM ingestion scope.

---

### 4.4 Threat Detection and Response → SOAR and MDR Upsell

**Core Message:** Detection without response is a smoke alarm with no fire department.

#### Moving from Detection-Only to Automated Response

**Discovery Questions:**
- "When your SIEM fires an alert, what happens next? Who sees it, and what is the response process?"
- "How many alerts per day does your team currently receive? What percentage are investigated?"
- "How long does it typically take from alert to containment of a confirmed incident?"

**SOAR Value Framing:**

"Your SIEM is doing its job — it's generating alerts. The gap is in the response workflow. For the most common, highest-confidence alert types — known malware hash, impossible travel login, phishing email with payload — the response playbook is the same every time: isolate endpoint, disable user account, capture forensic snapshot. SOAR automates that playbook so your team's attention goes to the alerts that actually require human judgment."

**SOAR Conversation by Platform:**
- **Splunk customers:** Introduce Splunk SOAR (Phantom) — native integration, strongest automation capability
- **InsightIDR customers:** Introduce InsightConnect — built on the same platform, easy activation
- **Sentinel customers:** Highlight Logic Apps playbooks — already included, no additional product to buy
- **QRadar customers:** Introduce QRadar SOAR (Resilient) — purpose-built SOC orchestration with case management

#### MDR Overlay: When to Recommend Managed Detection vs. Self-Managed SIEM

**Recommend MDR consideration when:**
- Client's security team has fewer than 2 FTEs dedicated to security operations
- Client cannot provide 24/7 alert monitoring coverage
- Client has experienced a security incident and leadership is demanding faster response
- Client's SIEM alert queue is not being cleared within acceptable SLAs
- Client is asking "we know we need a SIEM but we don't have the people to run it"

**MDR Positioning:** "A self-managed SIEM gives you maximum control and lowest per-event cost, but it requires dedicated security operations resources to be effective. If your team cannot investigate alerts within [X hours], the SIEM is generating evidence you will only read after an incident. An MDR overlay means a team of analysts is monitoring your alerts around the clock — and they are accountable for response SLAs."

---

### 4.5 Reporting Automation → SIEM Dashboard and Report Builder

**Core Message:** If your team is spending time building compliance reports manually, your SIEM is not doing its full job.

**Discovery Questions:**
- "How do you currently produce your board-level security reports? How long does that take each month?"
- "What evidence does your auditor require at your next PCI/SOC 2/HIPAA audit, and where does that evidence come from today?"
- "Does your leadership team have a real-time view of your security posture, or is that a quarterly slide deck?"

**Executive Dashboard Value:**

"Every major SIEM platform includes an executive dashboard capability. What most clients are not using is the automated report generation that runs on a schedule — daily security summary delivered to your CISO inbox, weekly threat trend report for your risk committee, monthly compliance posture summary for your audit trail. This replaces the manual work your analyst is currently doing to pull those numbers."

**Compliance Report Automation:**

| Compliance Framework | What SIEM Automates |
|---|---|
| **PCI DSS** | Log review evidence (10.2), access control logs (7.x/8.x), failed login tracking (8.2), network activity reports |
| **HIPAA** | PHI access audit logs, unauthorized access attempt reports, workforce activity monitoring |
| **SOC 2** | Logical access reviews, change management logs, incident detection evidence, availability monitoring |
| **CMMC** | Audit log collection (AU domain), incident tracking, user activity monitoring |

**ROI Framing:** "We can automate the compliance reports that currently take your team [X] hours per month. At a fully-loaded rate of [Y] per hour, that is [Z] per month in analyst time recaptured — time that goes back into actual threat investigation rather than report assembly."

---

### 4.6 Ticketing Integration → ServiceNow / Jira SIEM Integration

**Core Message:** Alerts that do not become tickets get forgotten. Tickets without alert context get closed without being investigated.

**Discovery Questions:**
- "When your SIEM fires an alert, does it automatically create a ticket, or does someone manually enter it?"
- "How do you track the status of open security alerts? Is that in your SIEM, your ticketing system, or a spreadsheet?"
- "Have you ever had a high-priority alert that did not get investigated because it fell through the cracks?"

**Bi-Directional Integration Benefits:**

"A SIEM-to-ticketing integration does two things. First, every alert that meets your severity threshold automatically creates a ticket in ServiceNow [or Jira] — with the full alert context, raw log data, and SIEM investigation link included. No manual copying. Second, when your analyst closes the ticket after investigation, the closure status flows back to the SIEM, closing the loop in your alert queue. Alerts do not fall through the cracks, and your SIEM alert hygiene stays clean."

**ServiceNow Integration Specifics:**
- SIEM platforms with native ServiceNow integrations: Splunk (certified app), IBM QRadar (certified app), Microsoft Sentinel (Logic Apps connector), Rapid7 InsightIDR (native connector), Elastic (via webhook or Elastic connector)
- Bi-directional: alert fires → ticket created → analyst investigates in ServiceNow → closure syncs to SIEM
- SLA tracking: ServiceNow SLA rules can enforce your MTTR (mean time to respond) SLAs on SIEM-generated tickets

**Jira Integration Specifics:**
- Particularly relevant for clients where the security team uses Jira alongside the development team
- AppSec findings + SIEM alerts in the same project board creates a unified risk tracking view
- Automate: SIEM alert → Jira issue → assigned to on-call analyst → closure triggers SIEM resolution

**ROI Framing:** "The cost of a missed high-severity alert is an incident you did not contain in time. The ticketing integration cost is a one-time setup. The question is not whether you can afford the integration — it is whether you can afford the alternative of continuing to track critical alerts in a manual process."

---

*End of SIEM Platform Guide*

---

> **Document Control**
> Version: 1.0 | Owner: [Practice Lead Name] | Review Cycle: Annual or upon major platform update
