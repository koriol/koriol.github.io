


### Phase 2: Reviewing the Initial Compliance Findings
We are now moving into the "Assessment" stage of the GRC lifecycle. After successfully triggering a scan across both PowerShell and Bash (demonstrating technical persistence), we are now interpreting the raw compliance data. This transition is where a security professional turns "data" into "actionable intelligence." We aren't just looking at red dots; we are identifying the technical gaps in the NYC infrastructure that pose a risk to the franchise's regulatory standing.

Gap Analysis: Formally identifying where the NYC Franchise infrastructure fails to meet NIST 800-53 controls.

Risk Categorization: Understanding the difference between "High," "Medium," and "Low" severity findings in a compliance report.

Evidence Gathering: Learning how to export or screenshot audit findings to prove a "Current State" assessment was performed.

We are documenting a "UI Failover" scenario. When the high-level Regulatory Compliance Dashboard failed to show data, we pivoted to the Azure Policy Compliance blade to find the raw audit results. This demonstrates a deep understanding of the Azure ecosystem—knowing that the "Dashboard" is just a visual wrapper for the underlying "Policy Engine." This is a key skill for GRC professionals who need data now, not in 24 hours.

Platform Navigation: Accessing backend security data when frontend dashboards are latent.

Audit Lifecycle Management: Tracking the "In Progress" state of a global regulatory scan.

Data Retrieval: Using the Policy engine to extract specific non-compliance evidence.

![](./grcac/policy_2.png)
> *Fig 7.6: Backend Compliance Verification—Utilizing the Azure Policy engine to view raw compliance data for the NIST 800-53 initiative. This bypasses the visual latency of the Defender dashboard and confirms that 400+ controls are currently being evaluated against the NYC Franchise resources.*

We are now moving from "Wait and See" to "Active Assessment." We've noticed that the compliance engine has different results for different scopes, highlighting the importance of Hierarchical Governance. We are now identifying the specific "Policy Violations" that are preventing the NYC Franchise from achieving NIST 800-53 compliance. This allows us to move into the Remediation Phase with a clear list of technical targets.

Compliance Scope Analysis: Differentiating between Tenant-wide and Subscription-specific audit results.

Root Cause Identification: Drilling down from a "Non-compliant" status to the specific resource and policy causing the failure.

GRC Data Interpretation: Understanding that "0% Compliant" is a starting point, not a failure of the engineer.

![Compliance implementation verification](./grcac/compliance_verification.png)

Upon initiating the NIST 800-53 audit, we pivoted to the Azure Policy Compliance engine to bypass dashboard latency. The assessment revealed that while individual resources (like the VM) were being scanned, the most critical "High" severity failures were Subscription-wide Governance gaps. We identified that the NYC Franchise lacked essential security "Mains"—specifically missing Incident Response contacts and Defender for Cloud coverage. This shift in focus from "Server Security" to "Tenant Governance" is a key milestone in moving the project toward an enterprise-ready state.

Subscription-Level Auditing: Identifying security gaps that affect an entire cloud environment rather than a single asset.

UUID/Resource Identification: Correlating unique Azure identifiers to specific subscription scopes during an audit.

Policy Type Interpretation: Understanding "AuditIfNotExists" logic—recognizing that the audit is failing because a required security feature hasn't been turned on yet.

![](./grcac/compliance_state.png)
> *Fig 8.1: Subscription-Wide Compliance Assessment—Reviewing the NIST 800-53 audit findings for the NYC-Franchise-Prod subscription. The results highlight critical 'Governance Gaps' in Incident Response (IR-6) and Continuous Monitoring (CA-7), providing a prioritized roadmap for environment-wide remediation.*



