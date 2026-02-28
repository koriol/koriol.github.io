# Governance and Compliance

## Phase 3: Remediation (The "Security Contact" Fix)

Now that the assessment is complete, we are beginning the Remediation phase. Our audit flagged a major operational risk: the lack of a designated security contact. If a "Break-Glass" account is activated or a brute-force attack is detected, Microsoft has no way to alert the NYC Franchise admins. By configuring these settings, we are formally closing a gap in the Incident Response (IR) family of NIST controls. This ensures that the technical alerts we built in the SIEM (Sentinel) have a corresponding "Human in the Loop" notification system.

**<u>Applied Skills</u>**
* **Security Operations Center (SOC) Setup:** Establishing the fundamental alerting pathways for a cloud environment.
* **Incident Response Readiness:** Implementing automated notification workflows to reduce Mean Time to Respond (MTTR).
* **Control-Specific Remediation:** Directly addressing NIST 800-53 IR-6 (Incident Reporting) requirements.

![Remediation for email notifications](./grcac/email_notifications.png)
> *Fig 9.1: Critical Control Remediation—Establishing formal security contact notifications within Microsoft Defender for Cloud. This configuration satisfies NIST 800-53 IR-6, ensuring that high-severity security telemetry is proactively pushed to the NYC Franchise administration for immediate response.*

---

In this step, we are addressing the Continuous Monitoring (CA-7) and Information System Monitoring (SI-4) requirements of the NIST 800-53 framework. While our previous steps focused on "Governance" (who to email), this is a "Technical" control. By enabling Defender for Servers, we are deploying an automated threat detection layer across the NYC Franchise. This ensures that if a malicious process runs on the Linux VM, the system doesn't just "Log" it—it actively detects and alerts on the behavior.

**<u>Applied Skills</u>**
* **Endpoint Detection and Response (EDR) Deployment:** Enabling advanced threat protection at the cloud scale.
* **Security Automation:** Utilizing "Auto-provisioning" to ensure all current and future VMs are born with security agents pre-installed.
* **Cloud Workload Protection (CWPP):** Understanding how to protect specific compute resources within a global security framework.

![Activate server for remediation](./grcac/server_on.png)
> *Fig 10.1: Technical Control Remediation—Activating Microsoft Defender for Servers to satisfy NIST 800-53 CA-7 and SI-4. This transition provides the NYC-Linux-VM with real-time EDR capabilities, moving the infrastructure from passive auditing to active threat protection.*

***
In a production-scale GRC environment, "Policy Drift" occurs when agents are installed but not configured to stay current. I identified that the Azure Monitor Agent (AMA) was stuck in a "Disabled" state. By manually enabling Automatic Upgrade orchestration, I bridged the gap between a static installation and a dynamic, self-healing security posture. This directly addresses NIST 800-53 SI-2, ensuring that the NYC Franchise infrastructure remains protected against the latest known vulnerabilities without manual administrative overhead.

**<u>Applied Skills</u>**
* **Security Orchestration:** Configuring automated lifecycle management for cloud security agents.
* **Control Mapping (SI-2):** Implementing automated flaw remediation (Patching/Updates) at the agent level.
* **Troubleshooting Cloud Fabric:** Resolving "Orchestration" logjams that prevent security agents from reaching a functional state.

![Automatic upgrade success and enabled](./grcac/provisioning_success.png)
> *Fig 10.2: Automated Flaw Remediation—Configuring 'Automatic Upgrade' for the Azure Monitor Agent. This satisfies NIST 800-53 SI-2 by ensuring the NYC-Linux-VM maintains an evergreen security posture, allowing the cloud fabric to automatically deploy security patches and agent improvements.*

***
In a high-velocity Cloud GRC environment, waiting for a full 24-hour compliance cycle is inefficient. We are utilizing Technical Verification to confirm that our remediations (NIST IR-6 and CA-7) have been pushed to the resource level. By checking the Extensions and Security Blade of the NYC-Linux-VM, we are proving that the "Governance" we set at the subscription level has successfully "Inherited" down to the actual hardware. This bridges the gap between a "Policy on Paper" and a "Technical Reality."

**<u>Applied Skills</u>**
* **Technical Validation:** Verifying policy inheritance from the Subscription level down to the Resource level.
* **Extension Management:** Understanding how Azure uses "Extensions" to deploy security agents automatically.
* **Audit Efficiency:** Utilizing "Batch Remediation" strategies to maximize productivity during compliance cycles.

![](./grcac/)
> *Fig 10.3: Remediation Verification—Confirming the successful auto-provisioning of security agents on the NYC-Linux-VM. This validates that the 'Defender for Servers' policy is now physically protecting the asset, even before the next formal NIST audit cycle completes.*

***

Identity is the new perimeter. After hardening the server and the notifications, I turned my attention to Identity and Access Management (IAM). The NIST audit flagged the "Subscription Owner" count as a risk. By reviewing the Role-Based Access Control (RBAC) settings, I ensured that the NYC Franchise follows the Principle of Least Privilege, ensuring that only a minimal number of highly-trusted identities hold the "Keys to the Kingdom.

**<u>Applied Skills</u>**
* **RBAC (Role-Based Access Control) Management:** Auditing and modifying high-level permissions.
* **Identity Governance:** Applying NIST 800-53 AC-2 (Account Management) standards.
* **Privileged Access Review:** Conducting a formal review of "Owner" level permissions.

![](./grcac/)
> *Fig 11.1: Identity Governance Remediation—Performing an RBAC audit to satisfy NIST 800-53 AC-2. By limiting the number of Subscription Owners, I reduced the potential attack surface and ensured that privileged access is restricted to essential personnel only.*

*** 
After completing a "Batch Remediation" of the high-severity findings—covering Incident Response, Threat Protection, and Identity Governance—I initiated a final manual compliance scan. This represents the "Validation" phase of the GRC lifecycle. By forcing a re-evaluation of the environment, I am moving the NYC Franchise from a "Non-compliant" baseline to a "Hardened" production state, providing the necessary evidence for a successful audit sign-off.

**<u>Applied Skills</u>**
* **Continuous Compliance Monitoring:** Utilizing CLI tools to reduce the audit feedback loop.
* **Batch Remediation Validation:** Proving that multiple technical fixes correctly satisfy complex regulatory frameworks.
* **Evidence Lifecycle Management:** Capturing the "After" state of a security hardening project.

![](.grcac/)
> *Fig 12.1: Final Compliance Validation—The NIST 800-53 dashboard showing successful remediation of previously flagged high-severity risks. The NYC Franchise now meets the baseline requirements for Incident Response and Endpoint Protection.*
