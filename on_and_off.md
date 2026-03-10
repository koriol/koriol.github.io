# IAM

## Onboarding and Offboarding

Project: Integrated IAM Onboarding & Offboarding
Goal: Establish a secure identity lifecycle by linking a project management "Request" to a technical "Provisioning" action in Entra ID.

Purpose: To establish a secure Identity Lifecycle Management (ILM) framework that bridges the gap between administrative requests (GRC) and technical enforcement (IAM).

Why This Matters:
* **Security Risk:** 80% of cyberattacks use identity-based methods. Poor offboarding leads to "orphaned accounts," which are primary targets for lateral movement.
* **Compliance:** Frameworks like NIST 800-53 (AC-2) and SOC2 mandate that access is granted only with authorization and revoked immediately upon termination.
* **Operational Efficiency:** Automated or standardized onboarding reduces "time-to-productivity," ensuring employees have the tools they need on Day 1 without over-provisioning access.

### Roadmap
Step 1: Initialize the "Source of Request" (Ticketing)
Create a dedicated "Onboarding/Offboarding" board in a free tool like Jira or Trello. Create your first "New Hire" card for a hypothetical user.
> Security actions should never be "shadow tasks." By starting with a ticket, we ensure every administrative action in Entra ID has an audit trail and a business justification. This aligns with NIST 800-53 Control AC-2 (Account Management), which requires documented authorization for account actions.

Success Criteria: A "To-Do" ticket exists containing the new hire's name, role, and department.

When to Take Screenshot: Once the ticket is created and assigned to "Security/IT."

Caption: Fig 1.0: Establishing a formal audit trail via a ticketing system to authorize account provisioning.

Step 2: Configure RBAC Groups in Microsoft Entra
Log into your Entra ID trial and create a Security Group (e.g., "Finance_Access") rather than assigning permissions to the user directly.
> We are implementing the Principle of Least Privilege (PoLP). Assigning permissions to groups rather than individuals prevents "privilege creep"—where a user keeps old permissions when they change roles. This makes offboarding significantly cleaner, as you only need to remove the user from the group.

Success Criteria: The Security Group is visible in the "Groups" blade of Entra ID with "Assigned" membership type.

When to Take Screenshot: The "Groups" dashboard showing your newly created department-specific security group.

Caption: Fig 1.1: Implementation of Role-Based Access Control (RBAC) within Microsoft Entra to enforce Least Privilege.

Step 3: Provision the Identity & Enforce MFA
Create the user in Entra ID, assign them to the group from Step 2, and enable Conditional Access (or Per-User MFA) to require a second factor on the first login.
> A "naked" password is a high-risk vulnerability. By enforcing MFA at the point of creation, we ensure that the identity is protected before it ever touches company data. This satisfies IA-2 (Identification and Authentication) controls by requiring a non-cryptographic or cryptographic multi-factor authenticator.

Success Criteria: User status shows "Enabled" and the "Authentication Methods" tab confirms MFA is required.

When to Take Screenshot: The "Users" blade showing the new account and the "Groups" tab within that user’s profile.

Caption: Fig 1.2: User provisioning in Entra ID with integrated MFA enforcement and group-based permissions.

Step 4: The "Kill Switch" (Offboarding Procedure)
Simulate a termination by moving the Jira ticket to "Closed" and immediately "Disabling" the account in Entra ID.
> Timing is the most critical factor in offboarding. Disabling an account is preferred over immediate deletion because it preserves the user's data for legal or forensic review while instantly revoking their ability to sign in. This is a key component of an Incident Response (IR) and Account Management strategy.

Success Criteria: The account status in Entra ID changes from "Enabled: Yes" to "Enabled: No," and all active sessions are revoked.

When to Take Screenshot: The "User Profile" screen showing the "Block Sign-in" toggle set to "Yes" with a timestamp.

Caption: Fig 2.0: Rapid deprovisioning via account disablement to mitigate the risk of unauthorized access or data exfiltration.



| Tool | Role in Project | Why it’s used |
| --- | --- | --- |
| Jira (Free) | The Request Layer | Acts as the formal ticketing system to document the audit trail for every hire and fire. |
| Microsoft Entra ID | The Enforcement Layer | Primary Identity Provider (IdP) for account creation, RBAC, and MFA enforcement. |
| Markdown / GitHub | The Documentation Layer | Where the SOP, Policy, and evidence are hosted, demonstrating professional technical writing. |
| Microsoft Graph API | Automation | To demonstrate how to audit MFA status or group memberships via script.|


### Core Competencies
* **IAM Lifecycle Management:** Managing an identity from "Hire to Retire."
* **Cross-Platform Integration:** Demonstrating how GRC processes (Ticketing) drive Technical Controls (Entra ID).
* **Audit Readiness:** Creating a "Paper Trail" that would satisfy a security auditor.

![](./formal_policy.md)
![](./sop.md)

