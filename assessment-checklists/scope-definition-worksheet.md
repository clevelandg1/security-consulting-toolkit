# Scope Definition Worksheet

**Client Name:** [Client Name]
**Date:** [Date]
**Engagement Type:** [Engagement Type — e.g., Vulnerability Management Advisory / Security Assessment / Penetration Test]
**Lead Consultant:** [Lead Consultant]
**Engagement ID:** [Engagement ID]
**Revision:** 1.0

---

## Purpose and Instructions

This worksheet defines the technical and organizational scope of the engagement. It establishes which assets, environments, networks, and processes are in scope for security activities, and documents the boundaries that must be observed throughout the engagement.

**This document must be completed and signed by both the consulting team and an authorized client representative before any active scanning, testing, or assessment work begins.**

**Instructions:**
1. Complete each section in collaboration with the client's IT and security leadership.
2. Use the asset criticality scale defined in Section 2 consistently throughout the document.
3. Flag any systems requiring special handling in Section 7 before work begins.
4. Any changes to scope after sign-off require a formal scope amendment and updated sign-off.

---

## Section 1: Organization Overview

### 1.1 Basic Organization Information

| Field | Response |
|-------|----------|
| Legal Entity Name | |
| Industry / Sector | |
| Approximate Number of Employees | |
| Approximate Annual Revenue | |
| Number of Physical Locations / Offices | |
| Headquarters Location | |
| Primary IT Contact | |
| Primary Security Contact | |

### 1.2 Regulatory and Compliance Requirements

List all regulatory frameworks, industry standards, or legal obligations that apply to this organization:

| Requirement | Applicable? | Notes |
|-------------|-------------|-------|
| PCI DSS | [ ] Yes [ ] No | |
| HIPAA / HITECH | [ ] Yes [ ] No | |
| SOC 2 Type I / Type II | [ ] Yes [ ] No | |
| ISO 27001 | [ ] Yes [ ] No | |
| NIST CSF | [ ] Yes [ ] No | |
| CMMC (DoD) | [ ] Yes [ ] No | |
| GDPR | [ ] Yes [ ] No | |
| CCPA / State Privacy Laws | [ ] Yes [ ] No | |
| NERC CIP | [ ] Yes [ ] No | |
| FFIEC | [ ] Yes [ ] No | |
| Other: _______________ | [ ] Yes [ ] No | |

### 1.3 IT Environment Overview

Describe the overall composition of the IT environment:

| Environment Type | Percentage of Infrastructure | Notes |
|-----------------|------------------------------|-------|
| On-Premises | _______ % | |
| Cloud (IaaS/PaaS) | _______ % | |
| Hybrid | _______ % | |
| SaaS Applications | _______ % | |
| Remote Workforce | _______ % of workforce | |
| OT / ICS / Industrial | [ ] Yes [ ] No | |

**Additional IT Environment Context:**

_______________________________________________
_______________________________________________

---

## Section 2: Asset Inventory and Criticality

### 2.1 Business Criticality Scale

| Rating | Label | Definition |
|--------|-------|------------|
| 1 | Low | Loss or compromise has minimal business impact; easily recoverable |
| 2 | Low-Medium | Limited business impact; recovery is possible within normal change windows |
| 3 | Medium | Moderate impact; affects a business unit or significant process; recovery within 24–72 hours |
| 4 | High | Significant business impact; affects revenue, operations, or customer data; recovery is complex |
| 5 | Critical | Catastrophic impact if compromised; essential to core business operations, safety, or regulatory compliance |

### 2.2 Asset Categories

For each asset type, provide an estimated count, business criticality rating, and indicate whether the asset type is in scope for this engagement.

| Asset Type | Count (Estimate) | Business Criticality (1–5) | In Scope? | Notes |
|------------|-----------------|---------------------------|-----------|-------|
| Servers — Windows | | | [ ] Yes [ ] No [ ] Partial | |
| Servers — Linux | | | [ ] Yes [ ] No [ ] Partial | |
| Workstations (Desktop) | | | [ ] Yes [ ] No [ ] Partial | |
| Laptops (End-User) | | | [ ] Yes [ ] No [ ] Partial | |
| Network Devices (Routers / Switches) | | | [ ] Yes [ ] No [ ] Partial | |
| Firewalls / UTM Appliances | | | [ ] Yes [ ] No [ ] Partial | |
| Load Balancers | | | [ ] Yes [ ] No [ ] Partial | |
| Storage Arrays / NAS / SAN | | | [ ] Yes [ ] No [ ] Partial | |
| Printers / IoT Devices | | | [ ] Yes [ ] No [ ] Partial | |
| Mobile Devices (Managed) | | | [ ] Yes [ ] No [ ] Partial | |
| Virtual Machines (on-prem hypervisor) | | | [ ] Yes [ ] No [ ] Partial | |
| Containers / Kubernetes Clusters | | | [ ] Yes [ ] No [ ] Partial | |
| Cloud VMs — AWS (EC2) | | | [ ] Yes [ ] No [ ] Partial | |
| Cloud VMs — Azure (Azure VMs) | | | [ ] Yes [ ] No [ ] Partial | |
| Cloud VMs — GCP (Compute Engine) | | | [ ] Yes [ ] No [ ] Partial | |
| SaaS Applications (managed) | | | [ ] Yes [ ] No [ ] Partial | |
| OT / ICS Systems | | | [ ] Yes [ ] No [ ] Partial | |
| **Total Estimated Assets** | | | | |

