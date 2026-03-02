# GRC and Governance as Code

## Phase 6: Persistence & Insider Threat

### Introduction
In Phase 5, we successfully blocked an external "Brute Force" attack at the network boundary (NIST 800-53 SC-7). However, advanced adversaries often aim for Persistence (MITRE ATT&CK TA0003)—maintaining access to a system even after restarts or credential changes.

In Phase 6, we will simulate a "Post-Compromise" scenario. We will act as an attacker who has gained temporary access and is now planting a "Backdoor" user and a scheduled "Phone Home" script. We will then use Sentinel Watchlists and KQL Behavior Analysis to detect this "Quiet" activity that doesn't trigger standard volume-based alerts.

**Phase 6 Roadmap: The "Hidden Guest"**
1. **Planting the Seed:** Creating a hidden "Backdoor" user on the Linux VM.
2. **The Persistence Loop:** Configuring a cron job to simulate "Command & Control" (C2) heartbeats.
3. **The Hunter’s Pivot:** Using KQL to identify "New User Creation" and "Unusual Process Execution."
4. **Watchlist Integration:** Creating a "High-Risk User" Watchlist in Sentinel to auto-flag any activity from our backdoor account.

<u>Targeted Skills</u>: Insider Threat Detection, Linux Audit Log Analysis, UEBA (User Entity Behavior Analytics) concepts.

<u>**Tools Applied**</u>

* Linux Terminal (sudo): For administrative backdoors.
* Microsoft Sentinel Watchlists: For "Gold Standard" account monitoring.
* KQL (Kusto Query Language): To track account management events.

***

During the transition to Phase 6, I performed a Connectivity Audit to ensure administrative access was aligned with my local hardware rather than ephemeral cloud resources. By updating the Network Security Group (NSG) 'Allow' rule to match my physical workstation's public IP, I solidified the Access Control (NIST 800-53 AC-3) baseline. This step was crucial for the 'Insider Threat' simulation, as it established a stable, authorized connection from which I could then simulate the escalation of privileges and the creation of unauthorized persistence mechanisms.

<u>**Skills Applied**</u>
* **Access Control Management:** Precisely managing IP-based whitelists to ensure continuous administrative availability.
* **Perimeter Synchronization:** Aligning cloud security rules with physical workstation metadata.

![](./grcac/updated_ip_rule.png)
> *Fig 25.0: Administrative Access Alignment—Updating the NSG whitelist to reflect the local management workstation. Ensuring a stable, authorized entry point is a prerequisite for testing internal persistence detection under NIST 800-53 AC-3.*

To establish the initial 'Administrative Bridge' for Phase 6, I utilized a PEM-encoded RSA Key Pair for authenticated access. This demonstrates the standard 'Hardened' state of the NYC-Franchise-Prod environment (NIST 800-53 IA-2). However, to simulate a realistic compromise where an attacker lacks the original private key, I maintained the 'Password Authentication' bypass. This allows the unauthorized 'backupadmin' account to access the system via a lower-security credential. This contrast—authorized key-based access vs. unauthorized password-based persistence—is a central theme of this detection simulation.

<u>**Skills Applied**</u>
* **SSH Key Management:** Utilizing identity files (`-i`) for secure, non-interactive authentication.
* **Credential Hierarchy:** Understanding the difference between high-assurance (Keys) and low-assurance (Passwords) authentication.

![](./grcac/ssh_login_1.png)
> *Fig 25.0.4: Secure Administrative Entry—Utilizing a PEM-encoded identity file to establish an authorized SSH session. This represents the high-assurance authentication baseline required by NIST 800-53 IA-2 before the simulation of 'Insider' credential degradation.*

***

