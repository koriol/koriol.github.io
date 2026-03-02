# Modern IAM

## JumpCloud & Identity Lifecycle Governance

### Introduction
In a modern cloud-first organization, the "Perimeter" is no longer a physical office or a firewall; it is the Identity. This project simulates the deployment of a Cloud Directory Service (JumpCloud) to act as the single source of truth for an organization. We will integrate this directory with Microsoft 365 (Entra ID) to automate the "Joiner-Mover-Leaver" process, ensuring that security follows the user regardless of where they log in.

<u>Purpose</u>: Manual user creation is a security risk. If an IT tech forgets to delete an account when an employee leaves, that "Orphaned Account" becomes a backdoor for attackers. By using JumpCloud to "Provision" and "Deprovision" users, we ensure that one click in JumpCloud instantly cuts off access to Microsoft 365, Azure, and the local Linux servers.

<u>**Skills Applied**</u>
* **Directory Integration:** Linking disparate identity providers (IdPs) via SCIM and SAML.
* **User Lifecycle Management:** Automating onboarding and offboarding to reduce human error.
* **SaaS Governance:** Managing third-party application access from a centralized console.
* **Compliance Alignment:** Mapping identity actions to NIST 800-53 controls.

**Tools Used**
* **JumpCloud:** (The Authoritative Directory)
* **Microsoft 365 / Azure Entra ID:** (The Target SaaS Suite)
* **Azure VNet:** (The existing networking infrastructure)

**Goals**
1. **Centralize Identity:** Create a single user account in JumpCloud that controls access to everything.
2. **Automate Provisioning:** Sync JumpCloud users to Microsoft 365 automatically.
3. **Secure the Entrance:** Implement MFA at the directory level to protect all downstream apps.

***

### Establishing the Authoritative Source (JumpCloud Setup)
Before we can manage users, we need a "Source of Truth." While we could use Azure's native Entra ID, companies like Agency Cybersecurity use tools like JumpCloud because they are "Platform Agnostic"—meaning they can manage Windows, Macs, Linux, and Google Workspace all from one place. We are setting up JumpCloud to be the "Boss" of your Azure environment.















