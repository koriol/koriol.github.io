# IAM

## Onboarding and Offboarding

Project: Integrated IAM Onboarding & Offboarding
Goal: Establish a secure identity lifecycle by linking a project management "Request" to a technical "Provisioning" action in Entra ID.

Project Introduction: The "Why"
Purpose: To establish a secure Identity Lifecycle Management (ILM) framework that bridges the gap between administrative requests (GRC) and technical enforcement (IAM).

Why This Matters:

Security Risk: 80% of cyberattacks use identity-based methods. Poor offboarding leads to "orphaned accounts," which are primary targets for lateral movement.

Compliance: Frameworks like NIST 800-53 (AC-2) and SOC2 mandate that access is granted only with authorization and revoked immediately upon termination.

Operational Efficiency: Automated or standardized onboarding reduces "time-to-productivity," ensuring employees have the tools they need on Day 1 without over-provisioning access.

Step 1: Initialize the "Source of Request" (Ticketing)
Create a dedicated "Onboarding/Offboarding" board in a free tool like Jira or Trello. Create your first "New Hire" card for a hypothetical user.

Thought Process: Security actions should never be "shadow tasks." By starting with a ticket, we ensure every administrative action in Entra ID has an audit trail and a business justification. This aligns with NIST 800-53 Control AC-2 (Account Management), which requires documented authorization for account actions.

Success Criteria: A "To-Do" ticket exists containing the new hire's name, role, and department.

When to Take Screenshot: Once the ticket is created and assigned to "Security/IT."

Caption: Fig 1.0: Establishing a formal audit trail via a ticketing system to authorize account provisioning.

Step 2: Configure RBAC Groups in Microsoft Entra
Log into your Entra ID trial and create a Security Group (e.g., "Finance_Access") rather than assigning permissions to the user directly.

Thought Process: We are implementing the Principle of Least Privilege (PoLP). Assigning permissions to groups rather than individuals prevents "privilege creep"—where a user keeps old permissions when they change roles. This makes offboarding significantly cleaner, as you only need to remove the user from the group.

Success Criteria: The Security Group is visible in the "Groups" blade of Entra ID with "Assigned" membership type.

When to Take Screenshot: The "Groups" dashboard showing your newly created department-specific security group.

Caption: Fig 1.1: Implementation of Role-Based Access Control (RBAC) within Microsoft Entra to enforce Least Privilege.

Step 3: Provision the Identity & Enforce MFA
Create the user in Entra ID, assign them to the group from Step 2, and enable Conditional Access (or Per-User MFA) to require a second factor on the first login.

Thought Process: A "naked" password is a high-risk vulnerability. By enforcing MFA at the point of creation, we ensure that the identity is protected before it ever touches company data. This satisfies IA-2 (Identification and Authentication) controls by requiring a non-cryptographic or cryptographic multi-factor authenticator.

Success Criteria: User status shows "Enabled" and the "Authentication Methods" tab confirms MFA is required.

When to Take Screenshot: The "Users" blade showing the new account and the "Groups" tab within that user’s profile.

Caption: Fig 1.2: User provisioning in Entra ID with integrated MFA enforcement and group-based permissions.

Step 4: The "Kill Switch" (Offboarding Procedure)
Simulate a termination by moving the Jira ticket to "Closed" and immediately "Disabling" the account in Entra ID.

Thought Process: Timing is the most critical factor in offboarding. Disabling an account is preferred over immediate deletion because it preserves the user's data for legal or forensic review while instantly revoking their ability to sign in. This is a key component of an Incident Response (IR) and Account Management strategy.

Success Criteria: The account status in Entra ID changes from "Enabled: Yes" to "Enabled: No," and all active sessions are revoked.

When to Take Screenshot: The "User Profile" screen showing the "Block Sign-in" toggle set to "Yes" with a timestamp.

Caption: Fig 2.0: Rapid deprovisioning via account disablement to mitigate the risk of unauthorized access or data exfiltration.



Tool,Role in Project,Why it’s used
Jira (Free),The Request Layer,Acts as the formal ticketing system to document the audit trail for every hire and fire.
Microsoft Entra ID,The Enforcement Layer,"Your primary Identity Provider (IdP) for account creation, RBAC, and MFA enforcement."
Markdown / GitHub,The Documentation Layer,"Where the SOP, Policy, and evidence are hosted, demonstrating professional technical writing."
Microsoft Graph API,Automation (Optional),(Since you're comfortable with Python) To demonstrate how to audit MFA status or group memberships via script.

Skills Honed for Your Portfolio
IAM Lifecycle Management: Managing an identity from "Hire to Retire."

Cross-Platform Integration: Demonstrating how GRC processes (Ticketing) drive Technical Controls (Entra ID).

Audit Readiness: Creating a "Paper Trail" that would satisfy a security auditor.

![](./
