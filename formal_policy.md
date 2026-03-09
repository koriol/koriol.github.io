# IAM

## Onboarding and Offboarding

### Formal Policy
A Formal Policy is the "Law" of your organization. While the SOP (Standard Operating Procedure) tells you how to click the buttons, the Policy explains what must be done and why it is required. In GRC (Governance, Risk, and Compliance), the policy is what an auditor looks at first. They ask: "Do you have a rule for this?" and then "Can you prove you followed it?" Most organizations follow the NIST Cybersecurity Framework (CSF) or NIST 800-53.

* AC-2 (Account Management): Specifically mandates that the organization manages information system accounts (including creating, activating, modifying, and disabling).
* IA-2 (Identification and Authentication): Requires that the system uniquely identifies and authenticates users (where MFA comes in).
* PS-4 (Personnel Termination): Requires that access is disabled and all keys/assets are returned upon termination.

A policy doesn't need to be a book, shorter is often better because people actually read it. For a portfolio, 1–2 pages is the "sweet spot." It should be high-level enough to last 3 years without needing an update, while the SOP (the step-by-step) can change every time Microsoft updates their dashboard. A professional policy generally follows this structure:
* **Purpose:** Why does this policy exist? (e.g., "To protect company data during personnel transitions.")
* **Scope:** Who does this apply to? (Employees, contractors, interns?)
* **Roles & Responsibilities:** Who is responsible for what? (HR triggers the request; IT/Security executes it.)
* **Policy Statements:** The "Musts."
  * Example: "All accounts must be disabled within 24 hours of termination."
  * Example: "MFA must be enforced for all administrative identities."
  * Compliance/Enforcement: What happens if the policy is broken?

***

### Personnel Identity Lifecycle Policy
**1. Purpose**
The purpose of this policy is to establish a secure framework for managing the lifecycle of digital identities. This ensures that access to organizational resources is granted to authorized users only, managed through structured roles, and revoked immediately upon termination to mitigate the risk of unauthorized access or data exfiltration.

**2. Scope**
This policy applies to all employees, contractors, and third-party vendors who require access to corporate information systems, including but not limited to Microsoft Entra ID, Azure Resources, and integrated SaaS applications.

**3. Policy Requirements**
This policy is designed to satisfy the following security controls:
* NIST 800-53 Rev. 5: AC-2 (Account Management), IA-2 (Identification and Authentication), PS-4 (Personnel Termination).
* ISO 27001: A.9.2 (User Access Management).

* Onboarding: * All access requests must originate from a verified HR ticket.
  * Access must be granted based on Role-Based Access Control (RBAC).
  * Multi-Factor Authentication (MFA) is mandatory for all accounts upon first login.

* Offboarding: * Involuntary terminations require immediate account disablement.
  * Voluntary terminations require account disablement no later than the close of business on the user's final day.
  * Access logs must be reviewed post-termination to ensure no unauthorized activity occurred.

**4. Policy Statements**

**4.1 Identification and Authentication (NIST IA-2)**
* All users must be uniquely identified with a dedicated corporate identity.
* Multi-Factor Authentication (MFA): MFA is mandatory for all users. Bypassing MFA requires executive approval and a documented compensatory control.
* Password complexity must meet or exceed organizational standards (min. 14 characters, complexity enabled).

**4.2 Onboarding & Provisioning (NIST AC-2)**
* Authorization: No account shall be created without a formal request ticket from HR or the department head.
* Least Privilege: Access must be granted based on Role-Based Access Control (RBAC). Users shall only be granted the minimum access necessary to perform their job functions.
* Default Deny: All access is "Denied by Default" until explicitly granted.

**4.3 Offboarding & Deprovisioning (NIST PS-4)**
* Timely Revocation: * Involuntary Termination: Access must be disabled immediately upon notification.
  * Voluntary Termination: Access must be disabled by the end of the user's final working day.
* Asset Recovery: All physical hardware (laptops, security keys) must be returned and verified against the asset register before the offboarding ticket is closed.
* Account Status: Accounts will be "Disabled" for a period of 30 days for data retention before being considered for deletion.

**4.4 Access Reviews**
* Privileged account access (Global Admins, etc.) will be reviewed quarterly.
* Standard user access will be reviewed annually to identify and remove "privilege creep."

**5. Compliance and Enforcement**
Failure to adhere to this policy may result in disciplinary action, up to and including termination of employment. Any identified security gaps must be logged in the Risk Register.






Creating a policy before a technical setup demonstrates "Governance-First" thinking. Not just a "button-clicker"—but the regulatory requirements (NIST 800-53) that drive those clicks.

