### Planting the Backdoor (The "Hidden" User)
Having secured the network perimeter against external brute-force attempts, I progressed to Phase 6: Persistence Detection. This phase addresses the reality that perimeter defenses (NIST 800-53 SC-7) are not infallible. I shifted the focus to Internal Audit Review (AU-6) and Least Privilege Enforcement (AC-6) by simulating a 'Living off the Land' attack. By creating an unauthorized local account and a persistence mechanism (Cron Job), I am testing the SOC's ability to detect 'Low and Slow' movements that bypass traditional threshold-based triggers. This ensures the NYC-Franchise-Prod environment is resilient against sophisticated lateral movement and insider threats.

<u>**Skills Applied**</u>
* **Post-Compromise Awareness:** Understanding how attackers maintain access after the initial breach.
* **Behavioral Baseling:** Identifying what "Normal" looks like vs. "Malicious" user creation.
* **Sentinel Watchlist Engineering:** Leveraging static lists to enhance dynamic alerting.

![](./grcac/create_backupadmin.png)
> *Fig 25.1: Simulating Persistence—Creating an unauthorized 'backupadmin' account with sudo privileges. This 'Insider Threat' scenario tests the SIEM's ability to detect unauthorized account management (NIST 800-53 AC-2) that occurs behind the perimeter firewall.*

***

### The "C2 Heartbeat" (The Cron Job)
After establishing an unauthorized user account, I implemented a Command & Control (C2) Simulation using a Linux `cron` job. By scheduling a script to execute a `curl` request every minute, I simulated a 'Beaconing' behavior common in malware persistence. This move tests the SOC's ability to detect anomalous outbound traffic patterns and unauthorized scheduled tasks (NIST 800-53 AU-12). This progression is vital because while the account creation is a 'point-in-time' event, the cron job creates a continuous 'behavioral footprint' that can be hunted via KQL.

<u>**Skills Applied**</u>
* **Linux Persistence Mechanisms:** Understanding how attackers use system schedulers (`cron`) to maintain presence.
* **C2 Beaconing Simulation:** Creating repetitive network traffic to test anomaly detection.
* **Living off the Land (LotL):** Using standard system tools (`curl`, `cron`) to perform malicious actions.

![](./grcac/crontab_confirm.png)
> *Fig 25.2: Establishing Command & Control (C2) Persistence—Configuring a cron job to execute a 'phone-home' script every minute. This simulates a persistent beaconing threat, allowing us to test Sentinel's ability to detect repetitive, unauthorized system tasks under NIST 800-53 SI-4.*

***

### Hunting the "New User" with KQL
With the persistence mechanism active, I transitioned to the Detection & Hunting phase. I utilized Kusto Query Language (KQL) to perform a forensic audit of the Syslog table, specifically targeting account management events. By filtering for the useradd process and 'sudo' group modifications, I was able to pinpoint the exact timestamp of the unauthorized escalation. This mirrors the requirements of NIST 800-53 AU-6, demonstrating the ability to extract actionable security intelligence from raw system telemetry even when no automated alert has fired.

<u>**Skills Applied**</u>
* **Log Aggregation Analysis:** Querying centralized Syslog data to identify local system changes.
* **Account Management Audit:** Tracking the creation and elevation of users (NIST 800-53 AC-2).
* **Forensic Filtering:** Using specific process names and message strings to bypass irrelevant log noise.

![](./grcac/add_new_user_backupadmin.png)
> *Fig 26.1: Unauthorized Account Detection—Utilizing KQL to identify the creation of the 'backupadmin' account. This manual hunt verifies that the Azure Monitor Agent is successfully capturing account management telemetry, satisfying NIST 800-53 AU-12.*

***

### Hunting the "Heartbeat" (C2 Detection)
During the forensic analysis of the cron persistence mechanism, I identified a high-frequency telemetry pattern. By summarizing CRON process events by the hour, I observed a consistent 1:1 event-to-minute ratio. This Statistical Anomaly is a primary indicator of automated Command & Control (C2) activity. In a production environment, this triggers a transition from 'General Monitoring' to 'Targeted Investigation' under NIST 800-53 SI-4, as it identifies a non-human process executing unauthorized network requests (C2 Heartbeats).

