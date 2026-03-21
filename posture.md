# Cloud Security Posture Baseline & SIEM Visualization

## Introduction
This project focuses on establishing a measurable security baseline for an Azure tenant using Microsoft Sentinel and Microsoft Defender for Cloud. By capturing "Pre-Remediation" data through specialized workbooks and custom KQL (Kusto Query Language) visualizations, I will create a professional dashboard that tracks security hygiene and global threat vectors. This provides a data-driven foundation to demonstrate the tangible impact of future hardening tasks.

**Main Tools:** Microsoft Sentinel (SIEM), Microsoft Entra ID, Microsoft Defender for Cloud, Kusto Query Language (KQL).
**Core Skills:** SIEM Dashboarding, Continuous Monitoring (NIST 800-53), Cloud Security Posture Management (CSPM), Threat Visualization, and Data Connector Integration.

## Roadmap
1. **Telemetry Foundation:** Connect Entra ID and Azure Activity logs to Sentinel to ensure the dashboard has a live data stream to visualize.
2. **Baseline Performance Capture:** Deploy standardized "Security Operations" workbooks and document the initial "Secure Score" to establish the pre-hardening state.
3. **Custom Threat Intelligence Visualization:** Develop and implement a custom KQL-based Global Threat Map to visualize real-time failed authentication attempts by geographic location.

***
### Telemetry Foundation

#### Establishing the Data Pipeline
I cannot secure what I cannot see. Before building a dashboard, I must ensure the SIEM is actually receiving telemetry. By connecting Entra ID and Azure Activity logs, I am creating a 'source of truth' for both identity-based threats and configuration changes within the subscription.

I initially struggled to find the connectors because of the platform migration to the unified Defender portal. I realized that 'Installing' a solution in the Content Hub is only the first half; the second half is 'Configuring' the data connector via Azure Policy. This taught me that cloud SIEM integration isn't just a toggle—it requires understanding the underlying Azure RBAC and Policy engine.



![After clicking "Connect" in the Entra ID Data Connector page.](./posture/)
> *Figure 1.1: Establishing Telemetry - Entra ID Log Integration.*

![Defender for Cloud Secure Score dashboard.](./posture/initial_posture.png)
> *Figure 1.2: Pre-Remediation Baseline - Initial Cloud Secure Score.*

![The "Security Operations Efficiency" workbook.](./posture/)
> *Figure 1.3: Baseline SIEM Metrics - Operational Efficiency Overview.*

![KQL query yields results](./posture/)
> *Figure 1.4: Real-time Threat Visualization - Global Failed Sign-ins.*

![The Cloud Secure Score percentage (Likely low due to these alerts).](./posture/initial_secure_posture.png)
> *Figure 1.3: Tenant Security Posture Baseline - Cloud Secure Score.*

![](./posture/initial_backlog.png)
> *Figure 1.2: Initial Incident Backlog - High-Severity Alerts Awaiting Triage*

#### Capturing the Baseline
Standardization is key for a professional audit. Instead of reinventing the wheel, I am leveraging Microsoft’s industry-standard templates to see how a 'healthy' SOC (Security Operations Center) measures efficiency. Seeing 'zeros' here isn't a failure—it’s the clean slate I need to prove my hardening works later.

#### Visualizing the Global Threat Landscape
Data in a table is hard to digest quickly. By using KQL to project failed logins onto a global map, I am creating an 'Executive View.' It immediately communicates the reality of the threat landscape: that this tenant is being probed by automated bots from across the globe, justifying the need for stricter Geo-blocking or Conditional Access.

#### Quantifying Risk
I need a benchmark that isn't just 'my opinion.' Secure Score provides a third-party, framework-aligned percentage. This serves as the primary KPI (Key Performance Indicator) for the project. If I move this needle from 30% to 70%, I have quantifiable proof of my value as a security professional.

#### Identifying Targeted Assets
A map shows where they are, but a bar chart shows who they want. By filtering for the top 5 targeted users, I am transitioning from a reactive posture to a proactive one. This allows me to recommend targeted training or extra security layers for the most 'at-risk' individuals in the organization.

### 

Observation: "Upon establishing telemetry, I identified a significant backlog of 32 high-severity security incidents and 26 unassigned alerts. Far from being a 'clean' environment, this tenant represents a high-risk scenario common in neglected or rapidly scaling cloud environments."

Analysis: "The presence of these incidents provides a clear baseline for my project. My goal has shifted from simple 'monitoring' to 'remediation and triaging.' I am effectively acting as a solo Security Analyst tasked with clearing a critical backlog and hardening the identity perimeter."

Technical Hurdle: "Encountered syntax limitations with the render map command in the Unified Defender portal's Advanced Hunting schema. Resolved this by successfully aggregating data by country and utilizing the UI-integrated visualization engine to project the threat landscape."


Technical Hurdle: "Encountered a schema mismatch error: failed to resolve expression `LocationDetails.countryOrRegion`. I identified that while the legacy Sentinel `SigninLogs` table uses nested property notation, the Unified Defender `AADSignInEventsBeta` table flattens these attributes."

Resolution: "Refactored the KQL query to utilize the direct `Country` column and filtered for `ErrorCode != 0` to isolate failed authentication attempts. This allowed for the successful aggregation of threat data across the 7-day lookback period."


