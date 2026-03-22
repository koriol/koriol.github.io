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
















































