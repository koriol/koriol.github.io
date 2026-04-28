# Securing the Modern Stack
## Phase 1: Infrastructure & Vulnerable Deployment
Goal: Establish a local Kubernetes cluster and deploy a "Patient Zero" application that is intentionally vulnerable to demonstrate why Zero Trust "Assume Breach" is necessary.

## 🛠️ Environment Bootstrapping

To ensure consistent results and alignment with the NIST SP 800-190 standards for container isolation, we utilize a standardized local development environment.

### Automated Setup (Native Linux)
If `minikube` is not present on your path, execute the following to align your workstation with the lab requirements:

```
# Fetch and install the Minikube binary
curl --location --remote-name https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64

# Initialize the Control Plane
# We use the Docker driver to simulate a node-level shared kernel environment
minikube start --driver=docker
```

> *We explicitly use the `--driver=docker` flag. In a Zero Trust model, we must account for Kernel Isolation. Since containers share the host kernel, our subsequent security policies (Phase 4 & 5) are critical to prevent "breakouts" where one compromised container affects the host.*
