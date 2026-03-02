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










