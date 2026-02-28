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

In early 2026, Microsoft finalized the unification of Microsoft Sentinel and Microsoft Defender for Cloud into a single security operations interface. I adapted to this architectural shift by managing the NYC Franchise incident queue through the Unified Security Operations Platform. By identifying and claiming the "Emergency User" login incidents, I demonstrated the transition from Governance (setting the rules) to Active Incident Response, fulfilling NIST 800-53 IR-4 (Incident Handling).

<u>**Applied Skills**</u>
* **Unified SOC Navigation:** Operating within the integrated Microsoft Defender/Sentinel ecosystem.
* **Incident Lifecycle Management:** Transitioning security alerts from "New" to "In Progress" through formal assignment.
* **Modern Security Tooling:** Staying current with 2026-standard cloud security interfaces and cross-platform workflows.

![](./grcac/)
> *Fig 16.1: Unified Security Operations—Managing NYC-Franchise-Prod incidents within the integrated Microsoft Defender portal. This reflects the 2026 industry standard for unified XDR + SIEM monitoring, where the 'Emergency User' login alerts are formally assigned for investigation in compliance with NIST 800-53 IR-4.*

***

To validate the effectiveness of the NYC-Franchise-Prod monitoring strategy, I performed a manual "Hunt" for a high-priority custom alert: Break-Glass Account Activation. Using Kusto Query Language (KQL) within the Unified Defender portal, I verified that the Syslog stream successfully captured the emergency administrator's login signature (EMRG-FRAN-ADMIN). This proactive verification ensures that even if automated correlation logic is delayed by portal synchronization, the underlying security telemetry is intact and discoverable, satisfying NIST 800-53 AU-6 (Audit Record Review).

<u>**Applied Skills**</u>
* **KQL Query Engineering:** Writing and executing custom search strings to isolate specific security events.
* **Proactive Threat Hunting:** Manually verifying alerts within the SIEM/XDR unified data lake.
* **Unified SOC Operations:** Navigating the 2026 Defender portal to bridge the gap between "Alerts" and "Incidents."

![](./grcac/kql_alert.png)
> *Fig 16.2: Custom Detection Validation—Executing a KQL hunt to verify the 'Break-Glass' alert logic. This query confirms that the NYC-Linux-VM is successfully transmitting critical administrative events to the SIEM, providing non-repudiable evidence of emergency account usage.*

***

To ensure the NYC Franchise SOC operates with industry-standard terminology, I mapped the "Break-Glass" detection to the MITRE ATT&CK categories within the Unified Defender Portal. By classifying the event under Credential Access, I enabled the SIEM to correlate this administrative login with other potential lifecycle stages, such as Persistence or Lateral Movement. This structured approach directly supports NIST 800-53 IR-4 (Incident Handling) by providing a clear, taxonomical record of the security event.

<u>**Applied Skills**</u>
* **Incident Scoping:** Defining the severity and category of security events based on GRC frameworks.
* **Entity Mapping:** Linking disparate data points (Users, IPs, Hosts) to create a unified "Attack Story."
* **SOC Workflow Management:** Moving security telemetry through the lifecycle of Alert -> Incident -> Assignment.

![](./grcac/)
> *Fig 16.3: Formal Incident Classification—Promoting the custom 'Break-Glass' alerts to a high-severity incident (INC-NYC-PRV-01). By mapping the 'EMRG-FRAN-ADMIN' entity to the target VM, I am establishing the forensic link required for a NIST-compliant security investigation.*

***

To align the NYC-Franchise-Prod incident with global threat intelligence standards, I performed a granular mapping of the alert to the MITRE ATT&CK Framework. I identified the activity as T1078 (Valid Accounts), specifically T1078.004 (Cloud Accounts). This classification acknowledges that while the account is "Valid," its activation outside of a declared emergency constitutes a high-risk security event. This level of precision is required for NIST 800-53 IR-4 to ensure that incident reporting is searchable and categorized by tactical behavior rather than just "Alert Name."

<u>**Applied Skills**</u>
* **Threat Taxonomy:** Applying specific MITRE ATT&CK techniques (T1078) to cloud identity events.
* **Cybersecurity Framework Integration:** Bridging the gap between NIST compliance and MITRE tactical operations.
* **Technical Precision:** Differentiating between "Malware" and "Credential Abuse" in a SOC environment.

![](./grcac/mitre_menu.png)
> *Fig 16.5: Tactical Intelligence Mapping—Applying MITRE ATT&CK Technique T1078 (Valid Accounts) to the NYC Franchise incident. Mapping to this specific technique ensures that the SOC can track the usage of high-privilege 'Break-Glass' accounts across the enterprise landscape.*

***

