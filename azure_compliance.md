## Automated NIST 800-53 Compliance Reporting via Azure SDK

### Introduction
In a modern cloud environment, compliance is not a "once-a-year" event; it is a continuous state. Manual audits are prone to human error and are outdated the moment they are finished. This project bridges the gap between Cloud Security Engineering and GRC by automating the extraction of compliance data. By programmatically querying Azure Defender for Cloud, we transform raw security telemetry into an auditor-ready report.

**Goal:** To demonstrate the ability to implement Compliance-as-Code, moving from manual dashboard monitoring to automated evidence collection. This ensures that stakeholders have real-time visibility into the organization's adherence to the NIST 800-53 framework.

<u>**Tools Used**</u>
* **Python:** The primary engine for automation due to its robust library support for cloud APIs.
* **Azure SDK (`azure-mgmt-security`):** To interact directly with the Azure Security Center API for granular control data.
* **Azure Identity Library:** To handle secure, industry-standard authentication via Service Principals.

<u>**Skills Used**</u>
* API Interaction & JSON Parsing
* Identity & Access Management (RBAC)
* GRC Framework Mapping (NIST 800-53)
* Automated Evidence Collection

### Environment Preparation & Identity Governance
Before we can pull sensitive security data, we must establish a secure identity. Using an App Registration (Service Principal) follows the principle of least privilege. We assign the Security Reader role to ensure the script can see compliance states without having the power to alter any security settings.

<u>**Skills**</u>
* IAM Management
* Service Principal Configuration
* Least Privilege Enforcement.

![The "Role Assignments" screen showing App Registration with the "Security Reader" role.](./Entra_audit/compliance_audit.png)
> *Establishing a Service Principal with the 'Security Reader' role to facilitate least-privileged, programmatic access to the Azure Security Center API.*

### Developing the Compliance Extractor Script
We use `DefaultAzureCredential` because it is versatile, allowing the script to run locally using environment variables or in the cloud using Managed Identities. The script targets the `regulatoryComplianceStandards` and `regulatoryComplianceControls` endpoints to filter specifically for NIST 800-53.

<u>**Skills**</u>
* Python Scripting
* SDK Implementation
* API Filtering

![IDE showing the script running in the terminal and the "Report Generated" message.](./)
> *Executing the Python extraction script using the Azure SDK to iterate through regulatory compliance assessments.*

### Parsing and Reporting
Raw JSON is for machines; Markdown is for humans. This step involves logic to parse the `state` property of each control. By mapping the technical failure to the `controlId`, we create a document that a GRC auditor can use to initiate remediation.

<u>**Skills**</u>
* Data Formatting
* Technical Documentation
* Audit Readiness

![A side-by-side view of the generated NIST_Report.md file and the Azure Defender "Regulatory Compliance" blade.](./)
> *Mapping programmatic API outputs to the NIST 800-53 framework, creating a clear audit trail of non-compliant resources.*










