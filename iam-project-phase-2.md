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
| Feature | Phase 1: Manual (Static) | Phase 2: Entra Suite (Dynamic) |
| --- | --- | --- |
| **Effort** | High (Manual entry for every hire) | Low (Auto-provisions based on attributes) |
| **Error Rate** | High (Human typos) | Zero (Logic-based) |
| **Security** | Static (Users stay even if fired) | Real-time (Users leave if attribute changes) |
| **Use Case** | Small Business / Specialized Roles | Enterprise / Scalable Franchises |
