# Securing the Modern Stack
The lab's progression follows a logical DevSecOps pipeline: you will intentionally deploy a vulnerable component to simulate a compromised environment, use AI to accelerate the decision-making process for remediation, and finally implement automated gatekeeping to prevent future risks.

## Roadmap
1. [Setup](./devsecops1.md) - Environment bootstrapping and prerequisite verification.
2. [Infiltration](./devsecops2.md) - Deploying the "Sacrificial App" and understanding the attack surface.
3. [AI Triage](./devsecops3.md) - Automated scanning and AI-assisted risk prioritization.
4. [Hardening](./devsecops4.md) - Applying Zero Trust controls to the active "breach."
5. [Governance](./devsecops5.md) - Implementing proactive guardrails and admission control.

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
