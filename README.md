# Immutable Backup Blueprints
### Surviving Identity Provider (IdP) Compromise.

> **Architecture Principle:** A backup is only valid if its restore path survives an Active Directory compromise.

## 📚 Canonical Architecture Reference  
This repository contains the blast-radius models and recovery sequence frameworks.

**The continuously maintained architectural specification lives here:** 👉 [https://www.rack2cloud.com/data-protection-architecture-strategy-guide/](https://www.rack2cloud.com/data-protection-architecture-strategy-guide/)

---

## What This Protects Against
If your primary Identity Provider (e.g., AD, Entra ID) is compromised, attackers will move laterally to your backup control plane. 

This model prevents:
* Backup policies being maliciously deleted.
* Immutable flags being modified via compromised admin accounts.
* Storage-level replication being poisoned.

## The Zero-Trust Vault Architecture
To guarantee recovery, the architecture must separate the data plane from the management plane.

| Component | Design Requirement |
| :--- | :--- |
| **Authentication** | Local vault accounts with physical MFA (YubiKey), completely decoupled from AD. |
| **Network** | Air-gapped or logically isolated via strict pull-only firewall rules. |
| **Storage** | Hardware-level immutability (WORM) that cannot be bypassed via the hypervisor. |

---
**Star this repo to secure your recovery paths.** *Maintained by [Rack2Cloud](https://www.rack2cloud.com)*
