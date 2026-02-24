# Enterprise Identity Governance & Lifetime Automation

## Executive Summary


## Table of Devices
| Device Category | OS / Type | Role in Lab |
| --- | --- | --- |
| Primary Server | Ubuntu Linux | "The ""Vault"" (Identity Audit host)" |
| Mobile Endpoint | iOS / Android | MFA & Conditional Access testing |
| Workstation | macOS / Windows | Primary Staff access testing |
| Legacy Device | Older Tablet/PC | "Risk Isolation & ""Grandfathered"" Access testing" |

## 🏗️ Phase 2 Roadmap: Advanced Identity Governance
*The following objectives are slated for implementation upon the successful propagation of Entra ID Premium licensing and the completion of the baseline identity migration.*

### 1. Automation & Scalability (Dynamic Membership)
**Objective:** Transition from Static to Dynamic Groups.
**Logic:** Implement Attribute-Based Access Control (ABAC) using the rule: (user.department -eq "Faculty").
**Goal:** Eliminate manual administrative overhead during the "Joiner-Mover-Leaver" (JML) lifecycle.

### 2. Context-Aware Security (Conditional Access)
**Objective:** Deploy Conditional Access Policies (CAPs) to replace "all-or-nothing" security.
**Scenarios:**
* **Geofencing:** Restrict administrative logins to known Franchise locations (e.g., NYC HQ and designated travel hubs like Cork, Ireland).
* **Device Compliance:** Require devices to be "Intune Managed" before accessing the NYC-Executives data.

### 3. Privileged Identity Management (PIM)
**Objective:** Implement "Just-In-Time" (JIT) access for the ADMN role.
**Rationale:** Alan Turing should not have Global Admin rights 24/7. He should "activate" them only when needed for a specific task, reducing the blast radius of a potential credential compromise.

### 4. Lifecycle Workflows
**Objective:** Automate the "Onboarding" experience.
**Logic:** Trigger an automated "Welcome to NYC Franchise" email and provision a temporary library pass as soon as a user with the STAF role is detected in the directory.

### The Plan: The "Hybrid Governance" Demonstration
To demonstrate advanced lifecycle management, I transitioned the Faculty group from a static assignment model to a dynamic membership rule based on the 'Department' attribute. This ensures that any new user provisioned with the 'Faculty' tag is automatically granted access to relevant resources, eliminating manual administrative intervention and reducing the risk of 'Access Creep'.

| Feature | Phase 1: Manual (Static) | Phase 2: Entra Suite (Dynamic) |
| --- | --- | --- |
| **Effort** | High (Manual entry for every hire) | Low (Auto-provisions based on attributes) |
| **Error Rate** | High (Human typos) | Zero (Logic-based) |
| **Security** | Static (Users stay even if fired) | Real-time (Users leave if attribute changes) |
| **Use Case** | Small Business / Specialized Roles | Enterprise / Scalable Franchises |

### Technical Change Log: Transitioning Security Baselines
**Date:** 2026-02-23
**Action:** Disabled Microsoft Entra "Security Defaults."
**Rationale:** To facilitate the implementation of granular **Conditional Access Policies (CAPs)**. Security Defaults (the baseline) is incompatible with CAPs (the enterprise standard).

**Risk Mitigation:** Before disabling the defaults, I pre-configured the `NYC-CAP-ADMN-RequireMFA` policy to ensure that no "Security Gap" occurred during the transition. Administrative identities remained protected throughout the cut-over.

**Critical Discovery: Microsoft Mandatory Portal MFA**
During UAT (User Acceptance Testing), it was observed that the STAF-MCurie identity was prompted for MFA despite being excluded from the organizational Conditional Access Policy.

**Technical Investigation:** > Analysis of the Sign-in Logs revealed that the interruption was not triggered by a custom policy, but by the Global Microsoft Admin Portal Mandate (aka.ms/mfaforazure). This mandate enforces MFA for all identities—regardless of role—when accessing administrative endpoints (entra.microsoft.com).

**Validation of Custom CAP:**
To validate the custom NYC-CAP-ADMN-RequireMFA policy, a secondary test was performed using a standard productivity endpoint (portal.office.com).
* **Result:** The standard user successfully authenticated via Single-Factor Authentication (SFA), confirming that the custom CAP is correctly excluding non-privileged users from MFA friction during standard operations, while Microsoft's global policy maintains baseline security for the portal itself.

**Self-Service Password Reset (SSPR) & Converged Policy**
**Implementation:** Transitioned from legacy SSPR settings to the Converged Authentication Methods Policy in Entra ID.
* **Enabled Methods:** Microsoft Authenticator (Push), Email OTP.
**UAT Observation (The "Registration Gap"):** > Initial testing for user STAF-MCurie resulted in a "Not Registered" error.
* **Analysis:** SSPR is a two-part system: Policy Enablement + User Registration.
* **Remediation:** In a production environment, this would be addressed via an "MFA/SSPR Registration Campaign." For this lab, registration was manually completed via the aka.ms/ssprsetup endpoint to verify the end-to-end reset workflow.

### SSPR Verification Log:
* **Status:** FUNCTIONAL / SUCCESSFUL
* **Test Path:** Triggered "Forgotten Password" workflow for STAF-MCurie.
* **Validation:** System successfully triggered an SMS OTP to the registered mobile device. Identity was verified, and the user reached the "New Password" entry portal.
> Note: For the integrity of the lab environment, the password was not rotated after successful verification to prevent session disruption.

![SSPR validation through registered phone](./assets/sspr_phone_recovery_request.png)
> *Fig 2.1: SSPR Identity Challenge—System successfully identifying user-registered recovery methods.*
![Received code text verification](./assets/text_verification_code.png)
> *Fig 2.2: Out-of-Band (OOB) Verification—SMS delivery of the one-time passcode (OTP).*
![Successful code verification for new passwor](./assets/verification_password_step.png)
> *Fig 2.3: Verification Success—System granting the password-reset write-back permission after successful authentication.*