To validate the end-to-end security pipeline, I analyzed raw Syslog telemetry captured by the Azure Monitor Agent. The logs successfully identified the EMRG-FRAN-ADMIN user initiating a session on vm-nyc-linux-01. By documenting the specific TimeGenerated and SyslogMessage within the incident file, I’ve established a forensic timeline that satisfies NIST 800-53 IR-5 (Incident Monitoring). I concluded the exercise by resolving the incident as a "Sanctioned Test," demonstrating professional "Closing the Loop" procedures.

<u>**Applied Skills**</u>
* **Log Forensic Analysis:** Interpreting Linux Syslog strings to identify users, terminal sessions, and command context.
* **Evidence Documentation:** Maintaining a chain of custody for security logs within a SIEM incident file.
* **Incident Resolution:** Properly classifying and closing security cases according to industry-standard SOC workflows.

![](./grcac/)
> *Fig 16.4: Forensic Log Verification—Analysis of raw Syslog telemetry confirming the activation of the 'EMRG-FRAN-ADMIN' account. This high-fidelity data provides the necessary audit trail for NIST 800-53 compliance, linking the administrative alert to a specific timestamp and system-level event.*

***

In the final stage of incident creation, I focused on Asset Correlation to ensure high-quality incident grouping. By explicitly mapping the EMRG-FRAN-ADMIN entity to the vm-nyc-linux-01 host, I provided the Defender XDR engine with the context needed to calculate the "Blast Radius" of the event. This satisfies NIST 800-53 IR-4(4) (Information Correlation), which requires organizations to correlate incident information to achieve an organization-wide perspective. This ensures that any subsequent suspicious activity from this user or on this host will be automatically appended to this case file, preventing "Alert Fatigue."

<u>**Applied Skills**</u>
* **Incident Correlation:** Mastering the logic of how entities (Users/Hosts) drive the grouping of security alerts.
* **Blast Radius Analysis:** Understanding how mapping assets allows a SIEM to visualize the potential spread of a threat.
* **XDR Hygiene:** Maintaining a clean incident queue by ensuring "High Quality" entity associations.

![](./grcac/)
> *Fig 16.6: Entity-Based Correlation—Mapping the NYC-Linux-VM and the Emergency Admin account as the primary entities for INC-NYC-PRV-01. This technical association enables the XDR platform to track the 'Blast Radius' and correlate future telemetry, fulfilling NIST 800-53 IR-4 requirements for information correlation.*

***

In the final stage of incident engineering, I performed Schema Mapping to translate raw KQL query results into recognized Security Entities. By designating the Computer column as a Device Entity and the SyslogMessage as the source of Account data, I enabled the SIEM’s correlation engine to "see" the actors involved rather than just treating the logs as flat text. This fulfills NIST 800-53 AU-10 (Non-repudiation), as it creates a definitive link between the system resource and the administrative action.

<u>**Applied Skills**</u>
* **Schema Mapping:** Translating raw log data (KQL columns) into standardized security entities (Accounts/Devices).
* **Data Normalization:** Ensuring that custom alerts "speak the same language" as the rest of the Microsoft Defender ecosystem.
* **Entity Linking:** Creating the logical associations required for automated incident grouping and blast-radius visualization.

![](./grcac/entity_mapping.png)
> *Fig 16.7: Logical Entity Mapping—Configuring the schema to translate raw KQL columns into actionable security entities. By mapping the 'Computer' column to a 'Device' entity, I am enabling the SOC to perform cross-resource correlation and automated incident tracking across the NYC-Franchise-Prod environment.*

***

With the incident formally created, I utilized the Visual Investigation Graph to map the "Attack Story." By correlating the EMRG-FRAN-ADMIN account with the vm-nyc-linux-01 host, the SIEM generated a relational web showing the timeline of the login events. This visual evidence is critical for NIST 800-53 IR-4, as it allows stakeholders to quickly understand the scope of a potential breach without reading thousands of lines of raw logs.

<u>**Applied Skills**</u>
* **Visual Forensics:** Using graph-based modeling to track account movement and resource impact.
* **Attack Path Analysis:** Identifying the relationship between a privileged identity and a production asset.
* **XDR Storyboarding:** Translating technical alerts into a visual narrative for executive reporting.

![](./grcac/node_mapping.png)
> *Fig 17.1: Visual Incident Correlation—The Investigation Map for INC-NYC-PRV-01. The graph visualizes the relationship between the NYC-Linux-VM and the security alerts, providing a 360-degree view of the administrative event and confirming no lateral movement occurred.*

***

The transition from Detection to Response was completed by analyzing the visual "Attack Story" generated by the SIEM. By investigating the relationship between the `EMRG-FRAN-ADMIN` identity and the `vm-nyc-linux-01` resource, I confirmed the scope of the event was limited to a single authorized session. The resolution of this incident marks the successful validation of NIST 800-53 IR-4 (Incident Handling) and AU-6 (Audit Review), establishing a hardened and observable environment for the NYC Franchise.

