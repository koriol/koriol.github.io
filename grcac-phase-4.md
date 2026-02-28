# GRC and Governance as Code

## Phase 4: Security Operations & SIEM Integration

### Introduction & Goals:
In this phase, we are establishing the Security Operations Center (SOC) capabilities for the NYC Franchise. While our previous work ensured the VM is compliant, we now need to ensure it is observable. The goal is to ingest raw security telemetry (logs) into Microsoft Sentinel, our Cloud-Native SIEM (Security Information and Event Management). This allows us to correlate data, detect brute-force attacks in real-time, and fulfill the NIST 800-53 AU (Audit and Accountability) control family.

### Phase 4 Roadmap:

**Workspace Creation:** Deploying a Log Analytics Workspace (LAW) as the data "Bucket."

**Sentinel Onboarding:** Initializing Microsoft Sentinel on top of the LAW.

**Data Connector Configuration:** Hooking the NYC-Linux-VM into Sentinel using the Azure Monitor Agent (AMA).

**Log Verification:** Running KQL (Kusto Query Language) to confirm that heartbeats and security events are flowing.

### Applied Skills
* **SIEM Architecture:** Understanding how logs flow from an endpoint to a central analytics engine.
* **Data Ingestion & Connectors:** Configuring the "pipes" that move security telemetry across the cloud fabric.
* **KQL (Kusto Query Language):** The primary language used to hunt for threats in the Microsoft ecosystem.
* **Log Analytics Management:** Organizing and retaining security data for forensic investigations.

***

Compliance without visibility is a major risk. To satisfy NIST 800-53 AU-2 (Event Logging), I initiated the deployment of a centralized Log Analytics Workspace (LAW). This serves as the foundational data layer for the NYC Franchise's security operations. By placing the LAW in the same region and resource group as the production assets, I ensured low-latency data ingestion and simplified resource management, establishing the "Data Reservoir" required for advanced threat hunting.

In a production environment, resource re-usability is key to cost optimization. I evaluated an existing Log Analytics Workspace (`law`) to determine its suitability for the NYC Franchise's SIEM backbone. By verifying that the workspace shared the same geographical region as the compute resources, I ensured compliance with NIST 800-53 AU-3 (Content of Audit Records) while minimizing egress costs. I then onboarded Microsoft Sentinel to this workspace, effectively upgrading a simple "Log Bucket" into a full-scale Security Operations Center.

<u>**Applied Skills**</u>
* **Security Data Architecture:** Designing the storage backend for enterprise-scale logging.
* **Resource Lifecycle Management:** Strategically grouping security assets to maintain operational efficiency.
* **Compliance Alignment (AU-2):** Implementing the infrastructure required for systematic audit record generation.
* **Resource Assessment:** Evaluating existing infrastructure for compatibility with advanced security services.
* **Cost Management:** Reducing cloud spend by consolidating logging resources.
* **SIEM Initialization:** Understanding the "Layered" relationship between Log Analytics (Storage) and Sentinel (Intelligence).

![](./grcac/law_sentinel.png)
> *Fig 15.1: SIEM Onboarding—Activating Microsoft Sentinel on the existing 'law' Log Analytics Workspace. This centralizes all security telemetry for the NYC-Franchise-Prod environment, providing the 'Single Pane of Glass' required for real-time incident detection and response.*

***

To centralize security intelligence for the NYC Franchise, I onboarded Microsoft Sentinel onto the existing law Log Analytics Workspace. While the compute resource (NYC-Linux-VM) is located in East US 2 and the workspace in East US, I made the architectural decision to utilize the existing workspace to maintain a consolidated audit trail. This transition elevates the environment from basic logging to a full Cloud-Native SIEM, enabling automated threat detection and response in alignment with NIST 800-53 AU-1 (Audit and Accountability Policy).

<u>**Applied Skills**</u>
* **SIEM Provisioning:** Deploying and configuring a cloud-native Security Information and Event Management system.
* **Regional Data Architecture:** Managing cross-region log ingestion and understanding the associated egress implications.
* **SOC Foundation Building:** Establishing the centralized "Single Pane of Glass" for security telemetry.

