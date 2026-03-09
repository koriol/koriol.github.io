# IAM

## SOP: User Provisioning & Identity Lifecycle
**Associated Policy:** Identity and Access Management (IAM) Policy
**Control Mapping:** NIST 800-53: AC-2, IA-2

We never create an account based on a verbal request or a casual email. By requiring a ticket, we establish a "non-repudiation" trail. If an account is ever compromised, we can trace exactly who authorized its creation and when.

### 1. Technical Onboarding Procedure
#### Step 1: Ticket Verification & Identity Creation
Instructions: 
1. Open the Jira/Ticketing system and locate the "New Hire" request.
2. Cross-reference the "Role" on the ticket with the approved RBAC Matrix.
3. Log into the Microsoft Entra Admin Center.
4. Navigate to Users > All Users > New User and enter the details from the ticket.

We avoid "manual permissioning." If you assign permissions directly to a user, you will eventually forget to remove them. By using Security Groups, we ensure that if the user changes departments, we simply swap their group, and their old access is instantly revoked.

#### Step 2: Role-Based Group Assignment
Instructions:
1. In the user’s profile, select Groups.
2. Click Add Memberships.
3. Search for and select the groups mapped to their department (e.g., `SG-Finance-ReadWrite`, `SG-All-Staff`).

Identity is the new perimeter. A password alone is no longer sufficient. By enforcing MFA at the "Onboarding" stage, we ensure the user cannot access sensitive company data until they have registered a second factor (something they have, like a phone, and something they know, like a password).

#### Step 3: MFA Enforcement & Conditional Access
Instructions:
1. Navigate to Protection > Conditional Access.
2. Ensure the "Require MFA for all users" policy is active.
3. (Alternatively) Go to Authentication Methods and ensure Microsoft Authenticator is set as a required method.

### Technical Offboarding Procedure (The "Kill Switch")
#### Step 1: Immediate Account Disablement
Instructions:
1. Search for the user in Entra ID.
2. On the Overview page, click Block Sign-in.
3. Toggle "Block sign-in" to Yes and Save.


<u>**Skills Applied**</u>
* **Identity Governance:** Ensuring the digital identity is managed consistently across the organization.
* **NIST Mapping:** Understanding how a "button click" in a dashboard satisfies a federal security requirement.
* **Audit REadiness:** Building a process that is "bulletproof" for a future security auditor.