<u>**Applied Skills**</u>
* **Incident Lifecycle Completion:** Taking a security event from "New" to "Resolved" with full documentation.
* **Evidence Retention:** Utilizing cloud-native logging to maintain a forensic trail even when compute resources are deallocated.
* **XDR Platform Proficiency:** Navigating the unified Microsoft security stack to perform end-to-end SOC operations.

![](./grcac/)
> *Fig 17.2: Incident Lifecycle Completion—Formal resolution of INC-NYC-PRV-01. The inclusion of a detailed closure statement and forensic log evidence provides the 'Full-Loop' documentation required for NIST 800-53 IR-5 compliance, proving the SOC's ability to identify and neutralize administrative risks.*

***

In this final stage of the NYC-Franchise-Prod monitoring setup, I successfully mapped the incident's "Attack Story" using the Unified Defender Investigation Graph. While the graph correctly identified the NYC-Linux-VM as the primary impacted asset, I performed additional manual correlation to link the EMRG-FRAN-ADMIN identity to the event. I moved the raw forensic logs from the Advanced Hunting environment into the Incident Activity Log, ensuring a centralized and immutable audit trail in compliance with NIST 800-53 AU-6.

<u>**Applied Skills**</u>
* **Visual Forensics:** Interpreting node-based investigation maps to determine incident scope.
* **Evidence Centralization:** Transferring raw telemetry from hunting queries into formal incident documentation.
* **Asset/Entity Distinction:** Understanding the hierarchy of Assets (Hardware) vs. Entities (Identities) within an XDR ecosystem.

![](./grcac/comment_log.png)
> *Fig 17.2: Forensic Chain of Custody—Attaching raw Syslog telemetry to the incident activity log. This step ensures that the 'Emergency Access' alert is backed by non-repudiable system logs, satisfying NIST 800-53 requirements for evidence retention and incident accountability.*

***

With the technical evidence secured, I transitioned the incident to a Resolved state, utilizing standardized GRC classification (True Positive - Authorized Test). To conclude Phase 4, I performed a post-incident Security Posture Review via Microsoft Secure Score. This allowed me to see the direct impact of my work—moving the NYC-Franchise-Prod environment closer to NIST 800-53 alignment by successfully implementing logging and monitoring configurations that were previously "Missing" or "At Risk."

<u>**Applied Skills**</u>
* **Incident Post-Mortem:** Formally closing cases with clear, audit-ready determinations.
* **Security Posture Management (CSPM):** Using Secure Score to track the progress of control implementation.
* **Closing the GRC Loop:** Demonstrating that technical configuration directly results in measurable compliance growth.

![](./grcac/incident_resolved.png)
> *Fig 18.1: Formal Incident Closure—The 'Resolved' incident queue for the NYC Franchise. This marks the successful completion of the detection and response lifecycle for the Break-Glass account activation event, ensuring full compliance with NIST 800-53 IR-4.*

***

To conclude Phase 4, I navigated the Incident Management filters to verify the successful transition of the NYC-Linux-VM alerts to a "Resolved" state. Recognizing that cloud security scores often lag behind real-time configuration changes, I pivoted to the Completed Actions log within Microsoft Secure Score to document the tangible impact of previous GRC hardening tasks (MFA implementation). This dual-verification approach ensures that my portfolio reflects both Operational Success (closing incidents) and Strategic Success (improving the overall security posture).

<u>**Applied Skills**</u>
* **Advanced Incident Filtering:** Navigating SOC dashboards to locate and audit historical security cases.
* **Compliance Progress Tracking:** Using CSPM (Cloud Security Posture Management) tools to quantify the value of security labor.
* **Audit-Ready Documentation:** Ensuring that "Resolved" statuses and "Completed" logs are captured as non-repudiable evidence.

![](./grcac/completed_actions.png)
> *Fig 18.2: Measured Security Improvement—Reviewing completed NIST-aligned actions within Microsoft Secure Score. The 'Impact' column quantifies how each completed control (such as MFA enforcement) directly reduces the organizational attack surface and increases the NYC Franchise compliance percentage.*

***

### Conclusion
Phase 4 transformed the NYC-Franchise-Prod environment from a collection of "blind" resources into a Hardened, Observable Ecosystem. By successfully implementing the Azure Monitor Agent (AMA) and custom KQL-based analytics, I established a "digital watchtower" capable of identifying privileged account abuse in real-time. The formal resolution of the "Break-Glass" incident proves that the governance policies established in the earlier phases are now backed by operational technical controls.

<u>**Lessons Learned**</u>
* **Cloud UI Agility:** Modern security platforms (Defender/Sentinel) are constantly evolving. Successful GRC professionals must focus on the underlying Security Logic (Entities, Tactics, Evidence) rather than memorizing button locations.
* **Telemetry Context:** A log without a "Story" is just noise. Mapping raw Syslog data to MITRE ATT&CK techniques (T1078) is what turns a data point into an actionable security incident.
* **The "Audit Trail" is King:** Getting the "Green Check" is satisfying, but the Comments and Forensic Logs are what save an organization during a real-world regulatory audit.
