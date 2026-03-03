# Entra ID User Audit

## Introduction
Modern GRC is moving away from manual spreadsheets and toward Continuous Controls Monitoring (CCM). This project demonstrates how to use Python and the Microsoft Graph API to perform automated identity audits within a Microsoft Entra ID (Azure AD) environment.

## Goals & Purpose
The primary goal is to build a reliable auditing tool that programmatically identifies security risks within a tenant.
* **Identify Stale Accounts:** Flag users who haven't signed in for 30+ days to reduce the attack surface.
* **Enforce MFA Compliance:** Detect users without "Strong Authentication" methods.
* **Audit Lifecycle Management:** Verify that "Disabled" accounts are actually restricted and not retaining active sessions.
* **Automate Evidence Collection:** Provide timestamped, repeatable data exports for internal and external auditors.

## Skills & Tools
* **Programming:** Python (msal, requests, python-dotenv).
* **Cloud Identity:** Microsoft Entra ID, Microsoft Graph API, OAuth 2.0 Client Credentials Flow.
* **Security Principles:** Least Privilege, Secret Management, Identity Governance.
* **Compliance Frameworks:** NIST 800-53 (AC-2, IA-2), SOC 2 (CC6.1).

## The Plan
1. Identity Provisioning & App Registration – Register the script as a "Service Principal" in Entra ID and grant scoped API permissions.
2. Secure Environment Setup – Configure local secret management to prevent credential leakage.
3. Development – Write Python logic to authenticate via OAuth 2.0 and query the Graph API.
4. Data Analysis & Reporting – Parse the JSON response into a human-readable audit report.
5. Portfolio Documentation – Log the technical workflow and map it to GRC controls.

***

### App Registration
Before a script can read sensitive user data, it must be granted a "Digital Identity." By registering an application in Entra ID, we create a Service Principal. This allows the script to authenticate securely without needing a human to type in a username and password (which would be a security risk).

<u>**Skills & Tools**</u>
* **Cloud Governance:** Implementing Least Privilege by selecting specific API "Scopes" rather than granting full Global Admin rights.
* **IAM Operations:** Managing Enterprise Application objects and Admin Consent workflows.
* **Tools:** Microsoft Entra Admin Center.

![](./entra_audit/api_permissions.png)
> *Fig 30: Provisioning Least Privilege: Configuring scoped Application Permissions (User.Read.All, AuditLog.Read.All) within Microsoft Entra ID to enable automated auditing while minimizing the security footprint.*

***

### Secure Environment Setup & Secret Management
In a GRC context, "Hardcoding" (writing passwords directly into your code) is a major security finding that would fail a SOC 2 or PCI-DSS audit. By using environment variables (.env), we separate our sensitive "Secrets" from our "Logic." This ensures that if you share your code on GitHub, your private credentials remain on your local machine and are not exposed to the public.

<u>**Skills & Tools**</u>
* **Security Best Practices:** Implementation of Secret Management and "Software Composition Analysis" (SCA) principles.
* **Linux/System Admin:** Managing hidden configuration files and local environment variables.
* **Tools:** Python `python-dotenv` library, `.gitignore`, and a text editor (VS Code).

![](./entra_audit/secure_cred.png)
> *Fig 31: Securing Identity Credentials: Utilizing environment variables (.env) and Git ignore rules to prevent credential leakage in the project repository—aligning with secure development lifecycle (SDLC) best practices.*

***

### Writing the Authentication Logic
Before we can audit users, we must successfully "handshake" with the Microsoft Identity Platform. This step implements the Authentication portion of IAM. We are writing the code that exchanges our protected `.env` secrets for a secure, short-lived Bearer Token.

<u>**Skills & Tools**</u>
* **Security Engineering:** Implementing the OAuth 2.0 protocol.
* **Identity & Access Management:** Utilizing Service Principals for machine-to-machine (M2M) communication.
* **Tools:** Python msal (Microsoft Authentication Library), requests library.

MSAL stands for Microsoft Authentication Library.
* The Problem: Hand-coding the math and security handshakes for OAuth 2.0 is incredibly difficult and prone to bugs.
* The Solution: Microsoft provides this library (MSAL) to handle the heavy lifting. When you import msal, you are bringing in a toolkit that knows exactly how to talk to Microsoft's login servers, how to format your Client Secret, and how to ask for a "Token."
* GRC Value: Using an official, maintained library like MSAL is a Security Best Practice. It ensures your authentication follows the latest industry standards (like encrypted transmissions).

![](./entra_audit/auth_token.png)
> *Fig 32: Verified Identity Handshake: Successfully executing the OAuth 2.0 Client Credentials flow to obtain a JWT access token for non-interactive directory auditing.*

***

