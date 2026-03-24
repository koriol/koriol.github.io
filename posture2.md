# Cloud Security Posture Baseline & SIEM Visualization

## Triage & Hardening
Now that you have documented the "chaos" of your baseline, Phase 2 is where you transform from a passive observer into an active Security Analyst. You will move from simply seeing the 32 High-Severity incidents to investigating, neutralizing, and preventing them from recurring. This phase is the "Action" part of your portfolio that proves you can reduce an organization's attack surface.

Main Tools: Microsoft Defender for Endpoint/Identity, Microsoft Entra Conditional Access, Microsoft Sentinel Incident Management.

Core Skills: Incident Response (IR), Risk Mitigation, Conditional Access Policy Design, Log Analysis, and Identity Protection.

Why: Establishing a baseline (Phase 1) is useless without a remediation plan. Phase 2 aligns with NIST 800-53 IR-4 (Incident Handling) and AC-2 (Account Management), showing you can execute the full lifecycle of a security event.

### Roadmap

Phase 2 Roadmap: From Detection to Defense
1. The Triage Sprint
Step: Categorize and "Claim" the 32 High-Severity incidents. You will perform a "True Positive vs. Benign Positive" analysis.

Why: In a real SOC, you must prioritize. You will identify if these alerts are actual brute-force attacks or just misconfigured service accounts.

2. Root Cause Analysis (RCA)
Step: Drill into the top 5 targeted users identified in your KQL bar chart. Investigate the UserEntity and IPEntity to see where the attacks are originating.

Why: Fixing one alert is a bandage; finding the source is a cure. This demonstrates your ability to perform deep-dive forensics.

3. Identity Perimeter Hardening (The "Wall")
Step: Deploy Conditional Access Policies to block the specific geographic threats visualized in your Phase 1 map.

Why: This is your primary "Hardening" task. By implementing "Location-Based Blocking" and "MFA Enforcement," you are proactively stopping the next 32 incidents before they happen.

4. Automated Remediation (The "Future")
Step: Configure a "Playbook" or "Automation Rule" in Sentinel to automatically assign "Unassigned" incidents to a specific owner or close "Informational" alerts.

Why: This showcases your interest in SOAR (Security Orchestration, Automation, and Response), proving you know how to scale security efforts using automation.

***

Technical Hurdle: "Encountered a permission propagation delay after activating Privileged Identity Management (PIM) roles. Despite 'Security Administrator' status being active in Entra ID, the unified Defender portal failed to render the full administrative sidebar."

Resolution: "Applied a session-level 'Force Refresh' by performing a full logout and re-authenticating via an incognito session. This forced a refresh of the JSON Web Token (JWT), ensuring the new administrative claims were recognized by the Microsoft Defender XDR engine."

Skills Honed & Why
Identity & Access Management (IAM): You are demonstrating hands-on experience with Just-In-Time (JIT) access.

NIST 800-53 AC-2 (PIM/PAM): This maps to Privileged Access Management. Using PIM instead of staying "Permanently Admin" is a high-level security practice that protects against credential theft.

Observation: "Upon transitioning to the dedicated Security Analyst account (Alan Turing), the incident queue initially appeared empty due to default portal filters."

Resolution: "I performed a global filter reset, expanding the lookback period and status parameters to reveal the 32 High-Severity incidents identified in the baseline phase. I then formally assumed ownership of the top priority alerts, transitioning them from 'New' to 'Active' status."

GRC Alignment: "This action demonstrates compliance with NIST 800-53 IR-4, ensuring that every critical alert has a designated human respondent and a tracked lifecycle."

Challenge: "Encountered a persistent UI rendering issue where the Microsoft Sentinel incident blade failed to populate despite active telemetry. I identified this as a synchronization lag within the Unified Defender Portal."

Technical Workaround: "I pivoted to a data-centric approach, utilizing KQL Advanced Hunting to query the SecurityIncident table directly. This bypassed the UI limitations and provided a verifiable list of the 32 High-Severity incidents requiring triage."

Strategy: "To overcome persistent UI synchronization delays between the Sentinel workspace and the unified Defender XDR portal, I utilized the Emergency Access (Break Glass) account to perform a bulk assignment of the top 5 high-severity incidents to the Alan Turing Security Analyst account."