***

#### The Request (Ticketing & Audit Trail): Initialize the Security Ticket
Before we touch Microsoft Entra ID, we must have a "Source of Truth" for the request. We will use Jira to simulate a request from HR. Every administrative action in a production environment must be tied to a request. This prevents "Shadow IT" and unauthorized account creation. From a GRC perspective, this ticket serves as the Authorization Evidence required by NIST 800-53 Control AC-2. If an auditor asks why "Alex Rivera" has access to your data, you point to this ticket.

![Onboarding Alex Rivera on Sprint 1 SCRUM - 5 active ticketing](./modern_iam/active_ticket.png)
> *Fig 4.0: Initiating the identity lifecycle through a formal HR-to-IT ticketing workflow for auditability.*

A security professional ensures that the data being collected is structured. If "Department" is just a random sentence in a description box, it’s hard to audit later. By creating specific fields, you ensure that every onboarding request contains the exact information needed to satisfy NIST 800-53 AC-2.

![Ticket categories added to Jira](./modern_iam/ticket_categories.png)
> *Fig 4.0a: Configuring Jira custom fields to ensure standardized data collection for IAM audit requirements.*


#### Provisioning the Identity (Entra ID): Create the User Account
We are creating a unique identity for the user. By requiring a password change on the first login, we ensure the "Secret" is known only to the user, not the administrator, supporting the Principle of Non-Repudiation. Filling out the Job Info fields is critical for future automation (like Dynamic Groups).

We are mirroring the data from your Jira ticket exactly. Consistency between the Request (Jira) and the Execution (Entra) is what prevents security gaps. If the department is wrong, the user might get access to the wrong files, violating the Principle of Least Privilege.

![](./modern_iam/entra_ticket.png)
> *Fig 4.1: Provisioning a unique digital identity in Microsoft Entra ID based on authorized ticket metadata.*

#### Role-Based Access (RBAC): Assign to Security Groups
Instead of granting "Finance Folder" access directly to Alex, we put Alex in the `Finance_Users` group. This is Role-Based Access Control (RBAC). If Alex leaves the Finance department, we simply remove them from the group, and all associated permissions are revoked instantly. This prevents Privilege Creep.

![](./modern_iam/arivera_sg_group.png)
> *Fig 4.2: Implementing Role-Based Access Control (RBAC) to enforce the Principle of Least Privilege.*

Passwords are the weakest link in the security chain. By creating a Conditional Access Policy, we are building a "Security Gate." This ensures that even if an attacker steals Alex's password, they cannot access the environment without the second factor (Alex's phone or hardware key). This is the "Gold Standard" for identity protection.

![](./modern_iam/grant_alex.png)
> *Fig 4.3: Mitigating credential-based attacks by enforcing Multi-Factor Authentication (MFA) via Entra Conditional Access.*

A task isn't "Done" until the documentation is updated. By commenting on the specific security controls applied (MFA and Group membership), you are providing a "Final Audit" for the ticket. This closes the loop between the Policy (what we said we'd do) and the Execution (what we did).

![](./modern_iam/onboard_done_ticket.png)
> *Fig 4.4: Completion of the secure onboarding workflow and closure of the audit trail.*

***

### The Offboarding Workflow (The Kill Switch)

Offboarding is a race against time. By creating a high-priority ticket, you are documenting the "Authorization to Revoke." This ensures that if the user attempts to sue for "loss of access" or if an auditor asks why the account was killed, you have the formal HR/Management directive on file.

![](./modern_iam/offboard_ticket.png)
> *Fig 5.0: Initiating emergency deprovisioning workflow to mitigate insider threat and unauthorized access risk.*

By switching the account to "No," you are effectively disabling the identity. This is the primary defense against "Orphaned Accounts." In a GRC context, this satisfies NIST 800-53 PS-4, as it ensures that access is formally and technically terminated the moment the personnel's relationship with the organization ends.

![](./modern_iam/alex_disable.png)
> *Fig 5.1: Disabling the user account to prevent unauthorized access following personnel termination.*

Blocking the account stops new logins, but Revoke sessions kills current ones. This is critical for emergency terminations where you need to ensure the user cannot send one last email or download a file after being notified of their departure.

![](./modern_iam/revoked_sessions.png)
> *Fig 5.2: Invalidation of all active refresh tokens to ensure immediate cessation of resource access.*


![](./modern_iam/offboarding_done.png)
> *Fig 5.3: Closed-loop lifecycle management showing the completion of both provisioning and deprovisioning requests.*

***

### Automated Security Auditing

To demonstrate programmatic verification of security controls. In an enterprise environment with thousands of users, manual checks are impossible. Using the Microsoft Graph API, I developed a script to instantly audit the tenant for "Disabled" accounts to verify that offboarding procedures were technically successful.