### 2.3 Critical Asset Identification

List the specific systems, applications, or data repositories that — if compromised, encrypted, or made unavailable — would cause the greatest business impact. These systems receive elevated priority in all assessment and remediation activities.

| System / Application Name | Asset Type | Business Criticality (1–5) | Rationale for Criticality |
|--------------------------|-----------|---------------------------|---------------------------|
| | | | |
| | | | |
| | | | |
| | | | |
| | | | |
| | | | |

**Key Question — Critical Asset Dependencies:**
Are there interdependencies between critical assets (e.g., if System A fails, System B also fails)?

_______________________________________________
_______________________________________________

---

## Section 3: External Asset Visibility and Attack Surface

### 3.1 External-Facing Asset Inventory

Document all known assets that are accessible from the public internet:

| Asset | Type | IP Address / URL | Hosted Where | Last Reviewed |
|-------|------|-----------------|--------------|---------------|
| | Domain / Subdomain | | | |
| | Public IP Address | | | |
| | Internet-Facing Application | | | |
| | API Endpoint | | | |
| | VPN / Remote Access Gateway | | | |
| | Cloud Storage Bucket (S3, Azure Blob, GCS) | | | |
| | Email Gateway / MX Records | | | |
| | Other: _______________ | | | |

### 3.2 External Exposure Discovery Questions

| Question | Response |
|----------|----------|
| Do you have a complete and accurate inventory of all your external-facing assets? | [ ] Yes [ ] No [ ] Unsure |
| When was the last external vulnerability scan or external-facing review conducted? | |
| When was the last external penetration test conducted? | |
| Do you use an Attack Surface Management (ASM) tool? If yes, which one? | |
| Have you had any shadow IT or unknown external exposure incidents in the past 12 months? | [ ] Yes [ ] No — details: |
| Do you monitor for new external asset exposure (e.g., new subdomains, certificates)? | [ ] Yes [ ] No |

### 3.3 External Exposure Risk Rating

Based on the above, assess the current external exposure posture:

**External Exposure Risk Rating:** [ ] Low [ ] Medium [ ] High [ ] Critical

**Rationale:**

_______________________________________________
_______________________________________________

---

## Section 4: Network Segmentation and Architecture

### 4.1 Network Segmentation Assessment

| Question | Response | Details |
|----------|----------|---------|
| Are network zones formally defined and documented? | [ ] Yes [ ] No | |
| Is a DMZ in place for internet-facing systems? | [ ] Yes [ ] No [ ] Partial | |
| Is there network segmentation between critical systems and general corporate networks? | [ ] Yes [ ] No [ ] Partial | |
| Are there flat network areas (no segmentation) in the environment? | [ ] Yes [ ] No | Location: |
| Is there network access control (NAC) in place? | [ ] Yes [ ] No [ ] Partial | |
| Are guest wireless networks isolated from the corporate network? | [ ] Yes [ ] No [ ] N/A | |
| Are OT / ICS networks isolated from corporate IT networks? | [ ] Yes [ ] No [ ] N/A | |
| Is micro-segmentation or zero trust networking in use? | [ ] Yes [ ] No [ ] Partial | |
| Are firewall rules documented and reviewed regularly? | [ ] Yes [ ] No | Last review: |

### 4.2 Network Zone Inventory

List the defined network zones / segments in the environment:

| Zone Name | VLAN / Subnet | Purpose | Criticality | Segmented From Corporate? |
|-----------|--------------|---------|-------------|--------------------------|
| | | | | |
| | | | | |
| | | | | |
| | | | | |
| | | | | |

**Network Architecture Notes:**

_______________________________________________
_______________________________________________

---

## Section 5: Cloud Environment Scope

For each cloud provider in use, define what is in scope for this engagement.

### 5.1 Amazon Web Services (AWS)

| Field | Response |
|-------|----------|
| In use? | [ ] Yes [ ] No |
| Number of AWS accounts in scope | |
| Account IDs in scope | |
| AWS services in scope (check all that apply) | [ ] EC2 [ ] S3 [ ] RDS [ ] Lambda [ ] EKS [ ] ECS [ ] IAM [ ] VPC [ ] CloudTrail [ ] Other: ___ |
| Cloud security tool in place (e.g., Security Hub, Prisma, Wiz) | |
| AWS Security Hub enabled? | [ ] Yes [ ] No |

### 5.2 Microsoft Azure

| Field | Response |
|-------|----------|
| In use? | [ ] Yes [ ] No |
| Number of subscriptions in scope | |
| Subscription IDs in scope | |
| Azure services in scope | [ ] Azure VMs [ ] Azure SQL [ ] Azure Storage [ ] AKS [ ] Azure AD [ ] Defender for Cloud [ ] Other: ___ |
| Cloud security tool in place | |
| Microsoft Defender for Cloud enabled? | [ ] Yes [ ] No |

