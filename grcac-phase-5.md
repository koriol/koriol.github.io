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

<u>**Skills Applied**</u>
* **Detection Engineering:** Creating custom logic to transform raw telemetry into actionable security alerts.
* **Threshold Optimization:** Setting specific "Noise vs. Signal" parameters (5 attempts / 5 minutes) to prevent alert fatigue.
* **SIEM Automation:** Configuring the automated transition from "Alert" to "Incident" within the XDR framework.

![](./grcac/rule_logic.png)
> *Fig 20.1: Detection Engineering—Configuring the 'NYC-SSH-Brute-Force' analytics rule. By defining a 5-attempt threshold and mapping the 'Computer' entity, I am ensuring that automated brute-force attacks are caught and escalated to the SOC immediately, fulfilling NIST 800-53 SI-4.*

***

### Triggering the Live Incident
With the custom NIST 800-53 SI-4 detection rule active, I initiated a high-velocity Brute Force simulation. By script-cycling 10 failed SSH authentication attempts, I deliberately crossed the "5 failures per 5 minutes" threshold defined in my detection logic. This step validates that the SIEM isn't just a passive repository for logs, but an active participant in the Incident Response (IR) lifecycle, capable of escalating raw telemetry into a high-severity investigation without human intervention.

<u>**Skills Applied**</u>
* **Validation Testing:** Confirming that custom security logic functions as designed under "live-fire" conditions.
* **Incident Lifecycle Management:** Observing the automated transition from raw data -> detection rule -> generated incident.
* **Threshold Verification:** Ensuring the "Signal-to-Noise" ratio is correctly tuned to catch real attacks while ignoring occasional human typos.

![](./grcac/permission_denied_loop.png)
> *Fig 21.1: Stress-Testing the Detection Logic—Executing 10 unauthorized SSH login attempts to cross the 5-event threshold of the 'NYC-SSH-Brute-Force' rule. This live-fire test is the final validation step for NIST 800-53 SI-4, ensuring the SOC is alerted to credential access attacks in real-time.*

***

### Investigative Triage & "Blast Radius" Check
With the automated detection logic successfully triggering an incident, I transitioned into the Triage and Investigation phase. By assigning the incident to my administrative account, I established accountability in accordance with NIST 800-53 AC-2. I utilized the Unified Attack Story to visualize the relationship between the brute-force alerts and the targeted `vm-nyc-linux-01` asset. The primary objective was to identify the source IP address of the attacker to determine the scope of the threat and prepare for immediate remediation via Network Security Group (NSG) modification.

<u>**Skills Applied**</u>
* **Incident Triage:** Moving a security event from "New" to "In Progress" with proper ownership.
* **Source Attribution:** Identifying the specific IP address or entity responsible for the unauthorized access attempt.
* **Contextual Analysis:** Using the Attack Story graph to verify that the threat has not spread laterally to other NYC-Franchise-Prod assets.

![](./grcac/incident_overview.png)
> *Fig 21.2: Incident Management—Initiating the response lifecycle by assigning ownership and acknowledging the alert. While the automated Entity Map has not yet populated the Attacker IP, this step ensures accountability and tracking under NIST 800-53 IR-4.*

***

### Hunting for the "Source IP"
During the triage of the brute-force incident, I encountered a common SOC challenge: Entity Obfuscation. While the high-level incident correctly identified the "Host" (`vm-nyc-linux-01`), the "Attacker Entity" (Source IP) required deeper forensic inspection. I pivoted from the Incident Dashboard to the Alert Evidence layer and utilized a KQL Parsing Query to extract the specific IP address hidden within the raw `SyslogMessage` string. This technical pivot ensures that my response is data-driven and satisfies NIST 800-53 AU-6, ensuring no critical audit data is overlooked due to UI limitations.

<u>**Skills Applied**</u>
* **Forensic String Parsing:** Using the `parse` operator in KQL to extract structured data (IPs) from unstructured text logs.
* **Deep-Dive Triage:** Navigating sub-alert layers to find actionable Indicators of Compromise (IOCs).
* **Data Extraction:** Converting raw telemetry into a "Blacklist-ready" IP address for remediation.

![](./grcac/kql_no_results.png)
> *Fig 21.3: Forensic Troubleshooting—Identifying a detection gap where standard 24-hour queries failed to return telemetry. This 'Cold Trail' scenario required a pivot to a wider temporal search window to account for log rotation and ingestion latency.*

