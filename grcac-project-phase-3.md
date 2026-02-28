# Governance and Compliance

## Phase 3: Remediation (The "Security Contact" Fix)

Now that the assessment is complete, we are beginning the Remediation phase. Our audit flagged a major operational risk: the lack of a designated security contact. If a "Break-Glass" account is activated or a brute-force attack is detected, Microsoft has no way to alert the NYC Franchise admins. By configuring these settings, we are formally closing a gap in the Incident Response (IR) family of NIST controls. This ensures that the technical alerts we built in the SIEM (Sentinel) have a corresponding "Human in the Loop" notification system.

Security Operations Center (SOC) Setup: Establishing the fundamental alerting pathways for a cloud environment.

Incident Response Readiness: Implementing automated notification workflows to reduce Mean Time to Respond (MTTR).

Control-Specific Remediation: Directly addressing NIST 800-53 IR-6 (Incident Reporting) requirements.

![Remediation for email notifications](./grcac/email_notifications.png)
> *Fig 9.1: Critical Control Remediation—Establishing formal security contact notifications within Microsoft Defender for Cloud. This configuration satisfies NIST 800-53 IR-6, ensuring that high-severity security telemetry is proactively pushed to the NYC Franchise administration for immediate response.*



