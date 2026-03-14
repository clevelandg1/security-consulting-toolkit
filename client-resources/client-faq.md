# Frequently Asked Questions — Security Consulting Engagement

This document answers the questions we hear most often from clients at every stage of a security consulting engagement. If your question is not covered here, please reach out to your consultant directly — no question is too basic.

---

## Getting Started

**What will the first 30 days look like?**

The first 30 days are focused on understanding your environment and establishing a baseline. Here is a general outline of what to expect:

- **Week 1–2:** Kickoff meeting, onboarding paperwork, and gathering information about your systems, technology inventory, and priorities. We set up our tools and establish secure access to your environment.
- **Week 2–3:** Initial discovery and vulnerability scanning. We run our first scans to identify what exists in your environment and what potential issues are present.
- **Week 3–4:** Review of initial findings, a baseline risk assessment, and delivery of your first report. We will walk you through what we found, what it means, and what the priorities are.

By the end of Day 30, you will have a clear picture of where you stand and a prioritized plan for what comes next.

---

**What information do you need from us to get started?**

To get started efficiently, we typically need:

- A list of your systems, IP address ranges, and cloud environments (as complete as you have — we can help fill gaps)
- Contact information for your IT team or IT provider
- Any existing documentation about your network or technology infrastructure
- Information about systems that are sensitive or business-critical (so we treat them carefully during scanning)
- Any regulatory or compliance frameworks that apply to your business (HIPAA, PCI-DSS, SOC 2, etc.)
- Network access credentials or VPN details, as agreed during onboarding

You do not need to have everything perfectly documented before we start. Part of our job is helping you build that picture.

---

**Who from our team needs to be involved?**

At minimum, we need a primary point of contact on the business side and someone who can coordinate access with your IT team. Beyond that, the level of involvement depends on what we find.

For day-to-day communication: your IT manager or IT point of contact.
For strategic decisions and report reviews: a business leader who can make decisions about risk and priorities.
For specific findings: the owners of the systems or applications in question.

We try to keep disruption to a minimum and work through a small number of contacts rather than pulling your entire team into every conversation.

---

**How disruptive will the initial assessment be to our operations?**

In most cases, our initial assessment has no noticeable impact on your day-to-day operations. Vulnerability scanning is largely passive and is designed to observe and probe systems without disrupting them.

That said, we do take precautions:

- We communicate our scanning schedules in advance so your IT team is not alarmed by unusual network activity.
- We can schedule more intensive scans during off-hours if you prefer.
- We avoid aggressive scanning techniques on production systems unless we have discussed and agreed on that approach.

If you have systems that are especially sensitive — for example, older industrial control systems or legacy applications that might not handle scanning well — please tell us early so we can adjust our approach.

---

## Vulnerability Scanning and Assessment

**Will scanning impact our systems or cause downtime?**

Standard vulnerability scanning very rarely causes downtime. Our scanning tools are designed to test systems without disrupting them, and we follow industry best practices to minimize any risk.

The most common concern is with older or poorly maintained systems that may be less stable. If you have systems in that category, let us know and we will take extra care — or test those systems separately during a controlled window.

In the unlikely event that a scan does contribute to a system issue, we have procedures in place to document and communicate that promptly.

---

**How often will you scan our environment?**

The cadence depends on your engagement agreement, but a typical approach includes:

- **Continuous or weekly automated scanning** for your internet-facing systems (these are the most exposed and change most frequently)
- **Monthly internal scans** of your broader network environment
- **On-demand scans** triggered by significant changes — a new system deployed, a major software update, or a widely publicized vulnerability that could affect your technology

We also scan after remediation to verify that fixes have been applied correctly.

---

**What happens if you find something critical during a scan?**

We notify you immediately — we do not wait for a scheduled report. Critical findings trigger an out-of-cycle alert to your designated contacts with a clear explanation of what was found, what it means, and what to do first.

We will also be available to discuss the finding directly and provide guidance to your IT team on immediate steps to reduce the risk while a full fix is being applied.

---

