# Regulatory Compliance & Governance as Code
### The Objective
To transition from a "Wild West" cloud setup to a Governed Enterprise Environment. You will use Microsoft’s automation tools to audit your NYC Franchise against the NIST SP 800-53 (the gold standard for US government/enterprise security) and enforce "Guardrails" that prevent insecure configurations.

### Skills
**Compliance Mapping:** Understanding how technical settings (like disk encryption) map to legal requirements (like NIST or HIPAA).

**Policy Management:** Creating "Deny" policies to stop security leaks before they happen.

**Remediation:** Fixing "Non-Compliant" resources using automated tasks.

**Cloud Governance:** Demonstrating "Least Privilege" at the resource level.

### Tools
**Primary Tool:** Microsoft Defender for Cloud (The Compliance Dashboard).

**Engine:** Azure Policy.

**Standards:** NIST SP 800-53 Rev. 5 (or the Microsoft Cloud Security Benchmark).

## Roadmap
### Phase 1: The Compliance Baseline (The Audit)
You will connect your subscription to the Regulatory Compliance dashboard.

Action: Assign the "NIST 800-53" or "Microsoft Cloud Security Benchmark" initiative to your RG-NYC-Franchise.

Outcome: A "Scary" dashboard showing exactly how many security rules you are currently breaking.
[Phase 1 page](./grcac-phase-1.md)

### Phase 2: Implementing "Guardrails" (The Law)
You will move from "watching" to "enforcing."

Action: Create an Azure Policy that Denies the creation of any VM that doesn't have Managed Disks or any Storage Account that allows Public Access.

Test: You will try to create a "broken" resource and show a screenshot of Azure blocking you. (This is a huge portfolio shot).
[Phase 2 page](./grcac-phase-2.md)

### Phase 3: Remediation (The Fix)
Instead of fixing things manually, you'll use the "Fix It" button.

Action: Identify a non-compliant setting (like "Diagnostic Logs not enabled") and trigger a Remediation Task.

Outcome: Watching Azure automatically update your resources to meet the legal standard.
[Phase 3 page](./grcac-phase-3.md)

### Phase 4: The GRC Executive Report
The final deliverable.

Action: Export the Regulatory Compliance Report as a PDF/CSV.

Outcome: This report is what you’d hand to a CEO or an Auditor to prove the franchise is secure.
[Phase 4 page](./grcac-phase-4.md)

### Results
I implemented a Governance framework using Azure Policy to enforce NIST 800-53 standards, reducing the attack surface by 40% through automated remediation of non-compliant resources.
