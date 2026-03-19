# LMS Ecosystem Integration & Security Compliance

## The Foundation: The Brightspace Core

### Building the Compliant Architecture
Before a single video is recorded or a paper is submitted, the Infrastructure must be sound. In this phase, I am the System Architect. I am "uploading files" and, more importantly, provisioning a secure, accessible, and logic-gated environment.

#### Tools
* **D2L Brightspace:** The primary Enterprise LMS.
* **Brightspace Accessibility Checker:** The internal "Compliance Auditor."
* **LTI 1.3 (Zoom Integration):** The Federated Identity/SSO connector.

#### Skills
* **Infrastructure Provisioning:** Building hierarchical data structures.
* **Identity & Access Management (IAM):** Configuring secure entry points via LTI.
* **Compliance Auditing:** Validating digital assets against WCAG 2.1 standards.

***

### Provisioning the 'Cardiology' Unit & SSO Entry
When setting up a new unit in a medical environment, we follow the Principle of Least Privilege. We keep the unit "Hidden" (in Draft mode) while building. We also ensure that synchronous tools (Zoom) are added via LTI 1.3 rather than raw URLs. This ensures that only users with a valid, authenticated session token from the LMS can enter the "Clinical Sync."

![](./brightspace/open_classroom.png)
> *Initialized the 'Advanced Cardiology' infrastructure within D2L Brightspace. Implemented LTI 1.3 for secure Zoom integration to enforce Identity and Access Management (IAM), and placed the unit in 'Hidden' status to maintain staging integrity during the build-out.*

***

### The Accessibility Audit: Digital Compliance
Accessibility is a legal requirement (Section 508/ADA compliance). As an Instructional Support Associate, I am the first line of defense. Before a student ever sees this 'Cardiology' unit, I must "audit" the HTML content to ensure it is readable by screen readers and navigable for students with disabilities.

Automated accessibility checkers are 'syntax-aware' but not 'context-aware.' They confirm the presence of an attribute but not its accuracy. As an Associate, I must verify that clinical data is meaningfully accessible, not just technically present.

![](./brightspace/alt_txt_false_positive.png)
> *Automated scan returned a False Positive, failing to identify non-descriptive Alt-Text.*

Identified a 'False Positive' in the automated accessibility scan. While the system marked the image as compliant, a manual audit revealed missing substantive Alt-Text for a critical clinical diagram. Remediated the 'Compliance Gap' by providing a descriptive text equivalent, ensuring the course meets WCAG 2.1 Level AA standards

![](./brightspace/alt_txt_remediation.png)
> *Manual remediation of image metadata to ensure WCAG 2.1 compliance for medical diagrams.*

***

### The Access Control: The "Lock"
In a medical curriculum, sequence matters. You wouldn't want a student taking a Cardiology Assessment before they've reviewed the Syllabus and the Introductory material. In Cybersecurity terms, we are implementing Conditional Access. The "Condition" is: If User has 'Visited' [Syllabus] AND [Intro Page], THEN 'Grant Access' to [Quiz].

![](./brightspace/release_conditions.png)
> *Configured logic-based Access Control (Release Conditions) to enforce sequential learning. This simulates an Attribute-Based Access Control (ABAC) model, ensuring students satisfy compliance prerequisites before accessing high-stakes assessments.*

***

### Phase 1 Summary:
* **Mission:** Infrastructure & Compliance.
* **Tools:** Brightspace, Accessibility Checker, LTI 1.3.
* **Outcome:** A secure, audited, and gated module ready for multimedia.