**What is the difference between a vulnerability assessment and a penetration test?**

These are related but different activities, and it is worth understanding the distinction:

A **vulnerability assessment** is a broad, systematic scan of your environment to identify known weaknesses. It is comprehensive, it runs regularly, and it focuses on finding and cataloging problems so they can be addressed.

A **penetration test** (often called a "pen test") is a targeted, time-limited exercise where a security expert actively attempts to exploit vulnerabilities — simulating what a real attacker would do. It is more focused and is typically conducted once or twice a year.

Think of the difference this way: a vulnerability assessment is like a building inspector walking through your facility and noting every issue. A penetration test is like hiring an ethical burglar to see how far they can actually get.

Both are valuable. Ongoing vulnerability assessment is the foundation of your security program. Penetration testing adds depth by showing you what a real attack would look like.

---

**Will you be looking at our cloud environments too?**

Yes — if you have cloud environments (such as AWS, Microsoft Azure, or Google Cloud Platform) and you have included them in our scope, we assess them as part of your program.

Cloud environments have their own unique set of vulnerabilities: misconfigured storage buckets that are publicly accessible, over-permissioned user accounts, exposed APIs, and gaps in logging. These are increasingly common and consequential.

If cloud coverage is not yet part of your engagement, speak with your consultant about adding it. Organizations that operate in the cloud without extending their security monitoring to that environment have significant blind spots.

---

## Reports and Findings

**What reports will we receive and how often?**

You will typically receive:

- **Executive Summary Reports** — A brief, plain-English overview of your current risk posture, what has improved, and what still needs attention. Delivered monthly or quarterly depending on your engagement.
- **Technical Reports** — Detailed findings intended for your IT team, with full vulnerability descriptions and step-by-step remediation guidance. Delivered after each major scanning cycle.
- **Critical Finding Notifications** — Delivered immediately whenever a Critical vulnerability is identified, outside of the normal reporting schedule.
- **Trend and Progress Reports** — Periodic summaries showing how your risk posture is changing over time, useful for board presentations, insurance renewals, and audits.

Your consultant can adjust the format or frequency of reporting based on your needs.

---

**Who should review the technical report versus the executive report?**

**Executive Summary:** Written for business leaders, owners, and board members. It covers the bottom line — how are we doing, what is the current risk level, and are we moving in the right direction. No technical background required.

**Technical Report:** Written for your IT team, security staff, or managed IT provider. It contains specific vulnerability details, affected system names, and step-by-step remediation instructions. The technical report is not meant to be reviewed by executive leadership directly, though executives are welcome to ask us to walk them through any section.

---

**How are findings prioritized?**

We use a standardized severity rating system: Critical, High, Medium, and Low. Each level has a clear business meaning and a defined timeframe for remediation.

Beyond severity, we also consider context — a High vulnerability on a server that holds sensitive customer data is more urgent than the same High vulnerability on an internal system with no external exposure. We factor that into our recommendations.

For a full explanation of each severity level, see the companion document: *Understanding Risk Ratings.*

---

**What if we disagree with a finding or its severity rating?**

That is a reasonable and welcome conversation. Our findings are based on industry-standard scoring methodologies, but there are legitimate reasons why a finding might look different in your specific context.

If you believe a finding does not apply to your environment, or that the severity is overstated given your specific circumstances, bring it to your consultant. We will review it together. If the context warrants a rating adjustment or the finding can be marked as a false positive (meaning our tool flagged something that is not actually a real risk in your environment), we will update the record accordingly.

What we ask is that disagreements be discussed rather than silently ignored — an unaddressed finding, even a disputed one, carries risk until it is formally resolved.

---

**How long do we have to fix things?**

Response time targets are based on severity:

| Severity | Target Remediation Time |
|----------|------------------------|
| Critical | 24 to 48 hours |
| High | 7 days |
| Medium | 30 days |
| Low | 90 days |

These targets are guidelines, not arbitrary deadlines. If your team needs more time for a specific finding due to operational constraints, the right approach is to communicate that and work with us on a plan — which might include compensating controls to reduce risk in the interim.

