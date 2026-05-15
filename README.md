# SimplifyIAM IAM Implementation Portfolio

**Cohort:** SimplifyIAM Live Cohort 1  
**Name:** Uzo Bolarinwa  
**LinkedIn:** [linkedin.com/in/uzobolarinwa](https://linkedin.com/in/uzobolarinwa)  
**GitHub:** [github.com/uzobola](https://github.com/uzobola)  
**Completed:** In progress - May 2026

---

## What I Built

Over five live Saturday sessions I built a complete IAM environment from scratch using midPoint, a simulated HR source, and a 389 Directory Server. The environment runs on a dedicated cloud server and replicates how IAM provisioning works in a real enterprise engagement — from HR-triggered lifecycle events through to named accounts in a target directory.

This repository documents my configuration, architectural decisions, and analysis for each session. It is intended as portfolio evidence for  IAM implementation roles, Cloud Security and GRC Engineering roles, and is designed to bridge hands-on IGA implementation with enterprise-scale IAM architecture.

---

## Environment

| Component | Purpose |
| --- | --- |
| midPoint | IGA platform — identity lifecycle, provisioning, reconciliation, access governance |
| SimplifyHR (Flask) | HR source of truth — simulates enterprise HRIS (Workday / SAP SuccessFactors equivalent) |
| 389 Directory Server | Target directory — named user accounts provisioned here (Active Directory equivalent) |
| Auth0 | Access management — OIDC and SAML federation (covered in Week 4) |


## Session Deliverables

---

### Saturday 1 — IAM Architecture, Environment and Stakeholder Mapping

**Scenario:** Acting as the IAM consultant brought in to build SimplifyTech's identity infrastructure from scratch.

#### Architecture Diagram

```
SimplifyHR (Identity Source — authoritative source of truth)
        |
        |  [midPoint polls SimplifyHR for changes]
        v
SimplifyIAM / midPoint (IGA Platform)
  - Detects Joiner / Mover / Leaver events
  - Applies provisioning rules and attribute mappings
  - Enforces RBAC assignments
  - Generates audit evidence
        |
        v
389 Directory Server (Target System)
  - Named user accounts created/modified/disabled here
  - Browsable via phpLDAPadmin
```

#### Screenshots
[SimplifyIAM / midPoint (IGA Platform)](screenshots/midpoint_dashboard.png)
[SimplifyHR(Identity Source)](screenshots/simplifyhr_dashboard.png)
[389 Directory Server](screenshots/389_directory_server.png) 


**Enterprise equivalent mapping:**

| Lab Component | Enterprise Equivalent | What It Does |
| --- | --- | --- |
| SimplifyHR | Workday, SAP SuccessFactors, BambooHR | System of record for employee identities |
| midPoint | SailPoint IdentityNow, Saviynt | IGA — lifecycle governance and provisioning |
| 389 Directory Server | Active Directory, Okta Universal Directory | Target system where accounts live |
| (Week 4) Auth0 | Okta, Entra ID | Access management — authentication, SSO, MFA |

---

## What I Learned

#### The Four IAM Layers

A key architectural distinction from this session — enterprise IAM is not one system. It is four distinct capability layers:

| Layer | What It Owns | Enterprise Tools | AWS Equivalent | Microsoft Equivalent |
| --- | --- | --- | --- | --- |
| **IGA** | Identity lifecycle, access governance, audit evidence, SoD | SailPoint, Saviynt, midPoint | IAM + Access Analyzer (governance) | Entra ID Governance (Lifecycle Workflows, Entitlement Management, Access Reviews) |
| **Access Management** | Authentication, SSO, MFA, session tokens | Okta, Entra ID, Ping | Cognito, IAM Identity Center | Entra ID (Conditional Access, SSO, MFA) |
| **PAM** | Privileged credential vaulting, just-in-time access, session recording | CyberArk, BeyondTrust | Secrets Manager, SSM Session Manager | Entra PIM (Privileged Identity Management) |
| **CIAM** | External/customer identity, registration, consent, B2C federation | Auth0, Ping, ForgeRock | Cognito User Pools | Azure AD B2C / Entra External ID |

> **NOTE: IGA and Access Management are not the same thing.** IGA answers: *who should have access, and can we prove it?* Access Management answers: *are you who you say you are, and can you get in right now?* Both layers are required. midPoint handles IGA. Auth0 (Week 4) handles Access Management. Conflating them is one of the most common scoping mistakes in enterprise IAM engagements.


#### Stakeholder Mapping

A critical consulting skill introduced in this session: different stakeholders require different communication styles. The same IAM requirement described in technical terms to HR will produce confusion; described in business terms to a security engineer will produce the wrong implementation.

| Stakeholder | What They Care About | How to Speak to Them |
| --- | --- | --- |
| HR | Employee data accuracy, onboarding speed, offboarding compliance | "When HR adds someone, their accounts appear automatically. When they leave, access is revoked the same day." |
| InfoSec | Least privilege, audit trails, SoD enforcement, breach blast radius | "Every access grant and revocation is logged. We can produce evidence for any audit finding." |
| App Owners | Their application isn't broken, access is correct, no support tickets | "We provision to your app via a connector. You define the roles. We enforce them." |
| Auditors | Control evidence, exception documentation, certification records | "Every access event maps to a control. Certifications are scheduled and timestamped." |
| Business / Programme Lead | Cost, timeline, risk reduction | "This eliminates the manual account creation process and the audit risk of stale access." |

**Key principle:** Requirements drive every architecture decision. Arrive at stakeholder workshops with structured discovery questions prepared. Map pain points to business objectives before touching a configuration screen.

#### What I Built

Deployed and verified a three-component enterprise IAM lab environment on a dedicated cloud server. Mapped the architecture across IGA, access management, PAM, and CIAM domains — establishing the conceptual framework that all subsequent provisioning work builds on.


#### Resume Bullet

> Deployed and verified a three-component enterprise IAM lab environment (midPoint IGA, HR source simulator, 389 Directory Server) on a cloud server; mapped architecture across IGA, access management, PAM, and CIAM domains as foundation for full JML lifecycle implementation.

---

## My Transformation

**Where I am starting - Week 1 :** Cloud security engineer with AWS certifications (Solutions Architect, Security Specialty) and hands-on experience building security automation infrastructure — a 16-control GRC compliance platform, an IAM cross-account detection pipeline, and a Zero Trust serverless architecture. Foundation in AWS-native IAM and detection engineering, but no hands-on experience with enterprise IGA platforms or the JML lifecycle that sits upstream of the controls I was already automating.

**Where I am now:** Ongoing ...

**Roles I am targeting but not limited to :**  IAM Solutions Engineer, IAM Engineer, Cloud Security Engineer, GRC Engineer at enterprise security vendors, AWS, or major AWS partners. 

---