<u>**Skills Applied**</u>
* **Beaconing Analysis:** Identifying repetitive, automated system tasks through frequency counts.
* **Temporal Correlation:** Matching the 'Real-World' passage of time to the 'Log-World' event volume.

![](./grcac/cron_heartbeat.png)
> *Fig 26.2: Behavioral Pattern Analysis—Identifying the C2 'Heartbeat.' The consistent frequency of the CRON process (roughly 1 event per minute) confirms the presence of an automated persistence mechanism, a key detection metric for NIST 800-53 AU-6.*

***

### The "High-Risk" Watchlist (Sentinel Engineering)
To institutionalize the detection of the 'backupadmin' entity, I implemented a Microsoft Sentinel Watchlist. This moves the SOC from a reactive 'Hunting' posture to a proactive 'Governed' posture. By maintaining a 'High-Risk User' list, any future telemetry associated with this account can be automatically escalated to a High-Severity incident. This satisfies the NIST 800-53 AC-2 (Account Management) requirement for monitoring unauthorized or high-risk accounts, ensuring that the 'NYC-Franchise-Prod' environment has a persistent memory of identified threats.

<u>**Skills Applied**</u>
* **Watchlist Engineering:** Creating and uploading custom datasets to enhance SIEM correlation.
* **Threat Intelligence Integration:** Converting a manual finding into a permanent security asset.

![](./grcac/create_watchlist.png)
> *Fig 27.1: Proactive Threat Intelligence—Implementing a 'High-Risk User' Watchlist. By codifying the 'backupadmin' entity into Sentinel's memory, we are automating the detection of future unauthorized activity, fulfilling NIST 800-53 AC-2.*

***

### Creating the "High-Risk User" Alert Rule
To automate the monitoring of unauthorized entities, I engineered a Watchlist-Driven Analytics Rule within the Microsoft Defender Unified Platform. This rule performs a real-time correlation between incoming `Syslog` telemetry and the `HighRiskUsers` watchlist. By utilizing the `has_any` operator in KQL, the system can now identify any activity associated with the 'backupadmin' account without requiring a static, hard-coded rule for every individual threat actor. This represents a scalable application of NIST 800-53 SI-4 (Information System Monitoring), shifting the SOC from manual hunting to automated, intelligence-led alerting.

<u>**Skills Applied**</u>
* **Dynamic Correlation:** Linking static watchlists to live telemetry streams.
* **Unified Security Operations:** Configuring Sentinel-based analytics within the Microsoft Defender portal.
* **Extraction & Mapping:** Using KQL to pull account names from unstructured log messages for entity mapping.

![](./grcac/active_rules_highrisk.png)
> *Fig 27.2: Intelligence-Led Detection—Configuring a High-Severity Analytics Rule linked to the 'HighRiskUsers' Watchlist. This automation ensures that any activity from the identified 'backupadmin' account triggers an immediate SOC response, satisfying NIST 800-53 SI-4.*

To ensure the detection logic was aligned with industry standards, I mapped the analytics rule to the MITRE ATT&CK Framework, specifically targeting Persistence (T1053.003 - Cron). By implementing Entity Mapping, I enabled Microsoft Defender's 'Fusion' engine to correlate raw logs with specific 'Host' and 'Account' objects. Furthermore, I configured Alert Grouping to consolidate repetitive telemetry into a single, high-fidelity incident. This demonstrates an understanding of NIST 800-53 AU-6, ensuring that the SOC is not overwhelmed by 'Alert Fatigue' while maintaining a complete audit trail of the adversary's actions.

<u>**Skills Applied**</u>
* **MITRE ATT&CK Mapping:** Aligning custom detections with globally recognized adversary tactics.
* **Entity Enrichment:** Transforming text strings into actionable 'Account' and 'Host' objects for investigative graphing.
* **Alert Aggregation:** Configuring logic to prevent duplicate incidents and streamline the triage process.