During the follow-up investigation, I encountered a Data Discontinuity—the specific brute-force logs were no longer appearing in standard 24-hour queries. To maintain the Chain of Custody (NIST 800-53 AU-10), I expanded my forensic scope to 48 hours and utilized a "Wide Net" KQL search. This transition from specific process-matching (`sshd`) to general string-matching (`Failed`) is a critical SOC skill used when initial detection patterns fail to yield results due to log rotation or ingestion delays.

In this stage of the simulation, I performed a Network Topology Analysis to determine the origin of the brute-force attempts. Recognizing that the "Attacker" IP could vary based on the execution environment (Local Host vs. Cloud Shell), I utilized KQL to distinguish between Internal Loopback traffic and External Remote traffic. This distinction is vital for NIST 800-53 AC-4 (Information Flow Enforcement), as it ensures that remediation efforts (like IP blocking) target the external threat actor rather than inadvertently disrupting internal system processes.

<u>**Skills Applied**</u>
* **Network Attribution:** Differentiating between internal "System" traffic and external "Adversarial" traffic.
* **Infrastructure Analysis:** Understanding how Azure Cloud Shell environments interact with target VMs.
* **Surgical Remediation:** Ensuring the "Source IP" identified for blocking is the correct external entity.

![](./grcac/kql_failed_no_ip.png)
> *Fig 21.6: Forensic Data Recovery—Expanding the KQL look-back window to 48 hours to recover 'cold' incident telemetry. This wide-net approach ensures that even if logs were delayed or rotated, the Source IP can be recovered for final attribution and remediation, fulfilling NIST 800-53 AU-6..*

During the forensic investigation, I encountered Log Syntax Variation. Standard KQL filters for "Failed password" yielded no results, indicating that the target's Linux distribution utilizes non-standard strings for authentication failures. I pivoted to a Process-Level Audit of the `sshd` service to manually inspect the raw message telemetry. This approach allowed me to identify the specific rejection string used by the OS and extract the Source IP. This level of manual inspection is a key component of NIST 800-53 AU-6, ensuring that defensive measures are based on the actual technical output of the specific system component.

<u>**Skills Applied**</u>
* **Log Pattern Recognition:** Identifying OS-specific logging behavior that differs from standard documentation.
* **Service-Level Auditing:** Filtering telemetry by specific system processes (sshd) to isolate security events.
* **Forensic Flexibility:** Adapting search parameters when initial "known-bad" strings fail to appear.

![](./grcac/kql_live_attacks.png)
> *Fig 21.7: Log Syntax Identification—Analyzing the specific 'sshd' output for vm-nyc-linux-01. By identifying the unique rejection string used by this OS version, I was able to locate the attacker's metadata that was missed by generic 'failed password' filters, satisfying NIST 800-53 AU-12.*

Upon inspecting the `sshd` logs, I discovered that the NYC-Franchise-Prod infrastructure was being subjected to automated "Internet Background Noise"—constant, non-targeted brute-force attempts from global botnets. This presented a significant triage challenge: distinguishing my simulated "Red-Team" activity from actual malicious activity. To overcome the limitations of the Azure Portal's log display depth, I implemented a Temporal Forensic Filter. By defining a specific `datetime` range corresponding to the simulation window from the previous day, I successfully bypassed the "Internet Background Noise" generated by automated botnets today. 

By correlating the execution timestamps of my 'Red-Team' simulation with high-density log clusters in the Log Analytics Workspace, I was able to surgically isolate my specific source IP from a sea of global unauthorized actors. This method allowed me to bypass the 'Internet Background Noise'—automated botnets that frequently obfuscate targeted security events in high-volume environments. This level of precision is a critical requirement of NIST 800-53 AU-6, as it ensures that a SOC analyst can perform accurate historical incident reconstruction and identify specific indicators of interest amidst massive amounts of telemetry. Transitioning from this forensic identification to active mitigation allowed for a data-driven response, ensuring that the subsequent boundary protection measures targeted the verified adversary.

<u>**Skills Applied**</u>
* **Signal vs. Noise Discrimination:** Identifying specific forensic events within a high-volume, "noisy" log environment.
* **External Attribution:** Using local IP verification to confirm the "Attacker" identity in a multi-actor simulation.
* **Real-World Threat Awareness:** Recognizing the speed and frequency with which public cloud assets are scanned by automated threats.
  * **Temporal Query Scoping:** Using the `between` operator to isolate specific historical windows.
  * **Regex Extraction:** Utilizing the `extract` function in KQL to pull IP addresses directly from unstructured text strings.
  * **Volume Analysis:** Using `summarize` to identify the "Burst" characteristic of a targeted attack vs. a random scan.

