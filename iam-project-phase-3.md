# Governance
## Phase 3: Break-Glass and PIM

### Roadmap
Step 1: The "Break-Glass" Account (Emergency Access)
Step 2: Privileged Identity Management (PIM)
Step 3: The "Legal" AUP (Terms of Use)

### Project Component: Emergency Access (Break-Glass) Strategy

1. The Rationale: Why FIDO2/Passkey?
Resilience over Redundancy: Standard MFA (Push/SMS) depends on external cloud services. If Microsoft’s MFA service or a cellular network goes down, standard admins are locked out.

Mandate Compliance: As of 2025, Microsoft mandates MFA for all admin portals. A "password-only" exclusion is no longer possible for Entra/Azure portals.

Phishing Resistance: FIDO2/Passkeys provide hardware-backed security that cannot be intercepted by AitM (Adversary-in-the-Middle) phishing attacks.

2. Configuration & Lessons Learned
Identity Isolation: Created a cloud-only account (.onmicrosoft.com) to remove dependencies on on-premises sync or custom DNS.

Policy Neutralization: Explicitly excluded the account from all Conditional Access Policies (CAPs). This ensures that a misconfigured "Block All" policy won't lock the keys inside the safe.

Technical Lesson: Learned that Incognito Mode must be disabled during Passkey registration because the browser needs a direct hardware handshake with the device's security chip.

3. Results & Verification
Zero-Standing Dependency: The account can successfully bypass standard MFA service outages.

Successful Authentication: Verified via Sign-in Logs that the account successfully authenticated using FIDO2 Security Key as the primary credential.

Security Posture: Elevated the tenant’s "Identity Secure Score" by implementing phishing-resistant factors for the most privileged roles.

Note: While the EMRG account is excluded from organizational Conditional Access MFA, it remains subject to Microsoft’s Mandatory Portal MFA (aka.ms/mfaforazure). To ensure 100% availability during a cloud service outage, I have configured this account with a Phishing-Resistant Passkey/FIDO2 method, satisfying the mandate without creating a dependency on the Entra MFA push notification service.
The "Conflict" Explained
Microsoft's Mandatory MFA Mandate (Phase 1, which started late 2024/early 2025) overrides Conditional Access for "Admin Portals."

**The Problem:** Even if you exclude EMRG-FRAN-ADMIN from your "Conditional Access" policy, when that account hits the Entra Portal, Microsoft's system-level policy says, "I don't care about your exclusions; this is a high-value portal, so give me MFA."

**The Risk:** If your primary MFA service (like the Authenticator App) is down, and Microsoft is forcing MFA on your break-glass account, you are effectively locked out.

To have a "true" Break-Glass account in 2026, you must use an MFA method that is independent of the Entra MFA service (the cloud service that sends push notifications).

Microsoft officially recommends using a FIDO2 Security Key (like a YubiKey) or Passkey for these accounts.

Why: A FIDO2 key is a "Phishing-Resistant" hardware factor.

The Benefit: It satisfies the "Mandatory MFA" requirement because the key itself provides a second factor (Physical Key + PIN), but it doesn't rely on Maria's phone, Alan's phone, or the Microsoft Authenticator cloud service being "up."

Task,Status,Note
Break-Glass User Created,Complete ✅,EMRG-FRAN-ADMIN is ready.
Passkey Registered,In Progress ⏳,"This makes the account ""Portal-Proof."""
PIM Setup,Upcoming 📅,We'll do this once the EMRG account is verified.

![Pop-up for activating security key NFC](./assets/sec_key_pop-up.png)
> *Fig 3.1: FIDO2/Passkey Initialization—Enrolling a mobile device as a hardware-backed security key for the emergency access account.*

> *Fig 3.2: Phishing-Resistant MFA—Verification of the Passkey registration, satisfying the Microsoft Mandatory MFA mandate without cloud-service dependency.*
![Passkey successful configured](./assets/security_key_success.png)

![Option to login with passkey under password prompt](./assets/alt_login_passkey.png)
> *Fig 3.3: Break-Glass Entry Path—The specialized authentication flow for emergency scenarios, bypassing standard password entry.*

![Pop-up prompting to choose security key](./assets/passkey_options.png)
> *Fig 3.4: Break-Glass Entry Path—The specialized authentication flow for emergency scenarios, bypassing standard password entry.*

> 🚨 Audit Note: In a production environment, this account would be connected to a Microsoft Sentinel Alert. Any login by EMRG-FRAN-ADMIN should trigger a high-severity incident notification to the CISO, as it indicates a total failure of standard administrative paths.

![Role settings showing 4-hour limit and "Require Justification"](./assets/role_settings_max_4hr.png)
> *Fig 3.4: Configuring Just-In-Time (JIT) Policy—Enforcing a 4-hour limit and mandatory business justification for Global Admin elevation.*

