Phase 4: Infrastructure Hardening (The "Fortress")
The Task: Deploy a Linux VM (Ubuntu) in Azure.

The Security: Disable passwords. Enable Microsoft Entra ID Login for Linux.

The Governance: Apply a Conditional Access Policy that says: "To log into this specific server, you MUST be a member of 'NYC-Admins' and have an Active PIM session."

The "Wow" Factor: Using Azure Bastion (no public IP address) and Just-In-Time (JIT) VM Access.