Why this matters:
* **Continuous Monitoring:** Satisfies NIST 800-53 CA-7, which requires ongoing verification of security control effectiveness.
* **Accuracy:** Eliminates human error in the audit process.
* **Scalability:** Allows a security team to pull reports on thousands of users in seconds.

After performing the manual offboarding of Alex Rivera, I used this Python script to "close the loop." By querying the Graph API directly, I confirmed that the `accountEnabled` attribute was successfully set to `false` in the backend database. This demonstrates a "Trust but Verify" approach to identity governance.

```
import requests

# 1. THE COORDINATES
TENANT_ID = 'oriolkgmail.onmicrosoft.com' # Use the domain name to avoid ID errors
CLIENT_ID = 'PASTE_APPLICATION_CLIENT_ID_HERE' # From App Registration Overview
CLIENT_SECRET = 'PASTE_SECRET_VALUE_HERE' # The long string with symbols (~, _, etc.)

# 2. THE LOGIN (OAuth 2.0)
auth_url = f"https://login.microsoftonline.com/{TENANT_ID}/oauth2/v2.0/token"
auth_data = {
    'grant_type': 'client_credentials',
    'client_id': CLIENT_ID,
    'client_secret': CLIENT_SECRET,
    'scope': 'https://graph.microsoft.com/.default'
}

print("Attempting to get token...")
token_res = requests.post(auth_url, data=auth_data)
res_data = token_res.json()

if "access_token" not in res_data:
    print("FAILED TO LOG IN.")
    print(f"Microsoft says: {res_data.get('error_description')}")
else:
    token = res_data['access_token']
    print("SUCCESS: Logged in. Auditing tenant now...")
    
    # 3. THE AUDIT
    headers = {'Authorization': f'Bearer {token}', 'ConsistencyLevel': 'eventual'}
    query = "https://graph.microsoft.com/v1.0/users?$filter=accountEnabled eq false&$select=displayName,userPrincipalName,accountEnabled&$count=true"
    
    response = requests.get(query, headers=headers)
    
    if response.status_code == 200:
        users = response.json().get('value', [])
        print(f"Found {len(users)} disabled accounts.")
        for u in users:
            print(f"[VERIFIED] {u['displayName']} is DISABLED.")
    else:
        print(f"Audit Error: {response.text}")
```

![](./modern_iam/py_account_disabled.png)
> *Fig 6.1: Utilizing Python and Microsoft Graph API to programmatically audit account status and verify offboarding compliance.*

### Skills Applied
* **Security Automation:** Leveraging APIs and Python to perform continuous monitoring and automated auditing.
* **Service Principal Management:** Configuring App Registrations and OAuth2 flows for secure programmatic access.

***
## Identity Governance & Lifecycle Management
Framework: NIST 800-53 Rev. 5 (AC-2, PS-4) | Sector: Education Technology

This project simulates a high-stakes identity lifecycle for an NYC-based educational storefront. It bridges the gap between Governance (Policy) and Enforcement (Technical Controls) by automating the "Hire-to-Retire" process using an industry-standard tech stack.

![](./modern_iam/licensed-image-compliance-lifecycle.jpg)

### Key Accomplishments
* Engineered a Secure Onboarding SOP: Developed a formal ticketing workflow in Jira to ensure every new identity is authorized, fulfilling NIST 800-53 AC-2.
* Implemented Zero Trust MFA: Enforced Conditional Access Policies to mitigate credential-based attacks, ensuring that 100% of administrative identities require phishing-resistant factors.
* Executed Emergency Offboarding: Demonstrated the "Kill Switch" protocol (Deprovisioning + Session Revocation) to neutralize insider threats within minutes of a termination request (NIST 800-53 PS-4).
* Programmatic Verification: Built a custom Python script to query the Microsoft Graph API, providing an automated "Proof of Work" that identity status aligns with security policy.

### Lessons Learned & Troubleshooting (The "Real World" GRC)
A. Identity Identifier Mismatch (AADSTS700016)
* The Problem: The automation script failed to authenticate despite providing "correct" IDs.
* The Discovery: Diagnostic analysis of the Entra ID object hierarchy revealed that a User Object ID was being utilized instead of the Service Principal's Application (Client) ID.
* The Resolution: Corrected the OAuth 2.0 Client Credentials flow by identifying the specific Service Principal ID within the target tenant.

B. OData Filtering & API Latency
* The Problem: The Graph API returned an empty list even after the account was disabled.
* The Discovery: Discovered that Microsoft Graph requires the ConsistencyLevel: eventual header for advanced filtering on the accountEnabled attribute.
* The Resolution: Hardened the Python request headers to account for distributed data synchronization, ensuring accurate audit results.

C. Secret Hygiene
* The Problem: Distinguishing between Secret ID (Metadata) and Secret Value (Credential).
* The Resolution: Established a protocol for secret generation and secure handling, ensuring only the "Value" is utilized in authentication strings while the "ID" is used solely for audit logs.
