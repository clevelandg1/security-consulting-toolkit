# Renewal Conversation Prep Sheet

---

**Client Name:** [Client Name]
**Renewal Date:** [Renewal Date]
**Current Engagement Period:** [Start Date] – [End Date]
**Consultant:** [Consultant Name]
**Prep Sheet Prepared:** [Date]
**Renewal Meeting Scheduled:** [Date / Time]

---

## How to Use This Template

This prep sheet is designed to be completed before a renewal conversation and used as a facilitation guide during the meeting. Work through each section in order. Sections 1–5 are completed before the meeting using engagement records. Sections 6–9 are used during and after the conversation.

The goal of the renewal conversation is not simply to secure a signature — it is to demonstrate the value delivered, align on what is still open, and position the next engagement period as a continuation of a risk reduction journey the Client has already started.

---

## Section 1: Value Delivered Summary

Use this table to document measurable improvements over the engagement period. Pull data from monthly vulnerability reports, meeting notes, and the action item tracker.

| Metric | At Engagement Start | Current State | Improvement |
|--------|--------------------:|--------------|-------------|
| Total vulnerabilities identified (open count) | [#] | [#] | [↓ # / ↑ #] |
| Critical vulnerabilities open | [#] | [#] | [↓ # / ↑ #] |
| High vulnerabilities open | [#] | [#] | [↓ # / ↑ #] |
| Mean time to remediate — Critical (days) | [# days] | [# days] | [↓ # days] |
| Mean time to remediate — High (days) | [# days] | [# days] | [↓ # days] |
| SLA compliance % — Critical | [%] | [%] | [↑ %] |
| SLA compliance % — High | [%] | [%] | [↑ %] |
| Assets in scope / scanned (coverage %) | [%] | [%] | [↑ %] |
| Log sources active in SIEM | [#] | [#] | [↑ #] |
| Documented IR plan in place | [Yes / No / Partial] | [Yes / No / Partial] | [Status change] |
| [Custom metric relevant to this client] | [Baseline] | [Current] | [Delta] |

**Notes on Data Sources:**

> [Document where this data was pulled from — e.g., "Critical vuln count pulled from Tenable monthly report, October through [Month]." This ensures the data is defensible in the conversation.]

---

## Section 2: Posture Improvement Highlights

Document 3–5 specific, meaningful wins from the engagement period. Write each one using business impact language — frame improvements in terms of risk reduction, operational efficiency, compliance readiness, or business protection. Avoid purely technical language.

**Win 1:**

> **What changed:** [e.g., Vulnerability remediation SLAs were formally defined and implemented for the first time.]
> **Business impact:** *[e.g., "Critical vulnerabilities are now remediated an average of 22 days faster than at engagement start, reducing the window of exploitability for your most business-critical systems."]*

---

**Win 2:**

> **What changed:** [e.g., Four new log sources were onboarded into the SIEM, including cloud workloads and the identity provider.]
> **Business impact:** *[e.g., "Your security team now has visibility into authentication activity and cloud access events that were previously blind spots — events that are commonly involved in credential-based attacks."]*

---

**Win 3:**

> **What changed:** [e.g., Asset inventory was updated and criticality classifications were applied to 95% of the asset base.]
> **Business impact:** *[e.g., "Remediation teams can now prioritize patching for business-critical systems first, reducing effort spent on lower-priority assets and ensuring your most important systems are protected."]*

---

**Win 4:**

> **What changed:** [e.g., IR plan was reviewed, updated, and tested via a tabletop exercise.]
> **Business impact:** *[e.g., "Your team now has a practiced, tested response process — which means faster containment and reduced damage in the event of an actual incident."]*

---

**Win 5:**

> **What changed:** [e.g., [Compliance framework] gap assessment completed; 12 priority gaps closed.]
> **Business impact:** *[e.g., "You are now materially better positioned for your upcoming [SOC 2 / PCI / HIPAA] audit, with documented evidence of continuous security improvement."]*

---

## Section 3: Remaining Gap Analysis

Be direct and honest about what is still open. Framing remaining gaps as reasons for renewal — rather than failures — is a core element of the renewal conversation.

| Gap | Why It Remains Open | Risk if Left Unaddressed | Recommended Path Forward |
|-----|--------------------|--------------------------|--------------------------|
| [e.g., Cloud workload visibility — GCP not yet covered] | [e.g., GCP onboarding deprioritized in favor of critical vuln backlog reduction] | [e.g., Unmonitored cloud workloads represent a blind spot for detection and compliance] | [e.g., Prioritize GCP log source onboarding in Q1 of renewal period] |
| [e.g., High vulnerability backlog still elevated] | [e.g., Remediation capacity constrained by IT team bandwidth] | [e.g., Prolonged exposure window for unpatched systems increases breach likelihood] | [e.g., Introduce remediation workflow integration with Jira to improve throughput] |
| [e.g., External attack surface not formally reviewed] | [e.g., Scope did not include external scanning; advisory only] | [e.g., Internet-exposed assets may have unidentified vulnerabilities] | [e.g., Add EASM review to next engagement scope] |
| [e.g., Application security testing not performed] | [e.g., Out of scope for this engagement period] | [e.g., Web-facing applications represent a common attack entry point] | [e.g., Evaluate app security testing as an expansion service] |
| [Additional gap] | | | |

**Framing Note:**

> *Use this language in the conversation: "We've made strong progress — but security is not a destination. The gaps that remain aren't signs that the engagement hasn't worked; they're exactly why continued advisory engagement is valuable. Here's what we still need to close, and here's the plan."*

---

## Section 4: Upcoming Initiatives & Business Alignment

Use these questions to understand what is changing in the Client's business and ensure the renewal scope remains aligned to future priorities.

**Questions to Ask:**

- [ ] What are your top security priorities for the next 12 months? Have they shifted since we started?
  - Notes: _______________________________________________

- [ ] Are there any new cloud initiatives, infrastructure migrations, or technology changes planned?
  - Notes: _______________________________________________

- [ ] Are there compliance deadlines, audits, or certifications coming up in the next 12 months?
  - Notes: _______________________________________________

- [ ] Are there any planned acquisitions, mergers, or significant changes to the business?
  - Notes: _______________________________________________

- [ ] Is there any change in security team staffing — additions, departures, or restructuring?
  - Notes: _______________________________________________

- [ ] Has leadership's perspective on security investment or risk tolerance changed?
  - Notes: _______________________________________________

- [ ] Are there new business lines, products, or customer segments that bring new data types or compliance obligations?
  - Notes: _______________________________________________

**Summary of Upcoming Priorities:**

> [Summarize what the Client shared — this will directly inform the renewal scope and framing]

---

## Section 5: Platform Expectations Check

Understanding the Client's relationship with their current security tools is important for identifying frustration points and potential expansion opportunities.

**Questions to Ask:**

- [ ] Overall, are you getting the value you expected from [primary security tool / SIEM / vuln scanner]?
  - Notes: _______________________________________________

- [ ] Are there features or capabilities in your current tools that are not being used effectively?
  - Notes: _______________________________________________

- [ ] Are there reporting or dashboard capabilities you wish you had?
  - Notes: _______________________________________________

- [ ] Are there workflows between your security tools and IT operations (ticketing, change management) that feel manual or inefficient?
  - Notes: _______________________________________________

- [ ] Is there a tool gap you have been aware of but have not addressed?
  - Notes: _______________________________________________

**Platform Notes:**

> [Document any tool frustrations, gaps, or opportunities for improvement]

---

## Section 6: Renewal Framing

Use the following talking points to position the renewal as a continuation of the risk reduction journey — not a subscription renewal.

### Core Message

*"You started this engagement with [X] critical vulnerabilities open, no formal SLAs, and significant blind spots in your log coverage. Today, your critical backlog is [Y% lower], your mean time to remediate has dropped by [X days], and you have [N] more log sources providing detection coverage. That progress happened because of consistent, structured advisory engagement — and it stops without it."*

### Supporting Talking Points

**On progress made:**
> *"The work we've done together has materially changed your risk exposure. The improvements in [metric 1] and [metric 2] represent real, measurable reduction in the likelihood and impact of a security incident."*

**On remaining gaps:**
> *"There are still open gaps — and that's normal at this stage. What matters is that we have a clear plan to close them. The next engagement period is where we finish the job on [specific gap 1] and [specific gap 2]."*

**On the cost of not renewing:**
> *"The risk doesn't pause between engagements. Vulnerabilities continue to accumulate. Threat actors don't wait. Without continued advisory oversight, the progress we've made can erode — particularly in [area most at risk of regression, e.g., vuln backlog if patching slows]."*

**On alignment to upcoming initiatives:**
> *"You mentioned [new cloud initiative / upcoming audit / compliance deadline]. That's exactly the kind of change that requires security advisory support. We can build that directly into the renewal scope."*

**On value relative to cost:**
> *"Compare the investment in this engagement to the cost of a single security incident in your environment — the average cost of a data breach in [industry] is [$X]. Continued advisory engagement is one of the most cost-effective risk mitigation measures available."*

---

## Section 7: Expansion Opportunities

Based on the engagement to date and the renewal conversation, identify which expansion services are a good fit for this Client. Check all that apply and prepare a brief pitch for each selected item.

**CAF Upsell Paths:**

- [ ] **Additional Log Sources**
  *Pitch: "We currently have [N] log sources in your SIEM. Adding [specific sources — e.g., email security platform, VPN, cloud storage] would close [specific detection gap] and improve your coverage score significantly."*
  - Priority: [ ] High  [ ] Medium  [ ] Low
  - Notes: _______________________________________________

- [ ] **Cloud Workload Visibility — AWS**
  *Pitch: "Your AWS environment is currently not feeding into your SIEM. Adding CloudTrail, GuardDuty, and VPC Flow Logs would give you visibility into cloud access, API activity, and network behavior — critical for detecting compromises in cloud-hosted workloads."*
  - Priority: [ ] High  [ ] Medium  [ ] Low
  - Notes: _______________________________________________

- [ ] **Cloud Workload Visibility — Azure**
  *Pitch: "Extending Defender for Cloud advisory and onboarding Azure activity logs into your SIEM would provide unified visibility across your hybrid environment."*
  - Priority: [ ] High  [ ] Medium  [ ] Low
  - Notes: _______________________________________________

- [ ] **Cloud Workload Visibility — GCP**
  *Pitch: "GCP workloads currently lack centralized monitoring. Adding Cloud Audit Logs and Security Command Center findings to your SIEM closes a significant blind spot."*
  - Priority: [ ] High  [ ] Medium  [ ] Low
  - Notes: _______________________________________________

- [ ] **Application Security Testing**
  *Pitch: "Your web-facing applications represent a common attack vector that vulnerability scanning doesn't fully cover. Adding application security testing — even a focused DAST scan of your most critical apps — provides a layer of assurance that your current program doesn't include."*
  - Priority: [ ] High  [ ] Medium  [ ] Low
  - Notes: _______________________________________________

- [ ] **Threat Detection & Response Advisory**
  *Pitch: "Beyond log collection, we can build out your detection rule library and alert response playbooks — turning your SIEM from a log repository into an active detection engine."*
  - Priority: [ ] High  [ ] Medium  [ ] Low
  - Notes: _______________________________________________

- [ ] **Reporting Automation**
  *Pitch: "The metrics we're producing manually each month can be automated — saving your team time and giving leadership on-demand visibility into security posture. We can help design and implement a reporting dashboard."*
  - Priority: [ ] High  [ ] Medium  [ ] Low
  - Notes: _______________________________________________

- [ ] **Remediation Workflow & Ticketing Integration**
  *Pitch: "Connecting your vulnerability management platform directly to [ServiceNow / Jira] would automate ticket creation and tracking for remediation items — reducing the manual overhead for your IT team and improving SLA compliance."*
  - Priority: [ ] High  [ ] Medium  [ ] Low
  - Notes: _______________________________________________

**Expansion Summary:**

> [Summarize which 1–3 expansion opportunities to lead with in this conversation, and why they are the right fit for this Client at this time]

---

## Section 8: Proposed Renewal Terms

Use this section to outline the proposed terms for the next engagement period before the meeting. Adjust based on the conversation.

| Item | Current Engagement | Proposed Renewal |
|------|--------------------|------------------|
| Engagement Period | [Start] – [End] | [Proposed Start] – [Proposed End] |
| Monthly Retainer | $[X,XXX] / month | $[X,XXX] / month |
| Advisory Hours / Month | [X] hours | [X] hours |
| Monthly Advisory Meetings | [#] per month | [#] per month |
| Quarterly Business Reviews | [#] per year | [#] per year |
| Expansion Services Added | N/A | [List any new services proposed] |
| Pricing Adjustment | N/A | [e.g., CPI adjustment / discount for multi-year / expansion package pricing] |
| Proposed Contract Term | [12 months] | [12 / 24 months] |

**Pricing Notes:**

> [Space for any flexibility, discount considerations, or multi-year incentive notes]

---

## Section 9: Decision & Next Steps

Use this section during the closing portion of the renewal conversation to confirm the path forward.

**Decision Outcome:**

- [ ] Renewal confirmed — proceed to contract
- [ ] Renewal likely — Client needs [X] to make final decision
- [ ] Renewal uncertain — Client has concerns (document below)
- [ ] Not renewing — document reason below

**Client Concerns / Objections Raised:**

> [Document any objections, budget concerns, or hesitations so they can be addressed]

**Next Steps:**

| Action Item | Owner | Due Date |
|-------------|-------|----------|
| Send renewal proposal / updated SOW | [Consultant] | [Date] |
| Follow up on outstanding Client questions | [Consultant] | [Date] |
| Obtain Client signature on renewal agreement | [Client POC] | [Date] |
| Confirm engagement continuity — no service gap | [Consultant] | [Date] |
| Schedule kickoff for renewal period (if new scope) | [Both parties] | [Date] |
| [Additional action item] | | |

**Renewal Meeting Notes:**

> [Space for free-form notes from the renewal conversation]

---

*Renewal Prep Sheet Version: [1.0] | Prepared by: [Consultant Name] | Client: [Client Name] | Renewal Date: [Date]*
