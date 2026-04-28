# Securing the Modern Stack
## Project Overview
This hands-on cybersecurity lab provides a comprehensive roadmap for securing cloud-native environments by integrating Zero Trust Architecture (ZTA), the CISA Known Exploited Vulnerabilities (KEV) catalog, and Generative AI. Grounded in NIST SP 800-207 and NIST SP 800-190, this lab moves beyond static perimeter defenses to focus on granular resource protection, continuous authentication, and automated threat triage.  

The goal is to build a resilient system that "Assumes Breach" by isolating workloads via Kubernetes Network Policies and enforcing "Least Privilege" through Admission Controllers that block vulnerable images before they ever reach production.

## Roadmap
1. [Infrastructure & Vulnerable Deployment](./devsecops1.md) - Establish a secure local Kubernetes foundation and deploy a deliberately vulnerable "Patient Zero" application.
2. [KEV-Aware Vulnerability Scanning](./devsecops2.md) - Transition from generic vulnerability scanning to high-priority KEV-based intelligence.
3. [AI-Powered Risk Triage](./devsecops3.md) - Automate security analysis using Gemini AI to reduce "alert fatigue."
4. [Zero Trust Network Isolation](./devsecops4.md) - Implement micro-segmentation to prevent lateral movement.
5. [Admission Control & Enforcement](./devsecops5.md) - Shift security "Left" by preventing insecure deployments at the API level.

## Skills Used
* **Kubernetes Orchestration:** Managing pods, namespaces, and services.
* **Container Security:** Image scanning and vulnerability lifecycle management.
* **Policy as Code (PaC):** Writing declarative security rules for the cluster.
* **AI Integration:** Prompt engineering for security telemetry analysis.
* **Zero Trust Architecture (ZTA):** Applying NIST 800-207 principles to cloud-native workloads.

## Tools Implemented
* **Orchestration:** Minikube (local Kubernetes), kubectl.
* **Runtime:** Docker or containerd.
* **Scanner:** Trivy.
* **AI Engine:** Google Gemini API (via Python SDK).
* **Editor:** nvim (NeoVim).