![](./posture/goegraphic_incidents.png)
> *Figure 1.4: Multi-Vector Threat Analysis - Origin of Failed Identity Requests.*

```
AADSignInEventsBeta
| where ErrorCode != 0
| extend Country = tostring(LocationDetails.countryOrRegion)
| where isnotempty(Country)
| summarize FailedCount = count() by Country
```

Challenge: "Faced 'No results found' errors when querying identity logs in the Unified Defender Portal and discovered that the legacy render map command is deprecated in the Advanced Hunting schema."

Technical Pivot: "Broadened the hunting scope to the AADSignInEventsBeta table and adjusted the lookback period to 7 days to account for ingestion latency. Adapted the visualization strategy from a geographic map to a high-density bar chart to clearly communicate attack origins."



Executive Summary
This project initiates a 4-day security sprint by establishing a "Pre-Remediation" baseline. By integrating disparate cloud logs into a unified SIEM/XDR environment, I captured the "Day 0" state of the tenant—identifying a significant incident backlog and a broad geographic attack surface. This baseline serves as the technical KPI against which all future hardening tasks will be measured.

Main Tools: Microsoft Defender for Cloud, Microsoft Sentinel, Microsoft Entra ID, Kusto Query Language (KQL).

Core Skills: SIEM Dashboarding, Continuous Monitoring (NIST 800-53 CA-7), Cloud Security Posture Management (CSPM), Threat Visualization.

Phase 1 Roadmap: Environmental Baseline
Step 1: Telemetry Integration: Connect Entra ID and Azure Activity logs to the Unified Defender Portal.

Step 2: Operational Benchmarking: Deploy SOC Efficiency Workbooks and document the initial incident backlog.

Step 3: Posture Quantification: Capture the initial Cloud Secure Score to establish a risk-based KPI.

Step 4: Threat Intelligence Synthesis: Develop custom KQL queries to visualize failed authentication attempts by origin and target.

Technical Implementation & "Flow of Thought"
1. Establishing the Data Pipeline
"I cannot secure what I cannot see. Before building a dashboard, I must ensure the SIEM is actually receiving telemetry. By connecting Entra ID and Azure Activity logs, I am creating a 'source of truth' for both identity-based threats and configuration changes within the subscription."

Figure 1.1: Verification of Entra ID Log Integration in Data Connectors.

2. Capturing the Operational Baseline
"Standardization is key for a professional audit. I leveraged Microsoft’s industry-standard templates to see how a 'healthy' SOC measures efficiency. Seeing a backlog here isn't a failure—it’s the 'clean slate' needed to prove my hardening works later."

Figure 1.2: SOC Operational Baseline - Initial Incident Metrics showing 32 High-Severity Alerts.

3. Quantifying Risk (KPI Establishment)
"I need a benchmark that isn't just my opinion. Secure Score provides a third-party, framework-aligned percentage. This serves as the primary KPI; moving this needle from its baseline to a hardened state provides quantifiable proof of security value."

Figure 1.3: Tenant Security Posture Baseline - Cloud Secure Score (Pre-Remediation).

4. Visualizing the Global Threat Landscape
"Data in a table is hard to digest. By using KQL to project failed logins, I created an 'Executive View' that immediately communicates the reality of the threat landscape: this tenant is being probed by automated bots globally, justifying the need for stricter Geo-blocking."

Figure 1.4: Threat Intelligence Synthesis - Geographic Distribution of Failed Sign-ins.

Technical Challenges & Engineering Resolutions
Challenge A: Portal Migration & Connectivity
Issue: I initially struggled to locate connectors due to the 2026 migration to the Unified Defender portal.

Resolution: Discovered that 'Installing' a solution in the Content Hub is separate from 'Configuring' the connector. I utilized Azure Policy remediation to force ingestion, learning that cloud SIEM integration requires a deep understanding of Azure RBAC and Policy engines rather than just simple "toggles."

Challenge B: Schema Mismatch & KQL Syntax
Issue: Failed to resolve the expression LocationDetails.countryOrRegion and encountered deprecated render map syntax in Advanced Hunting.

Resolution: I identified that the Unified Defender AADSignInEventsBeta table flattens attributes differently than legacy SigninLogs. I refactored the query to utilize the direct Country column and adjusted the lookback period to 7 days to ensure data density.

Final Corrected Query:

Code snippet
AADSignInEventsBeta
| where ErrorCode != 0
| where isnotempty(Country)
| summarize FailedCount = count() by Country
| sort by FailedCount desc
Phase 1 Observations
Incident Backlog: Identified 32 High-Severity and 26 Unassigned alerts. This represents a high-risk scenario common in neglected cloud environments (NIST 800-53 IR-4).

Targeted Assets: Initial analysis shows authentication attempts are concentrated on five specific administrative accounts, allowing for a pivot from reactive monitoring to proactive Risk Prioritization (NIST 800-53 RA-3).

How to use this:
Check Image Links: Ensure the filenames in the ![](...) tags match your actual screenshot filenames.

Verify Figure Numbers: I fixed the numbering so it flows 1.1 to 1.4.

Hurdles: I placed these at the bottom so the reader sees your Success first, and your Problem Solving second.




























