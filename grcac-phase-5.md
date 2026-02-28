# GRC and Governance as Code

## Phase 5: The Incident Simulation (Attack & Defend)

### Introduction
In Phase 4, we proved the "Eyes" of our SOC were working by monitoring ourselves (the Emergency Admin). However, a robust NIST 800-53 framework requires more than just monitoring; it requires Red-Teaming and Control Validation (CA-7 - Continuous Monitoring).

Phase 5 transitions us from Passive Monitoring to Active Testing. We will simulate a real-world cyber attack against the NYC-Linux-VM to ensure our detection rules don't just work for "Expected Activity," but can catch a malicious actor attempting to compromise the franchise's production data.

### Phase 5 Roadmap: The "Kill Chain" Simulation
Preparation: Hardening our VM one last time and preparing the "Malicious Script."

Execution: Running an unauthorized Brute Force or Persistence script against the Linux VM.

Detection: Watching the "Live Stream" in Sentinel/Defender to see the alerts fire in real-time.

Mitigation: Using Automation Rules to lock down the attacker before they can exfiltrate NYC franchise data.

<u>**Applied Skill**</u>: Threat Hunting & Rule Fine-Tuning.

<u>**Tools Used**</u>
* **Kali Linux / PowerShell / Bash: For executing the simulated attack.
* **Microsoft Sentinel Automation (SOAR):** To create automated responses.
* **Kusto Query Language (KQL):** For advanced "Hunting" during the attack.