---

## Remediation

**Do you fix vulnerabilities or just tell us about them?**

Our primary role is to identify, analyze, and prioritize vulnerabilities and to guide your team through what needs to be done. The actual fixes — applying software patches, changing system configurations, updating firewall rules — are carried out by your internal IT team or your IT managed services provider.

This division makes sense for a few reasons: your IT team knows your systems, controls your change management processes, and is accountable for the stability of your environment. Our job is to make sure they know exactly what to fix, why it matters, and how to do it.

In some cases, we can assist with remediation directly — this depends on your engagement scope. Ask your consultant if hands-on remediation support is something you need.

---

**What if we cannot patch a system because it would break something?**

This is one of the most common situations we encounter, and there are practical options:

- **Compensating controls:** We can recommend alternative safeguards — for example, restricting network access to the vulnerable system, adding an additional layer of authentication, or enhancing monitoring — that reduce the risk without requiring a patch.
- **Risk acceptance:** If the risk is genuinely low or the compensating controls are strong, we can formally document a risk acceptance decision.
- **Vendor coordination:** If the issue is a vendor product, we can help you understand what the vendor's roadmap looks like and what your options are while you wait for an official fix.
- **Planned maintenance:** Some patches require testing or a maintenance window before they can be applied to production systems. We will work with your schedule.

We will never simply drop a finding because it is inconvenient. We track it, document the reason it has not been resolved, and revisit it regularly.

---

**Who is responsible for actually fixing the issues?**

Accountability for remediation lies with the owners of the affected systems — that is, your internal IT staff, your managed IT provider, or the relevant application or system vendor.

We provide the roadmap. We track progress and follow up. We verify that fixes are applied correctly. But the act of making changes to your systems rests with the people who are authorized and responsible for those systems.

Your consultant will work with you to make sure the right people receive the right information and that nothing falls through the cracks.

---

**What happens if we miss an SLA deadline?**

We understand that IT teams are busy and that not every deadline will be met perfectly. When a remediation target is missed, we:

- Flag the overdue finding in your next report
- Follow up to understand the reason and whether additional support is needed
- Document the delay and the current plan in your records (which matters for auditors and insurers)
- In the case of overdue Critical or High findings, escalate our communication to ensure leadership is aware

Missing a deadline does not result in a penalty, but it does increase your risk exposure — and it creates a documented record that the finding was known and unaddressed. That documentation can matter in a regulatory audit or an insurance claim.

---

## Our Data and Confidentiality

**What data do you collect about our environment?**

We collect information about your technology environment — the types of systems you operate, software versions, configuration details, and the vulnerabilities we identify. We do not intentionally collect business data such as customer records, financial transactions, or employee personal information.

If our scanning tools encounter sensitive data in the course of their operation (for example, detecting that a database is publicly accessible), we document the exposure without exfiltrating the data itself.

Everything we collect is documented in our engagement agreement and handled according to strict data handling policies.

---

**How is our sensitive information protected?**

All information about your environment is treated as confidential. Our data handling practices include:

- Encrypted storage for all client data
- Access restricted to the specific team members working on your engagement
- Secure transmission for all reports and communications
- Non-disclosure agreements in place before engagement work begins

We are happy to share our full data handling policy on request.

---

**Who on your team has access to our systems?**

Access to your systems is limited to the consultants and analysts directly assigned to your engagement. We maintain a clear record of who has been granted access, what level of access they have, and for what purpose.

At the start of the engagement, we will document all personnel with access and the specific credentials or accounts granted. You can request an access review at any time.

All access is revoked at the conclusion of the engagement unless otherwise agreed.

---

**How long do you retain our data?**

Our standard retention period for client engagement data is defined in your service agreement. Generally, we retain data for the duration of the engagement plus a defined post-engagement period (commonly one to three years) for audit and continuity purposes.

If you require a shorter retention period, or if you need us to certify that data has been deleted at engagement end, please raise this with your consultant during onboarding so it can be formalized in your agreement.

