# Understanding Risk Ratings — What Critical, High, Medium, and Low Mean for Your Business

---

## Introduction: Why Risk Ratings Exist

When we assess your environment, we typically find dozens — sometimes hundreds — of vulnerabilities. Not all of them are equally dangerous. If we treated every finding with the same level of urgency, your team would be overwhelmed and the most dangerous issues could get lost in the noise.

Risk ratings exist to give us a shared language for communicating how serious a problem is — and how quickly it needs to be addressed.

We use an industry-standard scoring system called CVSS (Common Vulnerability Scoring System), which rates vulnerabilities on a scale from 0 to 10. We then translate those scores into four severity categories: Critical, High, Medium, and Low. Each one carries a clear meaning, a defined response time, and specific guidance on who needs to be informed.

This document explains what each rating means in plain business terms — not technical jargon.

---

## Critical — Severity Score 9.0 to 10.0

### What It Means Technically
A Critical vulnerability scores between 9.0 and 10.0 on the CVSS scale. This means it is easy to exploit, requires little to no special skill or access, and can cause severe, widespread damage.

### What It Means in Plain English
A Critical vulnerability is a direct, open path into your most important systems. In many cases, automated tools used by criminals can find and exploit these vulnerabilities with no human effort required. These are not theoretical risks — they are active dangers.

### Business Analogy
A Critical vulnerability is like having a bank vault door standing wide open, with a sign on the street outside directing people to it. The barrier between attackers and your most sensitive assets has effectively been removed.

### Real-World Example of What Could Happen
A Critical vulnerability in an internet-facing server could allow an attacker to take complete control of that server, move into your internal network, install ransomware across your entire organization, and exfiltrate customer and financial data — all within hours of the vulnerability being discovered.

### Expected Response
**Immediate action required. Target remediation: 24 to 48 hours.**

We will notify you the moment a Critical finding is identified. We do not wait for a scheduled report. Your IT team should treat this with the same urgency as a detected break-in.

### Who Needs to Know
- Executive leadership (CEO, CFO, COO as appropriate)
- IT leadership and the team responsible for the affected system
- Legal or compliance teams if regulated data is at risk
- Cyber insurance carrier, depending on your policy requirements

### Business Impact
A single exploited Critical vulnerability can result in:
- Ransomware payments ranging from tens of thousands to millions of dollars
- Full operational shutdown while systems are rebuilt
- Regulatory fines and mandatory breach notifications to customers
- Long-term reputational damage and customer attrition
- Loss of cyber insurance coverage upon renewal

---

## High — Severity Score 7.0 to 8.9

### What It Means Technically
A High vulnerability scores between 7.0 and 8.9 on the CVSS scale. It is serious and exploitable, though it may require more effort, specific conditions, or limited access to carry out compared to a Critical vulnerability.

### What It Means in Plain English
A High vulnerability represents a significant security weakness that a skilled or determined attacker could use to gain unauthorized access or cause real harm. It does not rise to the level of "door standing wide open," but the risk is substantial and needs to be addressed promptly.

### Business Analogy
A High vulnerability is like a broken deadbolt on your front door. The door still closes, and most passersby won't notice. But anyone who specifically wants to get in has a clear path, and it won't take them long.

### Real-World Example of What Could Happen
A High vulnerability in your VPN (the system your employees use to connect to company resources remotely) could allow an attacker to intercept employee credentials, log in as a legitimate user, and access internal systems, files, or email without detection.

### Expected Response
**Target remediation: 7 days.**

These should be treated as urgent but do not require the same immediate all-hands response as a Critical finding. Your IT team should schedule remediation within the business week.

### Business Impact
- Unauthorized access to internal systems or sensitive data
- Credential theft leading to further compromise
- Regulatory exposure if sensitive customer or financial data is involved
- Potential for escalation to a more severe incident if not addressed

---

## Medium — Severity Score 4.0 to 6.9

### What It Means Technically
A Medium vulnerability scores between 4.0 and 6.9 on the CVSS scale. It represents a real security weakness, but exploitation typically requires specific conditions — for example, an attacker already having partial access, or the vulnerability only being reachable from inside your network.

### What It Means in Plain English
Medium vulnerabilities are genuine concerns that belong on your remediation list. They are not emergencies on their own, but they can contribute to a larger attack chain — where an attacker uses multiple smaller weaknesses together to achieve something more serious. Leaving many Medium findings unaddressed over time creates compounding risk.

### Business Analogy
A Medium vulnerability is like a window latch that does not fully catch. On its own, a determined attacker might use it, but it is not the most obvious entry point. Left unaddressed, it becomes part of a pattern of neglect that increases overall risk.