![](./grcac/kql_ip_success.png)
> *Fig 21.9: Forensic Time-Windowing—Isolating the 10-attempt brute-force burst from the previous day. By scoping the query to a specific 'datetime' range and summarizing by count, I successfully separated my simulated attack from the surrounding 'Internet Noise,' providing a clear Target IP for remediation.*

<u>**Lessons Learned: IP Search**</u>
Upon the triggering of the SSH Brute Force incident, I initiated the triage process by assigning ownership and moving the status to 'In Progress,' establishing an audit trail in line with NIST 800-53 IR-4. Initial investigation through the Defender 'Attack Story' proved challenging; while the target asset was identified, the Source IP of the adversary was not automatically parsed into the entity map. I pivoted to KQL to perform a manual forensic extraction. However, my initial queries returned zero results. I hypothesized that this was due to Temporal Data Volatility—the ingestion delay between the raw Syslog and the Defender schema, compounded by a 12-hour gap in activity. To overcome this 'Cold Trail,' I expanded my search parameters to a 48-hour window and used string-matching to identify the specific rejection syntax used by the Linux OS. This retrospective analysis successfully unmasked the attacker, allowing for a transition from Triage to Remediation.

***

### The "Surgical Block" (Remediation)
After identifying the "Attacker" IP through a targeted temporal KQL query, I moved to the Mitigation Phase. Recognizing that the source of the brute-force attempts was an external entity (Azure Cloud Shell environment), I implemented an Access Control List (ACL) modification within the Network Security Group (NSG). By creating a high-priority "Deny" rule, I effectively blacklisted the malicious source. This action demonstrates a direct application of NIST 800-53 SC-7, shifting the infrastructure from a "Detected" state to a "Hardened" state by physically preventing further communication from the identified adversary.

![](./grcac/deny_rule.png)
> *Fig 22.1: Perimeter Hardening—Implementing a surgical IP block via the Network Security Group. By assigning a priority of 100 to this 'Deny' rule, I have neutralized the brute-force threat from the identified Source IP, fulfilling the Boundary Protection requirements of NIST 800-53 SC-7.*

In the final stages of the remediation phase, I encountered a Dynamic Addressing Challenge. Because the simulation used a cloud-native ephemeral terminal (Azure Cloud Shell), the source IP of the attacker was subject to change between sessions. To ensure the efficacy of the NIST 800-53 SC-7 boundary controls, I performed a real-time IP verification using the `curl ifconfig.me` utility. This allowed me to synchronize the Network Security Group (NSG) "Deny" rule with the current session's metadata. This highlights the importance of Dynamic Asset Tracking—security rules must be as agile as the threats they intend to block.

<u>**Skills Applied**</u>
* **Dynamic IP Attribution:** Identifying and adapting to ephemeral source addresses in a cloud environment.
* **Connectivity Verification:** Using curl and ssh to test the status of network-level security boundaries.
* **Agile Remediation:** Updating security controls in real-time to maintain a "Lockdown" state.

![](./grcac/deny_ip_fix.png)
> *Fig 22.2: Synchronizing the Perimeter Defense—Verifying the ephemeral Source IP of the Cloud Shell environment via '`curl ifconfig.me`.' By ensuring the NSG Deny rule precisely matches the current attacker metadata, I am enforcing a valid and active boundary control under NIST 800-53 SC-7.*

***

### Final Verification & "Closing the Loop"
To conclude the incident response lifecycle, I performed a Post-Remediation Validation. After synchronizing the Network Security Group (NSG) 'Deny' rule with the verified ephemeral Source IP of the adversary (verified via `curl ifconfig.me`), I attempted a final brute-force entry. The transition from 'Permission Denied' (OS-level rejection) to a 'Connection Timeout' (Network-level drop) confirms the efficacy of the NIST 800-53 SC-7 boundary control. By dropping the traffic at the perimeter, I reduced the processing load on the target VM and eliminated the attack vector entirely. I closed the incident in Microsoft Sentinel as a True Positive, completing the full cycle from detection and forensic triage to active mitigation and recovery.
*(Note: In a production enterprise environment, this would typically be handled via a Static VPN Gateway or Azure Bastion, rather than an ephemeral Cloud Shell IP)*