---

## Communication and Escalation

**How will you communicate with us during the engagement?**

Day-to-day communication typically happens via email or your preferred collaboration tool (Microsoft Teams, Slack, etc.). Your consultant will establish communication norms during onboarding.

For critical findings or urgent matters, we will call — not just email. Make sure we have current phone numbers for your primary contacts.

All significant findings and decisions are documented in writing, either in formal reports or in tracked correspondence.

---

**What happens if there is a security incident during our engagement?**

If we detect or are notified of an active security incident during the engagement, we immediately shift focus to support you in responding. This includes:

- Alerting your designated contacts and escalating to appropriate leadership
- Sharing relevant findings that may be related to the incident
- Providing guidance on immediate containment steps
- Coordinating with any incident response resources you have in place

If your engagement includes incident response support, we will be directly involved in the response effort. If it does not, we will still provide all relevant information to support whoever is leading the response.

---

**How do we escalate an urgent issue to your team?**

Every client has a designated primary consultant and an escalation contact. Both are provided at the start of the engagement. For urgent matters — including critical findings, active incidents, or situations requiring an immediate decision — use the direct contact methods (phone) rather than waiting for email.

If for any reason your primary consultant is unreachable, the escalation contact at our firm can always be reached. We will make sure you always have a backup contact who knows your account.

---

**How often will we have meetings?**

Standard meeting cadence for most engagements includes:

- **Monthly check-in:** A brief update on scanning activity, remediation progress, and any emerging concerns.
- **Quarterly review:** A more comprehensive session covering trends, report walkthrough, priority setting for the next quarter, and strategic discussion.
- **Ad hoc calls:** Any time a significant finding or question warrants it — you never need to wait for a scheduled meeting.

If you would like more frequent touchpoints, especially early in the engagement, just ask. We would rather meet more often during onboarding than have you feel out of the loop.

---

## Pricing and Renewals

**How is pricing structured?**

Pricing for our engagements is typically structured in one of two ways:

- **Subscription/retainer model:** A fixed monthly or annual fee that covers a defined set of services — scanning cadence, reporting, and a set number of consulting hours.
- **Project-based pricing:** A fixed fee for a defined scope of work with a clear deliverable, such as a one-time vulnerability assessment or a penetration test.

Most ongoing clients are on a subscription model, which provides predictability for budgeting purposes.

---

**What is included versus what costs extra?**

Your engagement agreement specifies exactly what is included in your subscription. Common inclusions are:

- Regular vulnerability scanning of agreed-upon scope
- Scheduled reports (executive and technical)
- Critical finding notifications
- Monthly or quarterly review meetings
- Remediation guidance and verification scanning

Common add-ons that fall outside a standard engagement include:

- Penetration testing
- Cloud environment coverage beyond the original scope
- Additional log sources or SIEM integrations
- Remediation support (hands-on fixing)
- Compliance-specific assessments or audit support

If you are ever unsure whether something is included, ask before assuming. We would rather clarify upfront than have a billing surprise later.

---

**What happens at the end of our contract term?**

Approximately 60 to 90 days before your contract renewal date, your consultant will initiate a renewal discussion. This is a good opportunity to:

- Review how the engagement has gone and whether the scope still fits your needs
- Discuss any changes to your environment that should be reflected in the new term
- Explore whether additional services would be beneficial
- Negotiate pricing if your needs have changed significantly

At the end of the contract term, our access to your systems is terminated and data retention follows the terms in your agreement. We do not retain access beyond the agreed period.

---

**How do we expand the engagement if our needs grow?**

Your security needs will evolve as your business grows and as your environment changes. Expanding the engagement is straightforward — we scope the additional work, agree on pricing, and add it to your agreement.

Common expansion scenarios include extending scanning coverage to new systems or cloud environments, adding a penetration test, connecting additional log sources to your security monitoring, or increasing meeting frequency.

For a full overview of what expanded capabilities can do for your business, see the companion document: *Expanding Your Security Program — A Guide to What's Possible.*
