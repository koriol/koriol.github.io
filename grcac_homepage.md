# Regulatory Compliance & Governance as Code
### The Objective
The NYC-Franchise-Prod project is a comprehensive simulation of an enterprise-grade security deployment. It bridges the gap between infrastructure-as-code and security operations (SecOps) by moving through the entire lifecycle of a cloud asset: from initial provisioning to active threat hunting and remediation.

In modern cloud environments, a "Perimeter-Only" defense is insufficient. This project was designed to:
* **Bridge Compliance and Action:** Moving beyond "paper" security by implementing actual NIST 800-53 technical controls (AC-3, IA-2, SI-4).
* **Validate Detection Engineering:** Proving that custom telemetry (KQL) and Watchlists can detect "Low and Slow" attacks that standard alerts might miss.
* **Demonstrate Full-Spectrum Capability:** Showing competence in networking, Linux administration, identity management, and incident response within a single narrative.

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

### Phase 4: SIEM and Incident Reporting
[Phase 4 page](./grcac-phase-4.md)

### Phase 5: Incident Simulation
You’ll run a simple script to "Attack" your VM. Since your SIEM is already "tuned," it will catch it instantly.
[Phase 5 page](./grcac-phase-5.md)

### Phase 6: Final Reporting
We export the NIST dashboard and grab the final "Green" score.
[Phase 6 page](./grcac-phase-6.md)

Action: Export the Regulatory Compliance Report as a PDF/CSV.

Outcome: This report is what you’d hand to a CEO or an Auditor to prove the franchise is secure.
[Phase 4 page](./grcac-phase-4.md)

### Lessons Learned

* **The Latency Factor:** Real-world cloud logging isn't instantaneous. Understanding ingestion delay is vital for accurate incident timelines.
* **Protocol Precision:** Troubleshooting SSH naming conventions and IPv4/IPv6 mismatches highlighted the necessity of deep OS-level knowledge in security roles.
* **Governance Matters:** Security is only as good as its documentation. Mapping actions to the MITRE ATT&CK framework provided the "Language" needed to communicate risk to stakeholders.

### Conclusions & Reflections
This project transformed my understanding of "Security" from a static state to a continuous process. By building the environment from scratch, I learned that true security isn't about the tools themselves, but the integration between them. Seeing a custom KQL query catch a "backdoor" user in real-time was the ultimate validation of the "Assume Breach" mindset.