Security Justification: "This allowed for a clean transition of duties, ensuring that the dedicated analyst account had immediate visibility into the prioritized workload without requiring persistent Global Administrator rights. This move reinforces the Separation of Duties and Least Privilege principles (NIST 800-53 AC-5)."

Strategic Shift: "With 30 of the 32 baseline incidents successfully resolved, the project focus transitioned from active Incident Response to Security Posture Hardening. I identified that while the immediate threats were neutralized, the underlying vulnerabilities—reflected in a Secure Score of 39%—remained."

Analysis: "I utilized Microsoft Defender Exposure Management to identify high-impact recommendations. This proactive approach aligns with NIST 800-53 CA-7 (Continuous Monitoring), where the goal is to systematically reduce the attack surface to prevent the recurrence of the previously observed brute-force attempts."

Strategic Observation: "Upon assuming the Security Analyst role, I noted that while the active incident queue was clear, the Identity Exposure Score was critically low at 22.2%. This indicated that the underlying vulnerabilities used in previous brute-force attempts remained unpatched."

Decision Matrix: "I pivoted the project focus from reactive incident monitoring to Proactive Attack Surface Reduction. By targeting Identity misconfigurations, I am addressing the root cause of credential-based attacks rather than just the symptoms (alerts)."

Implementation: "I initiated a hardening sprint focused on NIST 800-53 AC-2 (Account Management) and IA-2 (Identification and Authentication), beginning with the enforcement of tenant-wide Multi-Factor Authentication (MFA) via Conditional Access."

![The Identity score (22.2%) dashboard in Exposure Management.](./posture/identity_score.png)
> *Figure 2.1: Baseline Identity Risk Assessment - 22.2% Configuration Score.*

![](./posture/mfa_secure_score.png)
> *Figure 2.1: Identity Exposure Analysis - Identifying Critical Vulnerabilities in Credential Management.*

![The Conditional Access 'Grant' controls for MFA.](./posture/grant_mfa_baseline.png)
> *Figure 2.2: Hardening Execution - Enforcing MFA for the Identity Perimeter.*

Skills Honed & Why
Security Posture Management (CSPM): Demonstrating the ability to use automated scoring systems to guide security strategy.

Identity & Access Management (IAM): Hands-on experience with the most critical layer of cloud security.

Risk-Based Prioritization: Showing you can look at a long list of problems and pick the one that reduces the most risk.

During the remediation phase, I observed a calculation lag between the Exposure Management Secure Score and the Identity Recommendations list. While the high-level Identity score reflected a 2% improvement (reaching 24.2%), the individual recommendations remained in an 'Active' state. I identified this as standard platform latency, where global posture metrics often aggregate faster than granular control-state verifications.

Observation: "Identified a 2% improvement in the Identity Security Posture within the Secure Score dashboard immediately following the deployment of Conditional Access policies. However, the Recommendations engine exhibited a 15-minute sync delay before marking the specific controls as 'Completed'."

Technical Insight: "This behavior highlights the importance of multi-vector auditing. In a real-world SOC, a Security Analyst must verify the 'Effective State' (the policy is on) rather than relying solely on 'Reporting State' (the score has updated)."

Skills Honed & Why
Audit Trail Verification: Understanding that a security control is only "done" when the auditor's engine sees it.

Cloud Platform Nuance: Navigating the specific sync behaviors of the Microsoft Defender XDR stack.

Data Integrity: Ensuring that your portfolio reflects the actual state of the environment, including the "hiccups" of cloud processing.

***

Goal: "Implement adaptive security controls to mitigate identity-based attacks using Microsoft Entra ID Protection."

Strategy: "Deployed a risk-based Conditional Access policy targeting 'Medium' and 'High' sign-in risks. This ensures that legitimate users are only challenged with MFA when the system detects anomalous behavior, reducing 'MFA Fatigue' while maintaining a high security bar (NIST 800-53 IA-2)."

Governance Note: "Maintained a strict exclusion for the 'Break Glass' account to prevent catastrophic lockout during high-risk scenarios, balancing automated protection with operational resilience."

Skills Honed & Why
Adaptive Access Control: Moving beyond static "Always-On" MFA to intelligent, risk-aware security.

Risk Management: Learning to calibrate security "friction" based on the severity of the threat.

Operational Safety: Correcting potential lockout vectors while deploying aggressive security policies.

![The 'Conditions' pane showing Medium/High risk selected.](./posture/med_hi_conditions.png)
> *Figure 2.5: Adaptive Security - Configuring AI-Driven Risk Thresholds.*