![](./grcac/mitre_analytics_rule.png)
> *Fig 27.3: Detection Metadata & Governance—Mapping the custom rule to MITRE ATT&CK Persistence (T1053). By defining Entity Mappings for 'Host' and 'Account,' I am enabling Defender to build a visual 'Attack Story' during the investigation phase, satisfying NIST 800-53 AU-12.*

***

### Triggering the "High-Risk" Incident
To validate the end-to-end efficacy of the NIST 800-53 SI-4 detection pipeline, I initiated a Live-Fire Trigger. By authenticating as the unauthorized 'backupadmin' account and executing privileged commands (sudo ls), I generated the specific behavioral markers required for incident generation. This step is the final proof of the Governance-as-Code model: the system didn't just 'log' the event; it 'recognized' the identity from the Watchlist and 'escalated' it to the SOC. This demonstrates the transition from passive log collection to Active Identity Defense.

<u>**Skills Applied**</u>
* **Incident Triggering:** Understanding how specific user actions (SSH login, sudo execution) generate detectable telemetry.
* **Detection Lifecycle Validation:** Confirming that the 'Watchlist -> Analytics Rule -> Incident' flow is functional.
* **Identity-Based Threat Hunting:** Moving beyond IP-based blocks to identity-based monitoring.

![](./grcac/)
> *Fig 28.1: Execution of the 'Insider' Attack—Logging in as the unauthorized 'backupadmin' account. This activity is designed to trigger the custom 'NYC-High-Risk-User-Activity-Detected' rule, providing a real-time test of our NIST 800-53 SI-4 monitoring controls.*

***

During the execution of the Phase 6 simulation, I encountered an Authentication Protocol Enforcement block. Despite enabling password authentication, the SSH daemon continued to default to Public Key exchange for the unauthorized 'backupadmin' account. To resolve this, I performed an Emergency Configuration Audit via the Azure Serial Console, enabling `KbdInteractiveAuthentication`. This technical hurdle highlights the complexity of NIST 800-53 IA-2 (Identification and Authentication), demonstrating that security engineers must understand the hierarchy of authentication protocols to successfully simulate—and ultimately defend against—credential-based attacks.

<u>**Skills Applied**</u>
* **SSH Protocol Debugging:** Identifying the difference between publickey and keyboard-interactive triggers.
* **System Hardening Reversal:** Intentionally modifying daemon configurations to test specific attack vectors.

![](./grcac/sshd_config_password_kbd.png)
> *Fig 28.0.5: Authentication Logic Modification—Enabling Keyboard-Interactive authentication to bypass the public key requirement for the 'backupadmin' simulation. This ensures the 'Insider Threat' can access the system via a compromised password, satisfying the requirements for a high-fidelity NIST 800-53 simulation.*

***

### Triage and The "Attack Story"
Following the successful execution of the 'Insider Threat' simulation, I transitioned to Incident Triage (NIST 800-53 IR-4) within the Microsoft Defender portal. The system successfully correlated the `backupadmin` activity against the High-Risk Watchlist, escalating the telemetry into a High-Severity incident. By utilizing the Attack Story visualization, I was able to map the relationship between the unauthorized user account and the target asset. This proves the efficacy of the Entity Mapping configured in Step 6, allowing for a rapid 'Blast Radius' assessment and moving the SOC from detection to active eviction.

<u>**Skills Applied**</u>
* **Incident Triage:** Moving a security event from 'New' to 'In Progress' with proper ownership.
* **Entity Relationship Mapping:** Visualizing how an attacker interacts with infrastructure.
* **Evidence Gathering:** Extracting specific commands from the Syslog alerts to build a timeline of the breach.

![](./grcac/backupadmin_incident.png)
> *Fig 29.1: Detection Efficacy—The 'High-Risk' incident triggered by the unauthorized 'backupadmin' login. This fulfills NIST 800-53 SI-4, demonstrating that the SIEM successfully identified a 'Low and Slow' threat using identity-based watchlist correlation.*

***