![](./grcac/sentinel_overview.png)
> *Fig 15.2: SIEM Activation—Successfully onboarding Microsoft Sentinel to the centralized 'law' workspace. This fulfills the NIST 800-53 requirement for a dedicated security monitoring platform, providing the intelligence layer necessary for the NYC Franchise's Security Operations Center.*

***

To move from identity monitoring to Full-Stack Observability, I configured the Azure Monitor Agent (AMA) data connector within Microsoft Sentinel. By creating a Data Collection Rule (DCR), I defined the specific telemetry streams (Syslog and Auth logs) required for the NYC-Linux-VM. This ensures that the SIEM isn't just watching "logins" (Identity), but is also monitoring the internal OS security events, fulfilling NIST 800-53 AU-12 (Audit Generation).

Navigating the evolving landscape of Azure's security offerings requires a pivot from traditional "Out of the Box" connectors to Solution-Based Ingestion. I identified that Microsoft has integrated Linux telemetry into a broader "Unified Agent" framework. By focusing on the Azure Monitor Agent (AMA) rather than legacy standalone connectors, I ensured that the NYC Franchise monitoring architecture is aligned with current DevOps-integrated security practices, satisfying NIST 800-53 AU-12 while navigating the complexities of modern cloud-native tooling.

<u>**Applied Skills**</u>
* **Technical Troubleshooting (UI Discrepancies):** Navigating non-intuitive cloud interfaces to locate critical security tools.
* **Unified Agent Management:** Understanding the role of the AMA in consolidating infrastructure and security telemetry.
* **Security Tooling Agility:** Adapting to rapid vendor updates and rebranding within the Microsoft security ecosystem.

![](./grcac/syslog_ama.png)
> *Fig 15.3: Adaptive Telemetry Configuration—Locating the Azure Monitor Agent (AMA) syslog connector within the consolidated Sentinel framework. This configuration allows for the secure, high-fidelity ingestion of Linux security events into the NYC Franchise SOC, bypassing legacy agent limitations.*

***

After locating the elusive Syslog via AMA connector, I moved into the "Policy-as-Code" phase by defining a Data Collection Rule (DCR). This is a critical step in Cloud GRC because it ensures we are not "over-logging" (which costs money) or "under-logging" (which leaves us blind). By specifically targeting the AUTH and AUTHPRIV facilities, I am focusing the NYC Franchise's monitoring budget on high-value security telemetry, directly fulfilling NIST 800-53 AU-2 (Audit Events).

<u>**Applied Skills**</u>
* **DCR Engineering:** Creating scoped rules to manage telemetry flow from Linux endpoints.
* **Granular Audit Logging:** Selecting specific Linux Syslog facilities required for security investigations.
* **Resource Mapping:** Associating specific Virtual Machines with centralized logging rules

![](./grcac/data_collection_rule.png)
> *Fig 15.4: Log Ingestion Strategy—Configuring the Data Collection Rule (DCR) for the NYC-Linux-VM. This 'Data Contract' specifies exactly which Linux security facilities (Auth/Authpriv) are transmitted to the SOC, ensuring compliance with NIST 800-53 AU-12 while optimizing for cloud storage costs.*

***

In a high-velocity cloud environment, "Notification Success" is insufficient for audit-grade verification. I navigated to the Data Collection Rule (DCR) management plane to formally verify the association between the NYC-Franchise-Prod telemetry stream and the centralized SIEM. By confirming that the NYC-Linux-VM is a registered resource within the DCR, I’ve established a non-repudiable link between the endpoint and the SOC, satisfying NIST 800-53 AU-6 (Audit Record Review, Analysis, and Reporting).

<u>**Applied Skills**</u>
* **Technical Verification:** Validating policy and rule associations beyond simple UI notifications.
* **Association Auditing:** Ensuring that "Policy-as-Code" (the DCR) is correctly applied to the target "Hardware" (the VM).
* **System Traceability:** Mapping the path of a log from the Linux kernel to the DCR and finally into the Log Analytics Workspace.

![](./grcac/resources_data_vm.png)
> *Fig 15.5: Telemetry Association Verification—Confirming that the NYC-Linux-VM is successfully associated with the DCR-NYC-Linux-Security rule. This validates the technical 'Handshake' between the production server and the SIEM, ensuring that all authentication-level logs are being actively transmitted for SOC analysis.*

***




