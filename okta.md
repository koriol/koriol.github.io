# Modern IAM

## Okta & Identity Lifecycle Governance

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

With the elevated credentials active, the next step is establishing JumpCloud as the "Source of Truth." I am setting up a cloud-native directory that will act as the master controller for users, devices, and applications. By using Alan’s (Aturing) email for the signup, I am linking the identity of the person performing the work to the account that will hold the "Owner" status in the new IdP.

<u>**Skills Applied**</u>
* **IdP Tenant Provisioning:** Initializing a multi-tenant SaaS security platform.
* **Administrative Account Hardening:** Establishing the root-level identity for the organization.

### Provisioning the Okta Identity Cloud
In a production environment, "Vendor Lock-in" or "Access Friction" can delay critical security deployments. After encountering registration blocks on the JumpCloud platform, I executed a Technical Pivot to Okta, the industry-leading Identity-as-a-Service (IDaaS) provider. By utilizing the Okta Developer Tenant, I established a federated identity source that integrates seamlessly with Microsoft Entra ID, ensuring that the goal of Centralized Identity Governance was achieved without administrative delay.

When selecting an Identity-as-a-Service (IDaaS) provider, I distinguished between Customer Identity (CIAM) and Workforce Identity. For the NYC-Franchise-Prod environment, I implemented the Okta Workforce Identity Cloud. This choice aligns with the operational requirements of a corporate IT environment, where the focus is on securing internal employee access to SaaS suites like Microsoft 365 and enforcing Single Sign-On (SSO) and Multi-Factor Authentication (MFA) across the enterprise.

When initializing the Okta Workforce Identity tenant, I deliberately chose to use the NYC-ADMIN-Aturing account rather than the root 'Owner' account. This decision reflects an adherence to NIST 800-53 (AC-6) by delegating administrative tasks to a secondary privileged identity. By utilizing the account recently elevated via Azure PIM, I maintained a clear audit trail and ensured that the primary 'Owner' credentials remain isolated from third-party service registrations.

<u>**Skills Applied**</u>
* **Vendor Agility:** The ability to swap specialized tools based on availability and requirement.
* **IAM Architecture:** Implementing the same "Source of Truth" logic across different platforms.
* **Product Differentiation:** Understanding the architectural difference between CIAM (Auth0) and Workforce IAM (Okta).
* **Enterprise Identity Strategy:** Selecting tools that support employee lifecycle management (Joiner-Mover-Leaver).

![](./okta/)
> *Fig 2.1: Strategic Pivot to Okta IDaaS & Okta Workforce Identity Initialization — Successfully provisioning the 'NYC-Franchise-Prod' Identity Tenant. Selecting the enterprise-grade Workforce Identity Cloud to manage internal employee lifecycles for the NYC-Franchise-Prod environment.*

***

Recognizing the inherent risk of utilizing a temporary administrative relay for initial tenant provisioning, I immediately moved to establish Administrative Persistence. I provisioned a secondary 'Break-Glass' administrator account tied to a permanent, verified identity. This adherence to Redundancy and Continuity planning ensures that the NYC-Franchise-Prod environment remains manageable throughout the project lifecycle, regardless of third-party mail-flow volatility.

![](./modern_iam/dual_admin.png)
> *Fig 2.2: Establishing Administrative Persistence—Provisioning a permanent secondary administrator to ensure continuous access to the IdP console, independent of the initial registration relay.*