### Real-World Example of What Could Happen
A Medium vulnerability in an internal application could allow a user who should not have access to view records they are not authorized to see — a data exposure issue that could trigger privacy regulation requirements or damage customer trust.

### Expected Response
**Target remediation: 30 days.**

These should be scheduled into your regular IT maintenance and patching cycles within the month.

### Business Impact
- Incremental expansion of an attacker's access once they are inside your network
- Regulatory exposure from data access control failures
- Reputational risk if combined with other vulnerabilities and exploited
- Audit findings if unaddressed in a regulated environment

---

## Low — Severity Score 0.1 to 3.9

### What It Means Technically
A Low vulnerability scores between 0.1 and 3.9 on the CVSS scale. Exploitation is very difficult, requires highly specific circumstances, or produces limited impact even if successfully exploited.

### What It Means in Plain English
Low vulnerabilities are minor weaknesses that represent minimal immediate risk. On their own, they are unlikely to cause significant harm. They are worth tracking and addressing as part of good security hygiene, but they should not divert resources from higher-priority findings.

### Business Analogy
A Low vulnerability is like a fence around your property that is slightly shorter than recommended — it is a marginal reduction in your overall security posture, but it is not what an attacker is going to prioritize.

### Expected Response
**Target remediation: 90 days.**

Address these as part of routine maintenance and improvement cycles. They should not be ignored indefinitely, but they do not require urgent action.

### Business Impact
- Minimal on their own
- May contribute marginally to overall attack surface
- Could become relevant if your environment changes and the vulnerability becomes easier to exploit

---

## Risk Rating Summary Table

| Severity | CVSS Range | Response Time | Who Gets Notified | Example Business Impact |
|----------|------------|---------------|-------------------|------------------------|
| Critical | 9.0 – 10.0 | 24–48 hours | Executives, IT leadership, Legal/Compliance | Ransomware, full data breach, operational shutdown |
| High | 7.0 – 8.9 | 7 days | IT leadership, System owners | Credential theft, unauthorized system access |
| Medium | 4.0 – 6.9 | 30 days | IT team, Application owners | Data exposure, expanded attacker access |
| Low | 0.1 – 3.9 | 90 days | IT team | Minimal direct impact; contributes to overall risk |

---

## How We Use Risk Ratings to Help You Make Decisions

Risk ratings are not just labels — they are a tool for making smarter decisions about where to invest your time and resources.

**Prioritization**
When your IT team has a list of 50 vulnerabilities to address, risk ratings tell them where to start. A Critical finding on your payment processing system takes precedence over a Low finding on an internal development server.

**Budget Allocation**
If you are deciding whether to invest in security improvements, risk ratings help frame the conversation. A cluster of Critical and High findings on internet-facing systems makes a clear case for prioritizing that investment.

**Risk Acceptance**
Sometimes a fix is not immediately feasible — because of operational constraints, vendor limitations, or cost. In those cases, risk ratings help determine whether a formal risk acceptance decision is appropriate, and at what level of leadership that decision should be made. We generally do not recommend accepting Critical or High risks without a clear remediation plan and compensating controls in place.

**Demonstrating Progress**
As your program matures, reducing the number of open Critical and High findings is the clearest measure of progress. We track these numbers over time and include trends in your executive reports.

---

## What "Risk Accepted" Means — and When It Is Appropriate

Sometimes a vulnerability cannot be fixed right away. The system is too old to patch, the vendor has not released a fix, or applying the patch would break a critical business application. In these cases, rather than leaving the finding in limbo, we can formally document a risk acceptance.

A risk acceptance is a documented, leadership-approved decision to acknowledge that a vulnerability exists, understand the potential consequences, and choose to accept the risk — typically because compensating controls are in place or the remediation cost outweighs the risk.

Risk acceptance is appropriate when:
- The vulnerability is Low or Medium severity with limited exposure
- Compensating controls meaningfully reduce the likelihood of exploitation
- A vendor fix is expected within a defined timeframe
- The cost or operational disruption of remediation is disproportionate to the risk

Risk acceptance is generally not appropriate for Critical or High vulnerabilities without strong compensating controls and executive sign-off.

---

## Questions to Ask When You See a Critical or High Finding

When we present a Critical or High finding, here are useful questions to ask your team and ours:

- Is this vulnerability reachable from the internet, or only from inside our network?
- Is there evidence this vulnerability is being actively exploited by attackers in the wild?
- What data or systems could be accessed if this were exploited?
- What do we need to do to fix it, and how long will that take?
- Is there anything we can do right now to reduce the risk while the full fix is being applied?
- Does this trigger any regulatory notification requirements?
- Does our cyber insurance carrier need to be informed?
