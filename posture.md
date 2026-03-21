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

![Defender for Cloud Secure Score dashboard.](./posture/)
> *Figure 1.2: Pre-Remediation Baseline - Initial Cloud Secure Score.*

![The "Security Operations Efficiency" workbook.](./posture/)
> *Figure 1.3: Baseline SIEM Metrics - Operational Efficiency Overview.*

![KQL query yields results](./posture/)
> *Figure 1.4: Real-time Threat Visualization - Global Failed Sign-ins.*

#### Capturing the Baseline
Standardization is key for a professional audit. Instead of reinventing the wheel, I am leveraging Microsoft’s industry-standard templates to see how a 'healthy' SOC (Security Operations Center) measures efficiency. Seeing 'zeros' here isn't a failure—it’s the clean slate I need to prove my hardening works later.

#### Visualizing the Global Threat Landscape
Data in a table is hard to digest quickly. By using KQL to project failed logins onto a global map, I am creating an 'Executive View.' It immediately communicates the reality of the threat landscape: that this tenant is being probed by automated bots from across the globe, justifying the need for stricter Geo-blocking or Conditional Access.

#### Quantifying Risk
I need a benchmark that isn't just 'my opinion.' Secure Score provides a third-party, framework-aligned percentage. This serves as the primary KPI (Key Performance Indicator) for the project. If I move this needle from 30% to 70%, I have quantifiable proof of my value as a security professional.

#### Identifying Targeted Assets
A map shows where they are, but a bar chart shows who they want. By filtering for the top 5 targeted users, I am transitioning from a reactive posture to a proactive one. This allows me to recommend targeted training or extra security layers for the most 'at-risk' individuals in the organization.

### 






