![The 'Grant' pane showing the MFA requirement.](./posture/req_mfa.png)
> *Figure 2.6: Risk-Based Remediation - Automated MFA Challenges for Suspicious Logins.*

Technical Adaptation: "Identified a synchronization lag between the Microsoft Defender XDR portal and the Entra ID primary identity store. I pivoted to using Entra ID Secure Score as the authoritative metric, documenting a jump from 22.2% to 34% following the implementation of Risk-Based MFA."

Security Strategy: "Recognized that MFA is only effective if 'backdoor' entry points are sealed. I deployed a policy to Block Legacy Authentication, effectively closing off protocols like POP3 and IMAP that do not support modern MFA challenges, aligning with NIST 800-53 AC-17 (Remote Access)."

![The Entra ID Secure Score dashboard showing 34%.](./posture/ss_33.png)
> *Figure 2.7: Real-Time Posture Validation - Identity Score Increase to 33% (via Entra ID).*

![The 'Client Apps' condition showing 'Other clients' selected for blocking.](./posture/legacy_conditions.png)
> *Figure 2.8: Protocol Hardening - Eliminating Non-MFA Legacy Authentication Paths.*

Skills Honed & Why
Cross-Portal Navigation: Demonstrating the ability to find the "Source of Truth" when unified dashboards lag.

Attack Surface Minimization: Understanding that identity security requires both "Adding" (MFA) and "Subtracting" (Blocking Legacy Auth).

Protocol Analysis: Knowledge of which connection types (Modern vs. Legacy) represent the highest risk to the tenant.

Policy ID,Policy Name,Objective,NIST 800-53 Mapping
CA001,Foundational MFA,Enforce MFA for all user sessions to prevent credential stuffing.,IA-2 (1)
CA002,Risk-Based MFA,Trigger MFA/Password reset only when AI detects Medium/High risk.,SI-4 (Information Monitoring)
CA003,Block Legacy Auth,"Close ""Backdoor"" entry points (IMAP/POP3) that bypass MFA.",AC-17 (Remote Access)
CA004,Geo-Blocking,Prevent authentications from unauthorized geographic regions.,AC-3 (Access Enforcement)

![The Secure Score History graph showing the +2% uptick.](./posture/mfa_uptick.png)
> *Figure 2.4: Quantifiable Impact - Measurable Improvement in Identity Posture.*

***

#### Geo-Blocking

Goal: "Implement Geographic Fencing (Geo-blocking) to neutralize automated global brute-force attacks."

Strategy: "Leveraged the threat intelligence gathered in Phase 1 (KQL Global Threat Map) to identify unauthorized login origins. I established a 'Trusted Location' baseline and deployed a 'Block-by-Exclusion' policy. This ensures that any authentication attempt originating from outside authorized jurisdictions is dropped at the edge, significantly reducing the tenant's attack surface."

GRC Alignment: "This control aligns with NIST 800-53 AC-3 (Access Enforcement) by restricting access based on physical and logical location parameters."

Skills Honed & Why
Network Security: Understanding how to use IP-based location data as a security signal.

Risk Mitigation: Proactively stopping attacks before the "MFA" or "Password" stage is even reached.

Zero Trust Architecture: Moving toward a model where "Location" is a required verified claim for access.

![The list of 'Allowed Countries' in the Named Locations menu.](./posture/countries.png)
> *Figure 2.11: Defining the Trust Boundary - Establishing Geographic Named Locations.*

![The 'Locations' condition showing 'Include: Any' and 'Exclude: Allowed'.](./posture/exclude_us.png)
> *Figure 2.12: Edge Defense - Implementing Global Geo-Blocking via Conditional Access.*

"Following the deployment of CA003 (Block Legacy Auth) and CA004 (Geo-Blocking), I observed that the Entra ID Secure Score remained static. Investigation into the 'Status Description' revealed that the compliance engine's last assessment was dated 2/26/2026. This highlights a critical lesson in Security Operations: Configuration state and Reporting state are decoupled. I verified the active enforcement of these controls by inspecting the Conditional Access policy engine directly."

Skills Honed & Why
Control Validation: Using the "What If" tool to verify logic without needing a live attacker.

Audit Interpretation: Learning to read "Status Descriptions" to explain why reports don't match reality.

Persistence: Continuing the hardening roadmap despite reporting latency.









































