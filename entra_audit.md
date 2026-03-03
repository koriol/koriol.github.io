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














