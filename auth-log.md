# The Linux 'Auth-Log' Watchdog (Python)

## Introduction
In a modern enterprise, security is not just about perimeter defense; it is about continuous visibility. As a SOC analyst, manually monitoring logs for every server is impossible. This project was born from the need to automate the detection of one of the most common attack vectors: Brute Force SSH attacks.

The goal of this project is to build a proactive monitoring tool that acts as a first line of defense. By parsing system logs in real-time, this "Watchdog" script identifies suspicious patterns that would otherwise be lost in the "noise" of thousands of system events. This project demonstrates the transition from a passive security posture to an active, automated defense strategy.

**Purpose:**
* **Real-Time Incident Response:** Detection must happen in seconds, not hours. This tool alerts the analyst the moment a threshold is crossed.
* **Resource Efficiency:** Automation allows SOC teams to focus on high-level investigations rather than manual log filtering.
* **Compliance Readiness:** Continuous monitoring is a core requirement for major frameworks (NIST, SOC2, ISO 27001).

### Skills and Tools
The following are the main skills and tools implemented throughout the project
| Category | Skills & Tools |
| --- | --- |
| Programming | Python 3: Core logic, file handling, and real-time streaming (tail logic). |
| Data Extraction | Regular Expressions (RegEx): Pattern matching to extract specific IP addresses from unstructured log data. |
| System Admin | Linux Log Management: Navigating /var/log/auth.log, managing file permissions, and understanding system events. |
| SOC Operations | Detection Engineering: Creating threshold-based alerts and log normalization. |
| GRC / Compliance | NIST 800-53 Mapping: Specifically addressing SI-4 (Information System Monitoring) and AU-6 (Audit Record Review, Analysis, and Reporting). |

### Roadmap
1. Environment Hardening: Configure a Linux VM (Ubuntu/Debian) and secure permissions to allow the script to read sensitive system logs without compromising root security.
2. Logic Development: Write the Python "Watchdog" using the re module for pattern matching and time.sleep for continuous file polling.
3. Threshold Implementation: Develop a counter system to track failed login attempts per IP address and trigger an alert once a "Brute Force" pattern (5+ attempts) is detected.
4. Security Alerting: Program the script to output human-readable alerts to the console and persist them in a dedicated Security_Alerts.log for audit trails.
5. Attack Simulation: Execute a controlled Brute Force attack from a secondary source to validate that the script accurately identifies and logs the threat.
6. Portfolio Documentation: Log the success criteria and evidence of detection for GRC audit simulation.

***

### Environment Preparation & Permission Hardening
In a production SOC environment, you never run security tools as root unless absolutely necessary. This is the principle of Least Privilege. We need to give our Python script enough permission to read the system authentication logs (`/var/log/auth.log`) without giving it the power to modify system files. We will create a dedicated workspace and ensure our user is part of the `adm` (administration) group, which traditionally has read access to logs.

<u>**Skills Applied**</u>
* **Linux Privilege Management:** Understanding group-based permissions is vital for system hardening.
* **Access Control (IAM):** Implementing the Principle of Least Privilege (PoLP) to reduce the attack surface of your own security tools.

![](./Auth_log/ls_l_mkdir.png)
> *Figure 1: Configuring Least Privilege access. I verified that /var/log/auth.log is readable by the `adm` group and added my user to that group to ensure the script can parse logs without requiring root/sudo execution, adhering to NIST 800-53 access control principles.*

### Drafting the Python Watchdog Logic
Now that we have permissions, we need the "brain" of the operation. We are using Regular Expressions (RegEx) because log files are messy. We need to tell Python: "Ignore everything in this file UNLESS you see the specific phrase 'Failed password' followed by an IP address."

We also need to implement a stateful counter. The script needs to remember how many times a specific IP has failed so it can decide when a "random typo" becomes a "Brute Force Attack."

<u>**Skills Applied**</u>
* **Scripting for Automation:** Transitioning from manual log review to automated "tailing" of system files.
* **Detection Engineering (Tuning):** Setting a THRESHOLD variable is a real-world example of tuning a detection rule to balance between security and "false positive" noise.

![](./Auth_log/watchdog_script.png)
> *Figure 2: Python script implementation utilizing the re (Regular Expression) library for log parsing and a dictionary-based counter to track stateful login failures per unique IP address.*

### The Attack Simulation (The "Fun" Part)
A detection script is useless if it hasn't been tested against a live "threat." Since we are targeting the `auth.log`, we need to generate SSH failures.

We will use a Looping Bash Script to simulate a "Brute Force" attack. This mimics an automated botnet trying to guess passwords. By doing this, we verify that our RegEx is correctly catching the IP and that our counter is incrementing as expected.

#### Debugging & Signature Refinement
During the initial simulation, the script remained silent despite the attacker terminal showing "Permission denied." This indicated a Detection Gap. To solve this, I adopted a SOC Analyst's troubleshooting workflow:
1. Verify the Source: Used tail to inspect the raw log format.
2. Hypothesize: Identified that the system logged "Invalid user" rather than the expected "Failed password" string.
3. Test & Iterate: Broadened the RegEx signature and implemented a "Force Read" debug mode to isolate whether the issue was the Code or Permissions.