![Role assignment fail pop-up](./assets/role_assignment_fail.png)
> *Fig 3.5: Encountered a conflict where a pre-existing permanent assignment prevented PIM activation. Resolved by decommissioning the static assignment in favor of the Eligible JIT workflow.*

![Active assignments tab](./assets/aturing_active_assignments.png)
> *Fig*

![PIM audit log](./assets/PIM_audit_log.png)
> *Fig 3.8: PIM Audit Logs—The system-generated audit trail capturing the 'Why' behind the elevation. This ensures 100% accountability for high-privilege actions.*

### Project Component: Privileged Identity Management (PIM)
**1. The Strategy: Just-In-Time (JIT) Elevation**
<u>The Objective:</u> Eliminate "Standing Access" for administrative accounts. By default, even highly trusted users like Alan Turing should operate as standard users until elevated access is required for a specific task.

<u>The Policy:</u> Enforced a 4-hour activation window, mandatory MFA, and a required business justification for the Global Administrator role.

**2. Implementation & Troubleshooting (The "Overlapping Assignment" Fix)**
<u>The Conflict:</u> During setup, I encountered an error: "Role assignment already exists."

<u>The Diagnosis:</u> This was caused by an existing "Permanent Active" assignment conflicting with the new "Eligible" PIM assignment.

<u>The Resolution:</u> Successfully decommissioned the static/permanent assignment, allowing the PIM engine to manage the lifecycle exclusively. This ensured the user was strictly "Eligible" and had no persistent power.

**3. Results & Verification (The Audit Trail)**
<u>Activation Flow:</u> Verified that the user must go through a formal request process, providing a justification (e.g., "Monthly Security Audit") which is then logged permanently.

<u>Time-Bound Security:</u> Confirmed that privileges automatically expire after the 4-hour threshold, reducing the window of opportunity for credential abuse.

<u>Governance Visibility:</u> Leveraged PIM Audit Logs to track activation history, ensuring 100% accountability for privileged actions.

![Error for role assignments](./assets/update_role_queued.png)
> *Fig 3.5: Conflict Resolution—Decommissioning the pre-existing permanent role assignment to allow for JIT (Just-In-Time) eligibility.*

![Role elevation activation justification](./assets/activate_aturing_justification.png)
> *Fig 3.6: The Activation Workflow—User 'Alan Turing' requesting elevation. Note the mandatory justification and the 4-hour expiration timer.*

![Manual deactivation for active assignments](./assets/aturing_active_assignments.png)
> *Fig 3.7: Active State Verification—Evidence of the active assignment with the option to manually 'Deactivate' if tasks are completed early.*

![Audit log confirming role elevation activation](./assets/PIM_audit_log.png)
> *Fig 3.8: PIM Audit Logs—The system-generated audit trail capturing the 'Why' behind the elevation. This ensures 100% accountability for high-privilege actions.*

![Leaver access denied](./assets/leaver_access_denied.png)
> *Fig 3.7: Lifecycle Management (Leaver)—Demonstrating immediate revocation of privileges, ensuring that 'Leavers' or compromised accounts are neutralized instantly.*

### **Project Component: Compliance & Terms of Use (ToU)**

#### **1. Rationale**
To ensure legal and regulatory compliance, I implemented an **Acceptable Use Policy (AUP)**. This prevents "shadow IT" and ensures all users acknowledge their security responsibilities before accessing corporate resources.

#### **2. Configuration Highlights**
* **Policy Enforcement:** Applied via Conditional Access, targeting all Faculty and Staff.
* **Consent Requirement:** Enabled 'Require users to expand,' forcing a manual scroll/expansion of the document to prevent blind acceptance.
* **Audit Trail:** Enabled acceptance reporting to track when and where users agreed to the terms.

![Configuration of terms of use](./assets/tou_config.png)
> *Fig 3.9: Administrative Configuration—Setting the 'Hard' requirement for AUP expansion and acceptance.*
> Implemented the AUP policy initially in Report-only mode. This allowed for an impact analysis to ensure that legitimate sign-ins weren't being unintentionally blocked before full enforcement.

![Confirmation of AUP implementation](./assets/aup_confirm_mc.png)
> *Fig 3.10: End-User Compliance Flow—The mandatory interrupt experienced by users before accessing Office 365 apps.*

![Audit log of terms acceptance](./assets/tou_audit_log.png)
> *Fig 3.11: Audit & Compliance—Detailed reporting showing user acceptance logs, providing an immutable record for legal and regulatory audits.*
![Must expand to accept terms](./assets/aup_read_confirm.png)
> *Fig 3.11: Users must expand the terms of service to confirm acceptance and be granted access.*
