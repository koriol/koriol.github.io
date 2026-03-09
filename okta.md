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

I implemented a Cloud-to-Cloud (C2C) Integration between Microsoft Entra ID and the JumpCloud Open Directory. By utilizing the OAuth 2.0 protocol, I established a secure, delegated authorization flow. This allows JumpCloud to act as the primary Identity Provider (IdP), centralizing user management and laying the groundwork for automated provisioning. This architecture prevents 'Identity Silos' and ensures that administrative actions in Entra ID are reflected across the franchise's security stack.

<u>**Skills Applied**</u>
* **Identity Federation:** Establishing cross-platform trust using modern protocols (OAuth/OIDC).
* **API Delegation:** Managing application permissions within the Microsoft Graph ecosystem.
* **Scalable Architecture:** Building a directory structure that supports multi-tenant expansion.

![](./modern_iam/identity_bridge.png)
> *Fig 3.1: Establishing the Identity Bridge—Successfully authorizing the OAuth 2.0 handshake between Microsoft Entra ID and JumpCloud. This enables real-time synchronization of the NYC-Franchise-Prod workforce.*

To ensure a secure onboarding process, I utilized JumpCloud’s Staged User State. This allowed me to verify the successful import of identities from Microsoft Entra ID before granting live access to the environment. I then transitioned the users to an Active State, which triggered the formal provisioning of their identity across the managed directory. This two-step process mirrors enterprise best practices for Identity Lifecycle Management, preventing unauthorized access during the initial staging and configuration phase.

<u>**Skills Applied**</u>
* **Lifecycle State Management:** Transitioning users between Staged, Active, and Suspended states.
* **Onboarding Workflow Design:** Implementing a "Ready-to-Work" gate for new identities.

![](./modern_iam/users_staged.png)
![](./modern_iam/users_active.png)
> *Fig 4.2: User Lifecycle Activation—Transitioning imported identities from Staged to Active status to enable resource access and policy enforcement.*

***

### The "Security Group" and MFA Enforcement
With the identity directory active, I transitioned to the Policy Enforcement phase. I implemented a Group-Based Access Control (GBAC) model, creating a 'Security-Enforced-Users' group to centralize security requirements. By applying a Forced MFA Enrollment Policy with a zero-day grace period, I ensured that all administrative and high-value identities (including the Alan Turing identity) adhere to the organization's Zero Trust mandate. This demonstrates the ability to translate compliance requirements (e.g., NIST 800-53 IA controls) into technical enforcement.

<u>**Skills Applied**</u>
* **Group-Based Access Control (GBAC):** Scalable management of security policies.
* **MFA Enrollment Orchestration:** Configuring "Push" and "TOTP" factors for a cloud workforce.
* **GRC Alignment:** Direct implementation of Identity Authentication (IA) controls.

![](./modern_iam/)
> *Fig 5.1: Zero Trust Enforcement—Implementing a mandatory MFA enrollment policy for the 'Security-Enforced-Users' group to satisfy NIST-aligned Identity Authentication requirements.*

During the policy enforcement phase, I identified a vendor-specific constraint regarding MFA Grace Periods. JumpCloud requires a minimum 1-day enrollment window for new policies. To validate the policy's efficacy immediately, I performed a Live Authentication Test. By simulating a user login within the enrollment window, I confirmed that the MFA 'Gate' was active and correctly interrupting the authentication flow to solicit secondary factor registration. This proactive testing ensures that security controls are functioning as intended prior to a full organizational rollout.

<u>**Skills Applied**</u>
* **Security Control Validation:** Testing policies in real-time to ensure expected behavior.
* **User Experience (UX) Auditing:** Understanding the 'Enrollment' flow from the end-user's perspective.

![](./modern_iam/jumpcloud_mfa_popup.png)
> *Fig 5.2: Policy Enforcement Validation—Confirming the MFA enrollment prompt is active for the 'Aturing' identity. While the administrative status shows 'Not Enrolled,' the technical control successfully intercepts the login attempt to force security registration.*