I modified the script to include a DEBUG READ statement that prints every line the script processes.

To rule out OS-level restrictions, I executed the script using sudo.
![](./Auth_log/sudo_debug.png)
> *Implementing Verbose Debugging: By adding a 'Force Read' print statement and escalating privileges with `sudo`, I confirmed the script could successfully hook into the `/var/log/auth.log` stream.*

I re-ran the attack loop and successfully captured the raw data stream.
![](./Auth_log/debug_results.png)
> *Successful detection after signature tuning. The output confirms the script is now accurately parsing authentication failures and identifying the source IP.*

After refining the signatures and validating the permission requirements, the script was returned to its production state (removing the verbose debug prints). A final simulation was conducted to ensure the alerting logic was functional and persistent.

<u>**Skills Applied**</u>
* **Incident Validation:** Proving that security controls work as intended through active testing (essential for GRC auditing).
* **Audit Trail Integrity:** Ensuring security events are recorded in a way that is useful for later forensic analysis.

### Outcomes
To ensure the project met the standards of a professional SOC tool, I verified the following:

Accuracy: The script's detection count was cross-referenced with sudo grep "Invalid user" /var/log/auth.log | wc -l, showing a 100% match.

Low Latency: The script processed log entries in real-time with less than 1 second of delay between the attack and the alert.

Zero False Positives: Successful logins did not trigger the counter, ensuring that only unauthorized attempts were flagged.

### GRC Mapping: NIST 800-53 Implementation
By developing this tool, I have implemented technical controls that map directly to federal and enterprise security standards:
| Control ID | Control Name | Implementation in Project |
| --- | --- | --- |
| SI-4 | Information System Monitoring | The Python watchdog provides host-based monitoring to detect indicators of potential attacks (Brute Force). |
| AU-12 | Audit Record Generation | The script generates a specialized Security_Alerts.log specifically for authentication failures. |
| AU-6 | Audit Record Review | Automated the analysis of raw system logs to find actionable security events, satisfying the requirement for regular audit review. |
| SI-4(24) | Indicators of Compromise | Using identified patterns to trigger automated responses. |
| SC-7 | Boundary Protection | Dynamically updating firewall rules to protect the internal host from external threats. |

### Lessons Learned
This project highlighted the importance of Signature Tuning. Initially, the script suffered from a False Negative because the RegEx was too specific. By analyzing the raw log data and broadening the search pattern, I improved the detection rate. Furthermore, I learned that even with proper group permissions, certain Linux environments require specific process-level privileges to maintain a continuous file stream from /var/log/auth.log.

### The "Bonus" Phase: Incident Response & Geolocation
Detecting 1,000 failed attempts is good; stopping the 1,001st attempt automatically is better. We will use Python’s `os.system` or `subprocess` module to interact with the UFW (Uncomplicated Firewall), which is standard on Ubuntu/Debian. When the threshold is hit, the script will issue a command to block that IP address entirely.

![](./Auth_log/)
> *Transitioning to an Intrusion Prevention System (IPS). The script automatically invokes a firewall rule to drop all future packets from the offending IP address.*

![](./Auth_log/)
> *Verification of Active Defense. The UFW status table confirms the malicious IP has been blacklisted dynamically by the Python Watchdog.*

<u>**Skills Applied**</u>
* **Active Defense (IPS):** Demonstrates the ability to not just watch a fire, but put it out.
* **Firewall Management:** Practical experience with host-based firewalls (UFW/iptables).
* **Security Orchestration:** Combining custom Python logic with native OS security tools (Orchestration/Automation).

## Lessons Learned: The Final Reflection
This is the most important part of your portfolio for a GRC or SOC Manager. It shows you can think critically about your own work.

1. The Challenge of "Silent Failures"
* **The Problem:** Initial tests resulted in no detections because the script was looking for "Failed password" while the system was logging "Invalid user."
* **The Lesson:** Security tools must be "tuned" to the specific environment. A one-size-fits-all signature often leads to False Negatives.

2. The Permission Bottleneck
* **The Problem:** The script required sudo to read /var/log/auth.log and modify ufw.
* **The Lesson:** While sudo solved the issue, in a production environment, I would look into Linux Capabilities or specific ACLs (Access Control Lists) to follow the Principle of Least Privilege (PoLP) more strictly.

3. From Monitoring to Mitigation
* **The Problem:** Detecting an attack manually is too slow for modern botnets.
* **The Lesson:** Automation (IPS) is a force multiplier. By linking Python to the system firewall, the Mean Time to Remediate (MTTR) was reduced to nearly zero.

4. NIST 800-53 Mapping Reflection
This project moved beyond simple coding into Compliance Orchestration. By meeting SI-4 (Monitoring) and SC-7 (Boundary Protection), I demonstrated how a simple script can fulfill complex federal security requirements.



