During the Incident Investigation (NIST 800-53 IR-4), I observed a clear distinction between Continuous Persistence (the `cron` heartbeat) and Point-in-Time Activity (the manual `sudo` login). The telemetry for the automated heartbeat was immediately available due to its high-frequency nature, whereas the manual discovery commands experienced standard ingestion latency. This delay is a critical 'Real-World' factor for SOC Analysts to understand; an attacker's actions may take several minutes to surface in the SIEM, requiring an analyst to remain patient and utilize Time-Windowing to capture the full scope of the breach.

<u>**Skills Applied**</u>
* **Log Ingestion Awareness:** Understanding the time-delay between an on-disk event and a cloud-based alert.
* **Forensic Patient Monitoring:** Staying within the investigation window until all telemetry has "settled."

![](./grcac/backupadmin_root_log.png)
> *Fig 29.2: Detailed Forensic Evidence—Extracting specific unauthorized commands from the Syslog. By linking the high-severity incident to the raw telemetry, I confirmed the adversary's attempt to access restricted directories, providing the necessary justification for immediate eviction under NIST 800-53 IR-4.*

***

### Eviction and Remediation (Closing the Loop)
To conclude the Phase 6 'Insider Threat' simulation, I initiated a Hardened Recovery of the NYC-Linux asset. Upon identifying the unauthorized `backupadmin` session and their attempt to access the `/root` directory (as evidenced in the Defender Alert telemetry), I executed an administrative eviction. This involved the removal of the unauthorized user account and the immediate decommissioning of the associated `cron` persistence mechanism. Finally, I remediated the intentional 'Configuration Drift' by reverting the SSH daemon to a Key-Only authentication model, satisfying NIST 800-53 IR-4 (Incident Handling) and CM-6 (Configuration Settings). This ensures the asset is returned to its baseline secure state.

<u>**Skills Applied**</u>
* **Adversary Eviction:** Using `deluser` and `crontab -r` to surgically remove a threat.
* **Baseline Restoration:** Reverting security-weakening changes (`sshd_config`) after a simulation.
* **Incident Documentation:** Closing the loop with technical evidence.

![](./grcac/deluser_backupadmin.png)
> *Fig 29.3: Threat Eviction & Recovery—Successfully removing the unauthorized 'backupadmin' account and associated persistence. By reverting SSH to an identity-file-only model, I have restored the NIST 800-53 CM-6 security baseline and finalized the NYC-Franchise-Prod recovery phase.*

***

### Phase 6 Conclusion: The "Insider Threat" Audit
Phase 6 served as the Stress Test for the NYC-Franchise-Prod environment. By simulating a compromised administrative account (`backupadmin`), I validated the efficacy of the Log Analytics Agent and the Microsoft Defender for Cloud unified detection engine. The core objective was to move beyond static perimeter defense and implement Behavioral Identity Monitoring.

<u>**Key outcomes included:**</u>

1. **Watchlist Integration:** Successfully mapped unauthorized entities to a high-priority monitoring list.
2. **Detection Efficacy:** Triggered a High-Severity incident within 5 minutes of unauthorized activity.
3. **Forensic Reconstruction:** Extracted specific TTY-level commands (ls /root) from raw Syslog telemetry to prove malicious intent.
4. **Incident Lifecycle Management:** Performed a full NIST 800-53 IR-4 recovery by evicting the user, removing persistence (cron), and re-hardening the SSH gateway to a Key-Only authentication baseline.

<u>**Skills Honed & Presented: **</u>

* **Detection Engineering:** Creating high-fidelity alerts that minimize false positives.
* **SIEM/SOAR Orchestration:** Using the Defender portal as a "Single Pane of Glass" for a Linux-based breach.
* **Cyber Kill Chain Interruption:** Specifically targeting the Persistence and Action on Objectives phases.

![](./grcac/incidents_resolved.png)
> *Fig 30.0: Incident Closure & Post-Mortem—Marking the unauthorized access incident as 'Resolved (True Positive).' All persistence mechanisms were neutralized, and the NIST 800-53 security baseline was successfully restored to the NYC-Linux-VM.*


