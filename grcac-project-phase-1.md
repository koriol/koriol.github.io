# GRC & Compliance

## Summary for Phase 1
We are shifting the project focus from active threat detection to Governance, Risk, and Compliance (GRC). By adopting the NIST 800-53 framework, we are aligning the NYC Franchise with federal-grade security standards. This transition demonstrates the ability to not just build a server, but to ensure it meets specific legal and regulatory requirements.

### Skills Honed & Presented:

Regulatory Framework Mapping: Understanding how to apply complex government standards (NIST) to cloud resources.

Cloud Governance: Learning to use "Policy as Code" to maintain a security posture.

Audit Readiness: Preparing an environment for a third-party audit by using automated compliance tracking.

![Add NIST](./grcac/nist_on.png)
> *Fig 7.1: Governance Orchestration—Activating the NIST SP 800-53 Rev. 5 regulatory standard at the Tenant/Management Group scope. This transition from manual hardening to automated governance ensures that the NYC Franchise remains compliant with federal-grade security benchmarks.*

One of the most critical skills in Cloud GRC is verification. Because cloud platforms can have "eventual consistency" (delays in settings taking effect), we are performing a secondary audit of our own governance engine. This ensures that the regulatory "Guardrails" we intend to have in place are actually active and hasn't just been a visual glitch in the UI.

Skills Honed & Presented:

Security Control Validation: Going beyond the "Dashboard" to verify underlying resource assignments.

Troubleshooting Governance Engines: Identifying when a policy assignment fails to propagate across a tenant.

Audit Trail Management: Ensuring that there is a documented record (the Assignment) of the security standard being applied.

![Nist assignment evidence](./grcac/nist_assign_confirm.png)
> *Fig 7.2: Governance Verification—Confirming the active assignment of the NIST SP 800-53 initiative within the Azure Policy engine. This confirms that the governance 'Guardrails' are legally active and the automated auditing of the NYC Franchise has commenced.*

We identified a gap between "Defining a Standard" and "Assigning a Standard." This is a crucial distinction in GRC. Simply having a policy available in the library does nothing for security; it must be explicitly assigned to a scope (the Subscription) to begin the audit process. We are now executing that assignment to bridge the gap.

Scope Definition: Mastering how to apply security controls to specific organizational boundaries (Subscriptions/Resource Groups).

Policy Initiative Deployment: Hands-on experience deploying large-scale security frameworks (Initiatives) rather than single rules (Policies).

GRC Workflow: Navigating the lifecycle of policy implementation from definition to active assignment.

Having both assignments is a great safety net. The Tenant Group assignment applies the "Law" to everything in your entire Azure directory, while the Subscription assignment ensures your specific project area is the primary focus.
![](./grcac/policy_2.png)
> *Fig 7.3: Formal Policy Assignment—Successfully assigning the NIST SP 800-53 Rev. 5 initiative to the NYC-Franchise-Prod subscription. This action initiates the continuous automated audit of all infrastructure components against 1,000+ security sub-controls.*

In a real enterprise, you often deal with "Policy Overlap" where the corporate office (Tenant level) and the local branch (Subscription level) both apply standards. We have intentionally left both active to ensure maximum coverage. We are also utilizing the Azure CLI/PowerShell to force a compliance evaluation, demonstrating that we don't just wait for the cloud—we know how to drive it.

Hierarchical Policy Management: Understanding how policies inherit from Tenant down to Subscription.

Proactive Compliance Auditing: Using CLI/PowerShell to initiate on-demand compliance scans (MTTR reduction).

Administrative Governance: Differentiating between "Operational" accounts (EMRG) and "Governance" accounts (Global Admin).

![](./grcac/ps_policy_run.png)
> *Fig 7.4: Proactive Governance—Executing an on-demand compliance scan via PowerShell. This bypasses standard evaluation latency and ensures the NYC Franchise infrastructure is immediately audited against the newly assigned NIST 800-53 controls.*

Real-world cloud engineering involves dealing with "API Latency." When the manual trigger command hung, we pivoted from PowerShell to the Azure CLI (az policy state) to verify the instruction. This demonstrates Technical Versatility—not being locked into one tool when a session fails.

Cross-Platform CLI Proficiency: Using both PowerShell and Bash/Azure CLI to manage resource states.

Asynchronous Operation Management: Understanding that cloud commands often run "In the background" (Asynchronously) even if the terminal appears frozen.

Resilience in Administration: Maintaining progress by verifying dashboard states when command-line tools hit a latency wall.

![Bash alternative trigger for compliance policy](./grcac/bash_policy_trigger.png)
> *Fig 7.5: Cross-Tool Verification—Utilizing the Azure CLI (Bash) to trigger a compliance state evaluation after a PowerShell session timeout. This ensures the audit engine is actively processing the NYC Franchise resources against the NIST framework.*

When command-line tools fail to provide immediate feedback, a security professional must pivot to platform-level logging. By checking the Activity Log, we are verifying that the "Handshake" between our NYC terminal and the Azure Policy Engine actually occurred. This confirms that the NIST 800-53 audit is currently running in the background, regardless of the terminal's lack of output.

Audit Trail Verification: Using the Azure Activity Log to confirm administrative actions.

Incident/Task Validation: Proving that a security-critical task (Compliance Scan) was initiated.

Platform Resilience: Overcoming UI/CLI "silence" by using deeper system logs.

![](./grcac/policy_trigger_confirm.png)
> *Fig 7.7: Audit Trail Validation—Verifying the successful manual trigger of the NIST 800-53 compliance scan via the Azure Activity Log. This provides non-repudiation proof that the governance audit was initiated despite CLI session timeouts.*
