# GRC and Governance as Code

## Phase 5: The Incident Simulation (Attack & Defend)

### Introduction
In Phase 4, we proved the "Eyes" of our SOC were working by monitoring ourselves (the Emergency Admin). However, a robust NIST 800-53 framework requires more than just monitoring; it requires Red-Teaming and Control Validation (CA-7 - Continuous Monitoring).

Phase 5 transitions us from Passive Monitoring to Active Testing. We will simulate a real-world cyber attack against the NYC-Linux-VM to ensure our detection rules don't just work for "Expected Activity," but can catch a malicious actor attempting to compromise the franchise's production data.

### Phase 5 Roadmap: The "Kill Chain" Simulation
**Preparation:** Hardening our VM one last time and preparing the "Malicious Script."

**Execution:** Running an unauthorized Brute Force or Persistence script against the Linux VM.

**Detection:** Watching the "Live Stream" in Sentinel/Defender to see the alerts fire in real-time.

**Mitigation:** Using Automation Rules to lock down the attacker before they can exfiltrate NYC franchise data.

<u>**Applied Skill**</u>: Threat Hunting & Rule Fine-Tuning.

<u>**Tools Used**</u>
* **Kali Linux / PowerShell / Bash:** For executing the simulated attack.
* **Microsoft Sentinel Automation (SOAR):** To create automated responses.
* **Kusto Query Language (KQL):** For advanced "Hunting" during the attack.

***

### Setting the Trap (The Attack Simulation)
To validate the efficacy of the NIST 800-53 controls implemented in Phase 4, I initiated a Red-Team Simulation targeting the NYC-Linux-VM. By executing a series of failed SSH authentication attempts, I simulated a Brute Force Tactic (MITRE T1110). This phase transitions the project from static configuration to dynamic defense, ensuring that the SOC can detect and correlate high-velocity authentication failures that precede a potential system compromise.

<u>**Skills Applied**</u>
* **Attack Simulation:** Executing controlled "Red-Team" actions to test defense boundaries.
* **Threat Surface Analysis:** Identifying SSH (Port 22) as a primary vector for Linux-based environments.
* **Telemetry Latency Awareness:** Understanding the real-world time gap between an attack event and SIEM alerting.

![Bash script to simulate brute force attack](./grcac/brute_force_attack.png)
> *Fig 19.1: Attack Simulation—Executing a simulated SSH Brute Force attack against the NYC-Linux-VM. By intentionally generating 'Permission Denied' telemetry, I am testing the SIEM's ability to trigger high-severity alerts based on anomalous authentication patterns.*

***

### Tuning the Trigger (KQL Validation)
After executing the simulation, I observed a "Detection Gap": raw telemetry was successfully ingested into the Log Analytics Workspace, but no high-level Incident was generated in the Defender portal. To resolve this, I pivoted to Advanced Hunting to perform "Log Parsing." By analyzing the raw `sshd` process messages, I identified the specific string patterns (`Failed password`) necessary to transition from passive logging to active alerting. This step demonstrates NIST 800-53 SI-4 (Information System Monitoring) by ensuring that monitoring tools are tuned to specific indicators of compromise.

<u>**Skills Applied**</u>
* **Gap Analysis:** Identifying why a security control failed to trigger despite evidence in the logs.
* **Log Parsing:** Identifying the "ProcessName" and "Message" strings required for high-fidelity alerting.
* **Proactive Tuning:** Refining SIEM detection logic based on real-world simulation data.

![](./grcac/no_results_defender_log)
> *Fig 19.2: XDR Latency Analysis—Verifying that while raw '`sshd`' failure logs are present in the Log Analytics Workspace (LAW), the Defender Incident queue has not yet correlated the telemetry. This gap analysis is essential for NIST 800-53 SI-4, ensuring that analysts know how to 'Hunt' in the raw data when automated alerting lags.*

***

Upon executing the SSH Brute Force simulation, I observed a significant delay in the Microsoft Defender incident correlation engine. To ensure the integrity of the data collection pipeline, I pivoted from the XDR dashboard to the Log Analytics Workspace (LAW). To troubleshoot the lack of alerting in the Defender portal, I performed a Raw Telemetry Audit within the Log Analytics Workspace. By executing a direct KQL query against the raw `Syslog` table, I confirmed that the Azure Monitor Agent (AMA) was successfully capturing and transmitting the 'Failed password' telemetry from `vm-nyc-linux-01`. This manual verification confirms that our monitoring 'Trap' is physically set, even while the automated alerting engine is processing the high-volume data stream. This step is a critical component of NIST 800-53 AU-6 (Audit Review and Analysis), ensuring that the underlying data ingestion pipeline is healthy even if the high-level alerting engine is experiencing latency.

<u>**Skills Applied**</u>
* **Raw Data Validation:** Pivoting from high-level XDR dashboards to low-level log tables for troubleshooting.
* **Ingestion Path Analysis:** Verifying the "Heartbeat" of the Azure Monitor Agent (AMA) during a simulated stress test.
* **Network Security Group (NSG) Awareness:** Understanding how perimeter firewalls can "silent" an attack before it reaches the OS logging layer.

![](./grcac/syslog_failed_auth.png)
> *Fig 19.3: Raw Telemetry Verification—Confirming that 'vm-nyc-linux-01' is successfully transmitting SSH failure logs to the Log Analytics Workspace. This proves the data ingestion pipeline is functional, identifying the delay as a portal indexing issue rather than a collection failure, satisfying NIST 800-53 AU-12.*

***

### Creating the "NYC-SSH-Brute-Force" Trigger
To eliminate the "Detection Gap" identified in the previous step, I engineered a Custom Analytics Rule within Microsoft Sentinel. Using Kusto Query Language (KQL), I defined a threshold-based trigger that monitors for more than five failed SSH authentication attempts within a five-minute window. This rule utilizes Entity Mapping to automatically link the `Computer` data to a `Host` entity, ensuring that when the threshold is met, the system generates a high-fidelity incident rather than a silent log entry. This directly addresses NIST 800-53 SI-4, providing active defense against brute-force tactics.


