





### Introduction
In this project, we are building a "Middleware" or a mini-SOAR. Raw logs tell you what happened, but Threat Intelligence tells you who is doing it and how much you should care. By the end of this, you’ll have a script that turns a messy text file of IP addresses into a structured, prioritized risk report. Analysts shouldn't waste time manually copy-pasting IPs into browser tabs. Automation reduces "Mean Time to Respond" (MTTR).
**Goal:** Automate the "Triage" phase of incident response by programmatically querying global threat databases.

<u>**Skills & Tools**</u>
* Python (Requests, JSON, Pandas), AbuseIPDB API.
* API Integration, Data Parsing, Incident Classification, and Defensive Automation.

#### Environment Orchestration & Data Preparation
Before we can automate intelligence, we need to ensure our environment has the right "connectors" (libraries) and that our Project 2 script is feeding data into a format Project 3 can understand. We are "setting the stage" by linking your Linux logs to your Python environment.

![](./Auth_log/triage_scan.png)
> *Execution of the Triage Script: The Python logic iterates through extracted logs and fetches real-time reputation data from AbuseIPDB.*

![](./Auth_log/incident_report.png)
> *Automated Incident Report: A structured JSON output used to feed downstream security tools or alert a human analyst.*

![](./Auth_log/triage_risk.png)
> *High-Risk Classification: Demonstrating the script's ability to flag IPs with an Abuse Confidence Score > 75% for immediate containment*

<u>**Skills & Tools**</u>
* **API Orchestration:** Learning to bridge two different systems (Linux Logs and External Threat Intel).
* **Structured Data Handling:** Converting unstructured text logs into actionable JSON intelligence.
* **Defensive Automation:** Implementing programmatic logic to reduce alert fatigue.
* **NIST 800-61 Alignment:** Maps directly to the Detection & Analysis phase.
  * Analysis: "Automating the process of identifying whether an event is a legitimate security incident or a false positive."

***

### Setting the Stage: The Infrastructure
We are transitioning from Active Defense to Intelligence Enrichment. We are setting up the environment to handle external data and preparing the "connectors" that allow Python to talk to the internet.

![](./Auth_log/)
> *Environment Provisioning: Installing the necessary Python dependencies and establishing a modular configuration for secure API key management.*

<u>**Skills & Tools**</u>
* **Python Pip:** Managing third-party libraries—a fundamental skill for any security automation engineer.
* **Secure Secret Management:** Moving API keys into a config file rather than hardcoding them (essential for DevSecOps).
* **Dependency Management:** Ensuring the Linux environment is properly provisioned to support the automation script.
* **AbuseIPDB API:** Utilizing third-party threat intelligence to enrich internal security data.

#### Dependency Isolation & Triage Logic
In this step, I addressed modern Linux security constraints by implementing a Python Virtual Environment (venv). This ensures that the SOAR tool's dependencies remain isolated from the core operating system. I then developed the core logic to bridge the gap between my Watchdog logs and global threat intelligence, automating the decision-making process for incident classification.

![](./Auth_log/)
> *Environment Isolation and Script Execution: Utilizing a Python Virtual Environment to securely manage dependencies while executing the automated triage logic.*

<u>**Skills & Tools**</u>
* **Python Virtual Environments (venv):** Essential for managing complex software dependencies without compromising system stability.
* **Error Resolution (PEP 668):** Demonstrated the ability to troubleshoot and bypass "Externally Managed Environment" errors using industry-standard practices.
* **Automated Incident Categorization:** Writing conditional logic to label threats (CRITICAL vs. CLEAN) based on third-party confidence scores.
* **Regex (Regular Expressions):** Used to parse unstructured log data from Project 2 to find specific indicators of compromise (IP addresses).

![](./Auth_log/)
> *Environment Isolation and Script Execution: Utilizing a Python Virtual Environment to securely manage dependencies while executing the automated triage logic.*

### Adversary Emulation & Validation
In a production environment, automation must be tested against diverse data sets. To validate the SOAR tool's logic, I performed Adversary Emulation by injecting "Known Bad" indicators into the log pipeline. By simulating brute-force attempts from real-world malicious IPs (sourced from active botnets), I ensured the script could accurately differentiate between high-risk threats and legitimate traffic. This allowed me to test the script’s ability to differentiate between legitimate traffic and high-risk botnets in a controlled environment.

![](./Auth_log/)
> *Synthetic Intelligence Injection: Emulating multi-vector attacks from known malicious IPs to validate the SOAR tool's scoring and categorization logic.*



This section documents the pivot from raw detection to automated intelligence. Building this "SOAR-lite" tool required navigating several real-world technical hurdles that are common in enterprise security environments.

![](./Auth_log/)
> *Final Incident Output: The SOAR script successfully parsed the 'Security_Alerts.log' and enriched the data with real-time threat intelligence, providing clear risk classifications for an analyst to review.*


### Lessons Learned
API Rate Limiting: While using a free tier API, I learned the importance of error handling for "429 Too Many Requests" errors and implemented logic to handle empty or failed responses gracefully.

Shell Neutrality: Encountered shell-specific errors when activating the virtual environment. I resolved this by using POSIX-compliant syntax (. venv/bin/activate), ensuring the script's portability across different Linux distributions.

Context is King: A blocked IP is good, but knowing why it was blocked (e.g., it's a known Russian botnet vs. a misconfigured internal server) is the difference between reactive and proactive security.
















