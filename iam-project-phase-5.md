Phase 5: Defensive Operations (The "Test & Audit")
The Task: Launch a Phishing Simulation against Maria Curie.

The Incident: Maria "fails" the test. We show her account being flagged as "High Risk" in Entra Identity Protection.

The Remediation: We show how your policies automatically force her to do a Self-Service Password Reset (SSPR) to "cleanse" her risk.

The Grand Finale: A quick look at Microsoft Sentinel (SIEM) to show all these logs in one place.

![](./assets/)
> *Fig 5.1: Web Service Deployment—Successfully initialized the Nginx HTTP server on the NYC-Franchise-01 instance. The transition from a 'blank' hardened server to a functional web host is confirmed via successful HTTP response over the public internet.*

![Inbound port rule](./assets/inbound_port_rule.png)
> *Fig 5.2: Inbound Traffic Regulation—Configuring the Network Security Group (NSG) to permit HTTP traffic on Port 80. This demonstrates the principle of least privilege by only opening specific ports required for the application's role as a web server.*

![](./assets/vm_nginx_valid.png)
> *Fig 5.3: Service Availability Validation—Confirmed Nginx is listening on localhost (Port 80) and UFW rules are correctly applied. Analyzing the 'split-horizon' connectivity to ensure Azure fabric rules align with internal OS security policies.*

![](./assets/loopback_valid.png)
> *Fig 5.7: Loopback Interface Validation—Internal HTTP request to the public-facing IP returns a 200 OK status. This confirms the Nginx service is correctly bound to the public interface and identifies external network interference (ISP/Hotel Firewall) as the primary bottleneck for client-side rendering.*

![](./assets/
> *Fig 5.8: Localhost Service Audit—Attempting a verbose curl against the local loopback interface. Connection refusal indicates the service is failing to bind despite the systemd status showing 'active.' Proceeding to configuration syntax validation.*

![](./assets/nginx_t_results.png)
> *Fig 5.9: Nginx Configuration Synthetic Testing—Validating configuration file syntax and existence of required directories. Confirming the web server is ready to bind to the network stack.*

![](./assets/)
> *Fig 5.10: Correcting NSG Port Mapping—Adjusting the source port range to wildcard to accommodate ephemeral ports from client browsers. This ensures that while the destination is locked to Port 80, the incoming request's origin port is not restricted, allowing for a successful TCP handshake.*

![](./assets/server_success.png)
> *Fig 5.11: Successful Public Web Service Deployment—Resolved connectivity issues by correcting the NSG Source Port range to wildcard. This allowed for the successful reception of HTTP requests from ephemeral client ports, as evidenced by the external rendering of the Nginx landing page.*

![](./assets/server_log.png)
> *Fig 5.13: Audit Trail—A chronological record of the system configuration, troubleshooting steps, and final deployment commands. This serves as a primary audit log for the build process.*

| **Security Layer** | **Technical Implementation** | **"Why It Matters"** |
| --- | --- | --- |
| Network Security,Stateful Firewall (NSG) | By fixing that Source Port to * and locking the Destination to 80, managed precise traffic flow and prevented unauthorized port access. |
| Host Hardening | UFW (Uncomplicated Firewall) | I implemented a "Secondary Gate." If the Azure NSG ever failed or was misconfigured, the internal Linux firewall would still protect the server. |
| Access Control | SSH Key Authentication | Moved away from vulnerable passwords to cryptographic keys, making "Brute Force" attacks nearly impossible. |
| Identity Management | Root Escalation Control | Practiced using sudo and managing root privileges, ensuring that everyday tasks aren't performed with "God Mode" enabled by default. |
| Service Security | Nginx Optimization | Successfully moved a service from a "Default" insecure state to a "Production" state with custom content and verified socket bindings. |