### 5.3 Google Cloud Platform (GCP)

| Field | Response |
|-------|----------|
| In use? | [ ] Yes [ ] No |
| Number of projects in scope | |
| Project IDs in scope | |
| GCP services in scope | [ ] Compute Engine [ ] GCS [ ] Cloud SQL [ ] GKE [ ] IAM [ ] Cloud Logging [ ] Security Command Center [ ] Other: ___ |
| Cloud security tool in place | |
| Security Command Center enabled? | [ ] Yes [ ] No |

### 5.4 Microsoft 365 / Azure AD

| Field | Response |
|-------|----------|
| In use? | [ ] Yes [ ] No |
| Tenant ID in scope | |
| Services in scope | [ ] Exchange Online [ ] SharePoint [ ] OneDrive [ ] Teams [ ] Azure AD [ ] Intune [ ] Defender for M365 [ ] Other: ___ |
| Conditional Access policies in place? | [ ] Yes [ ] No [ ] Partial |
| Microsoft Secure Score baseline taken? | [ ] Yes [ ] No |

---

## Section 6: Compliance and Regulatory Scope

### 6.1 Applicable Frameworks

| Framework | Applicable? | Most Recent Audit / Certification Date | Current Status | In Scope for This Engagement? |
|-----------|-------------|----------------------------------------|----------------|-------------------------------|
| PCI DSS | [ ] Yes [ ] No | | | [ ] Yes [ ] No |
| HIPAA | [ ] Yes [ ] No | | | [ ] Yes [ ] No |
| SOC 2 | [ ] Yes [ ] No | | | [ ] Yes [ ] No |
| ISO 27001 | [ ] Yes [ ] No | | | [ ] Yes [ ] No |
| NIST CSF | [ ] Yes [ ] No | | | [ ] Yes [ ] No |
| CIS Controls v8 | [ ] Yes [ ] No | | | [ ] Yes [ ] No |
| CMMC | [ ] Yes [ ] No | | | [ ] Yes [ ] No |
| GDPR | [ ] Yes [ ] No | | | [ ] Yes [ ] No |
| NERC CIP | [ ] Yes [ ] No | | | [ ] Yes [ ] No |
| FFIEC | [ ] Yes [ ] No | | | [ ] Yes [ ] No |
| Other: _______________ | [ ] Yes [ ] No | | | [ ] Yes [ ] No |

**Upcoming Audit or Compliance Deadlines:**

| Framework | Audit / Deadline Date | Notes |
|-----------|-----------------------|-------|
| | | |
| | | |

---

## Section 7: Engagement Scope Boundaries

### 7.1 In-Scope Statement

Describe specifically what is in scope for this engagement. Be explicit about environments, asset types, locations, and activities that are authorized.

**In Scope:**

_______________________________________________
_______________________________________________
_______________________________________________
_______________________________________________

### 7.2 Out-of-Scope Statement

Describe specifically what is excluded from this engagement. List systems, environments, or activities that must not be touched, tested, or accessed.

**Out of Scope:**

_______________________________________________
_______________________________________________
_______________________________________________
_______________________________________________

### 7.3 Special Handling Requirements

List any systems or environments that require special care, restricted access, or coordination before any work can begin. This includes production systems with zero-tolerance for disruption, systems covered by special regulatory requirements, or systems with defined change windows.

| System / Environment | Special Requirement | Coordination Required With | Notes |
|---------------------|---------------------|---------------------------|-------|
| | | | |
| | | | |
| | | | |
| | | | |

**Change Window / Maintenance Window Schedule (if applicable):**

| Window Type | Day / Time | Duration | Contact to Notify |
|-------------|------------|----------|-------------------|
| Routine Change Window | | | |
| Emergency Change Window | | | |
| Blackout Period (no changes) | | | |

**Additional Constraints or Requirements:**

_______________________________________________
_______________________________________________

---

## Section 8: Scope Sign-Off

Both parties confirm that this scope definition worksheet accurately reflects the agreed scope of the engagement. Any changes to scope must be documented as a formal amendment to this worksheet and require updated signatures from both parties.

**Consulting Team**

Lead Consultant: _______________________________________________
Title: _______________________________________________
Signature: _______________________________________________
Date: _______________________________________________

**Client Authorization**

Authorized Representative: _______________________________________________
Title: _______________________________________________
Department: _______________________________________________
Signature: _______________________________________________
Date: _______________________________________________

**IT / Security Lead Confirmation (if different from authorized representative):**

Name: _______________________________________________
Title: _______________________________________________
Signature: _______________________________________________
Date: _______________________________________________

---

**Scope Amendment Log** (use if scope changes after initial sign-off)

| Amendment # | Date | Description of Change | Requested By | Approved By |
|-------------|------|-----------------------|--------------|-------------|
| | | | | |
| | | | | |

---

*This worksheet is a binding engagement document. Both parties must retain a signed copy. Contact the engagement manager immediately if scope clarity is needed before work begins.*
