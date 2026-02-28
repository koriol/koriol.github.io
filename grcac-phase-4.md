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

<u>**Applied Skills**</u>
* **Security Data Architecture:** Designing the storage backend for enterprise-scale logging.
* **Resource Lifecycle Management:** Strategically grouping security assets to maintain operational efficiency.
* **Compliance Alignment (AU-2):** Implementing the infrastructure required for systematic audit record generation.

![](./grcac/)
> *Fig 15.1: Security Infrastructure Deployment—Establishing the 'LAW-NYC-SOC' Log Analytics Workspace. This centralized repository acts as the primary ingestion point for all security telemetry from the NYC-Linux-VM, fulfilling NIST 800-53 requirements for centralized audit logging.*

***






