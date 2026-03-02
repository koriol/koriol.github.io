# Modern Workplace Security & Identity

## Introduction
Recognizing the specific toolstack requirements for Agency Cybersecurity, I synthesized a high-intensity 'Interview Sprint' focused on Identity Governance and Administration (IGA) and Endpoint Security. By integrating JumpCloud and CrowdStrike into my existing Azure lab, I've moved from theoretical knowledge to hands-on proficiency in the exact platforms used by the hiring team. This demonstrates an 'Architect's Mindset'—the ability to pivot technical skills rapidly to meet organizational needs and compliance frameworks like SOC2 and ISO 27001.

### Just-In-Time (JIT) Administrative Elevation
To maintain a hardened security posture and adhere to NIST 800-53 (AC-6: Least Privilege), my environment is configured with a maximum of three permanent administrators. Routine administrative accounts, such as Aturing, do not hold standing "Global Administrator" privileges. Before integrating a third-party Identity Provider (IdP) like JumpCloud, I must utilize Azure Privileged Identity Management (PIM) to temporarily elevate my account. This ensures that high-level "Owner" permissions are only active during the 4-hour window required for the OAuth 2.0 handshake, reducing the "blast radius" of the account.

<u>**Skilss Applied**</u>
* **Privileged Identity Management (PIM):** Managing the lifecycle of "Eligible" vs. "Active" roles.
* **Identity Governance:** Enforcing time-bound access for critical infrastructure changes.
* **Audit Logging:** Creating a documented trail of why and when elevation occurred.

![](./pim_activated.png)
> *Fig 1.1: JIT Elevation via Azure PIM—Temporarily activating the Global Administrator role for the NYC-ADMIN-Aturing account. This 4-hour window provides the necessary consent level for the JumpCloud directory integration while maintaining NIST 800-53 compliance.*


## JumpCloud & Identity
