### Data Analysis & Audit Logic (The Core Project)
Now that we have our "wristband" (Access Token), we use it to pull raw identity data from the Microsoft Graph. This is the "Audit" phase where we transform raw JSON data into actionable security intelligence—specifically identifying accounts that lack MFA or have gone "stale" (no login in 30+ days).

This step demonstrates the transition from Authentication (who are you?) to Authorization (what are you allowed to see?). We are using the `requests` library to perform a GET request against the Microsoft Graph API, utilizing Data Minimization (via `$select`) to retrieve only the metadata required for a user access review.

<u>**Skills & Tools**</u>
* **Identity Governance:** Identifying orphaned or stale accounts, a key task for NIST 800-53 AC-2 (Account Management).
* **Data Parsing:** Using Python to filter nested JSON dictionaries into a readable format.
* **Tools:** Microsoft Graph Explorer (for testing), Python requests library.

![](./entra_audit/run_data_extract.png)
> *Fig 33: Audit Data Extraction: Programmatically querying the Microsoft Graph API to retrieve identity metadata. The output facilitates the identification of stale accounts, directly supporting SOC 2 CC6.3 (Review of User Access Rights).*

***

### Final Compilation & MFA Logic
The final phase of this project is adding the "Security Punch." We aren't just looking for names; we are looking for MFA (Multi-Factor Authentication) gaps. Identifying users who lack strong authentication is a critical GRC finding that maps directly to NIST 800-53 IA-2 (Identification and Authentication).

<u>**Skills & Tools**</u>
* **Cybersecurity Analysis:** Determining "Security Posture" based on authentication methods.
* **Logic Branching:** Using Python `if/else` statements to categorize security risks.
* **Tools:** Microsoft Graph `strongAuthenticationMethods` endpoint.

![](./entra_audit/risk_output_audit.png)
> *Fig 34: Risk-Based Identity Auditing: Final script execution identifying stale accounts and potential authentication gaps, providing actionable data for a User Access Review (UAR).*

***

## The PowerShell Version
In Windows-centric environments, PowerShell is the native language for automation. This version of the auditor utilizes the `Microsoft.Graph` PowerShell SDK. It achieves the same GRC goals—identifying stale accounts and MFA gaps—but demonstrates "Platform Agility," showing that you can enforce security policies regardless of the toolset provided.

<u>**Skills & Tools**</u>
* **Infrastructure as Code (IaC):** Automating identity audits via shell scripting.
* **Module Management:** Installing and authenticating via the Microsoft Graph PowerShell SDK.
* **Tools:** PowerShell 7, Microsoft Graph API.

![](./entra_audit/powershell_audit_output.png)
> *Fig 35: Native Automation: Utilizing the Microsoft Graph PowerShell SDK to perform identity audits, demonstrating the ability to enforce GRC controls across different technical environments (Python and PowerShell)*

## Summary
This project is functionally successful because it provides a repeatable, objective source of truth for identity auditors. By moving from manual checks to an API-driven approach, the organization reduces the risk of "Identity Sprawl" and ensures that stale or unauthorized accounts are flagged immediately.

***

## Challenges Overcome & Lessons Learned

1. Overcoming Environment & Interpreter Conflicts
   * Challenge: Initial script execution failed with command not found and NameError because the system was attempting to run Python code as a Bash script.
   * Lesson Learned: I learned to implement Shebang lines (#!/usr/bin/env python3) and use App Execution Aliases in Windows to ensure the correct Python interpreter is targeted. This taught me the importance of a standardized development environment in security automation.

2. Implementing Secure Secret Management
   * Challenge: Balancing the need for script automation with the risk of credential leakage (Hardcoding).
   * Lesson Learned: I successfully implemented the python-dotenv library to abstract sensitive Service Principal credentials into a .env file. I further secured the repository by configuring .gitignore to prevent these secrets from ever being committed to version control—a core requirement for Secure SDLC and SOC 2 compliance.

3. Navigating API Licensing & Data Gaps
   * Challenge: The script initially failed to return sign-in telemetry (signInActivity).
   * Lesson Learned: I discovered that certain Graph API properties require specific license tiers (Entra ID P1/P2) and granular permissions (AuditLog.Read.All). I learned to use the Microsoft Graph Explorer as a "sandbox" to validate API responses and troubleshoot "null" data before scaling my code.

4. Cross-Platform Troubleshooting (PowerShell)
   * Challenge: Encountered a CertificateThumbprint error when attempting to connect via the Microsoft Graph PowerShell SDK.
   * Lesson Learned: I analyzed the error and realized the SDK was defaulting to Certificate-based authentication. I pivoted to a PSCredential object approach, successfully using my existing Client Secret to authenticate. This demonstrated the value of understanding multiple authentication flows (Secret vs. Certificate) in an IAM context.