<u>**Skills Applied**</u>
* **Remediation Validation:** Using connectivity tests to confirm that security controls are functioning as intended.
* **Incident Documentation:** Closing the "Loop" in a SIEM by providing classification and resolution notes.
* **Control Efficacy:** Understanding the difference between application-level rejection and network-level dropping.

![](./grcac/resolved_incident.png)
> *Fig 22.3: Incident Resolution—Closing the 'NYC-SSH-Brute-Force' case as a True Positive. By documenting the remediation steps and the verification of the NSG block, I have fulfilled the requirements of NIST 800-53 IR-4 (Incident Handling) and IR-5 (Incident Monitoring). "Connection Timeout" is a Layer 4 (Transport) block, whereas "Permission Denied" was a Layer 7 (Application) response.*

Upon resolving the simulated brute-force incident, I observed a significant volume of 'Internet Background Noise'—over 200 automated unauthorized access attempts from various global botnets. Rather than performing a reactive, one-by-one IP block, I opted for a Proactive Zero-Trust Architecture. I modified the Network Security Group (NSG) to transition from an 'Allow-Any' ingress policy to a 'Strict Source-Validation' policy. By limiting SSH access exclusively to my authorized administrative IP (NIST 800-53 AC-3), I effectively neutralized the remaining 200+ threats simultaneously. This demonstrates a shift from Incident Response to Vulnerability Management, ensuring the NYC-Franchise-Prod environment remains resilient against automated mass-scanning. 

<u>**Skills Applied**</u>
* **Attack Surface Reduction:** Minimizing the "Target" area to only what is strictly necessary for operations.
* **Zero-Trust Implementation:** Moving toward an identity/IP-verified access model.
* **Strategic Remediation:** Choosing scalable security solutions over repetitive manual tasks.

![](./grcac/allow_ip_rule.png)
> *Fig 23.1: Strategic Surface Reduction—Transitioning to a 'Known-Good' IP whitelist. This proactive measure neutralized 200+ active botnet attacks simultaneously, moving the infrastructure toward a Zero-Trust model in compliance with NIST 800-53 AC-3.*

Following the successful mitigation of the targeted brute-force attack, I performed a broader Security Audit of the vm-nyc-linux-01 network profile. I identified an unnecessary Port 80 (HTTP) allowance which expanded the asset's attack surface without a functional requirement. Utilizing the principle of Least Privilege (NIST 800-53 AC-6), I decommissioned the HTTP rule and transitioned the SSH entry point to a 'Known-Good' IP whitelist. To conclude the lifecycle, I performed a Bulk Resolution of the 200+ background noise alerts, classifying them as 'Mitigated by Policy.' This final stage demonstrates the transition from reactive firefighting to proactive infrastructure hardening and dashboard hygiene.

![](./grcac/vm_complete_rules.png)
> *Fig 24.1: Final Infrastructure Hardening—Post-incident audit and remediation. By removing the unnecessary HTTP (Port 80) allowance and restricting SSH to a single administrative Source IP, I have enforced a 'Zero-Trust' ingress policy, satisfying NIST 800-53 AC-3 (Access Enforcement).*

![](./grcac/resolved_list.png)
> *Fig 24.2: Bulk Incident Resolution—Closing 200+ automated brute-force alerts. By implementing a structural change at the NSG layer, I neutralized the root cause of these alerts, allowing for a mass-resolution that restores the SOC dashboard to a manageable 'Clean' state.*

***

### Phase 5 Conclusion
The resolution of the NYC-SSH-Brute-Force incident transitioned from a narrow forensic investigation into a broad infrastructure hardening exercise. By utilizing KQL to bypass ingestion delays and identifying the unique 'Invalid User' syntax of the target OS, I successfully attributed the attack to a specific external IP. Following the implementation of a surgical 'Deny' rule (NIST 800-53 SC-7), I performed a secondary audit and decommissioned an unnecessary Port 80 (HTTP) allowance. This reduced the asset's attack surface by over 90% and allowed for the bulk resolution of 200+ automated background alerts. The incident concluded with a 'Clean Dashboard' state, moving the franchise from a reactive posture to a proactive, hardened security baseline.

<u>**Skills Applied**</u>
* **Full-Cycle Incident Handling:** Managing an alert from 'New' to 'Resolved.'
* **KQL Temporal Analysis:** Maneuvering through historical logs to find hidden data.
* **Network Surface Reduction:** Deleting unused protocols (HTTP) to minimize risk.
* **SIEM Hygiene:** Bulk-resolving noise to maintain "SOC Clarity."
