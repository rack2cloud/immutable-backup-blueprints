# Immutable Backup Blueprints
### Authority-Separated Recovery Architecture

![Status](https://img.shields.io/badge/status-architecture--pattern-blue)

> **Architecture Principle:** Immutability without authority separation is not resilience. A backup is only valid if its restore path survives an Active Directory compromise.

---

## 📚 Canonical Architecture Reference  
This repository contains the blast-radius models and recovery sequence frameworks for defending against identity plane compromises.

**The continuously maintained architectural specification lives here:** 👉 [https://www.rack2cloud.com/data-protection-architecture-strategy-guide/](https://www.rack2cloud.com/data-protection-architecture-strategy-guide/)

---

## Problem Statement

Most backup systems rely on production identity systems (e.g., Active Directory, Entra ID) for restore authorization. This creates a fatal circular dependency during compromise events. 

If your primary Identity Provider (IdP) is compromised, attackers will move laterally to your backup control plane to maliciously delete policies, poison replication, or bypass immutable flags using stolen privileged accounts.

---

## System Model

![Authority Separation Model](https://www.rack2cloud.com/wp-content/uploads/2026/02/diagram-authority-separation.jpg)

**Components:**
1. Production Domain (Compromised Zone)
2. Backup Storage Plane (Zero-Trust Data Plane)
3. Independent Recovery Authority (Isolated Control Plane)
4. Offline Credential Chain (Break-Glass Access)

---

## Threat & Mitigation Model

| Threat | Mitigation Strategy |
| :--- | :--- |
| **Ransomware / Wiper** | Hardware-level immutability (WORM) that cannot be bypassed via the hypervisor. |
| **Privilege Escalation** | Independent restore auth (Local vault accounts with physical MFA, decoupled from AD). |
| **Policy Deletion** | Out-of-band metadata and vault locking to prevent retention policy drift. |
| **Replication Poisoning** | Authority isolation and logically air-gapped pull-only firewall rules. |

---

## Zero-Trust Architectural Requirements

To guarantee recovery, the architecture must separate the data plane from the management plane:
1. **Separate Identity Plane:** Backup administration accounts must reside in a dedicated, isolated domain or utilize local physical tokens (YubiKey).
2. **Immutable Retention Enforcement:** Object-level retention policies must prevent deletion during defined windows, regardless of administrative intent.
3. **Offline Recovery Path:** The ability to recover must not depend on the availability of production DNS, DHCP, or IdP services.

---

## Non-Goals

- Vendor feature comparison
- Storage benchmarking

*This is a control-plane architecture model focused strictly on authority separation.*

---

## Support

If this framework helped secure your recovery paths, please star the repository. 

Architectural frameworks maintained by **[Rack2Cloud](https://www.rack2cloud.com)**.