I identified a critical dependency where the automated onboarding flow required a functional Exchange Online mailbox, which was not provisioned for the administrative accounts. To maintain the project's Zero-Trust architecture, I pivoted from 'Email-Driven Activation' to Manual Administrative Provisioning. By directly injecting an initial password hash into the directory and enforcing a 'Reset on First Use' policy, I successfully activated the workforce without relying on insecure or non-existent mail flow. This demonstrates proficiency in Manual Credential Management and Identity Lifecycle troubleshooting.

<u>**Skills Applied**</u>
* **Out-of-Band (OOB) Authentication:** Activating users without traditional email-based SMTP relays.
* **Credential Hygiene:** Enforcing immediate password rotation upon manual provisioning.

![](./modern_iam/aturing_password_reset.png)
> *Fig 4.3: Manual Credential Injection—Bypassing SMTP dependencies by manually provisioning initial credentials for the 'Aturing' identity, ensuring account activation in a mailbox-less environment.*

At this stage of the deployment, the Identity and Access Management (IAM) pillar of the NYC-Franchise-Prod environment is fully operational. I have successfully established a Single Source of Truth and enforced Zero Trust authentication via MFA. The project now enters the Endpoint Protection phase, where the focus shifts from 'Who is accessing the system' to 'How is the device behaving.' This layered defense strategy ensures that even if an identity is compromised, the underlying hardware is protected by industry-leading EDR (CrowdStrike).

***

### The CrowdStrike "Sensor" & CID
With the Identity Provider (IdP) fully operational, the project transitioned into the Endpoint Detection and Response (EDR) phase. I provisioned the CrowdStrike Falcon environment to serve as the primary defensive layer for the franchise's hardware assets. By retrieving the organization's unique Customer Identification (CID) and sourcing the appropriate sensor installers, I established the foundation for automated, cloud-managed endpoint protection. This strategy ensures that every device in the NYC-Franchise-Prod fleet is monitored for behavioral anomalies and malware in real-time.

<u>**Skills Applied**</u>
* **EDR Console Administration:** Navigating the CrowdStrike Falcon platform.
* **Security Software Provisioning:** Sourcing and managing sensor installers for enterprise deployment.
* **Asset Identification:** Managing unique Customer IDs (CIDs) for multi-tenant environments.

To implement a comprehensive security stack, I navigated the Cross-Platform Provisioning requirements between the Identity Provider (JumpCloud) and the Endpoint Detection and Response (EDR) platform (CrowdStrike). I recognized that while JumpCloud facilitates the deployment of the security agent, the Authoritative Management Console resides within the CrowdStrike Security Cloud. By establishing a standalone Falcon instance using a verified administrative identity, I secured the necessary Customer ID (CID) and API keys required to bridge the two platforms. This illustrates an understanding of Vendor Interoperability in a modern SaaS ecosystem.

<u>**Skills Applied**</u>
* **Vendor Management:** Sourcing and initializing separate enterprise security tools.
* **Architecture Design:** Understanding the relationship between an "Installer" (JumpCloud) and the "Controller" (CrowdStrike).

During the EDR (Endpoint Detection and Response) provisioning phase, I encountered Vendor Validation Filters that restricted trial access to verified business domains. To maintain project momentum, I utilized a professional-identifier (FRAN-NYC) and a temporary administrative relay to fulfill the business-logic requirements of the CrowdStrike Falcon vetting process. This highlights the real-world challenge of Security Procurement, where administrative overhead and vendor compliance checks must be navigated to secure critical infrastructure tools.

<u>**Skills Applied**</u>
* **Vendor Relationship Management:** Navigating enterprise sign-up and vetting workflows.
* **Problem-Solving under Constraints:** Bypassing domain-level restrictions for lab environments.

![](./modern_iam/crowdstrike_request.png)
> *Fig 5.2: Procurement & Vetting—Initiating the CrowdStrike Falcon trial request. This phase involves a 24-hour manual security review by the vendor to validate the business context (FRAN-NYC) before granting console access.*














