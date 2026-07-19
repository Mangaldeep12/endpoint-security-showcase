# ENDPOINT Security — Unified Endpoint Security Console

> A single pane of glass for endpoint protection, detection & response, data-loss prevention, identity security, cloud & AI-usage governance, compliance, and SOC operations — across Windows, macOS, and Linux.

![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-2b6cb0)
![Backend](https://img.shields.io/badge/backend-Go-00ADD8)
![Frontend](https://img.shields.io/badge/frontend-React%20%2B%20TypeScript-3178C6)
![UI](https://img.shields.io/badge/styling-Tailwind%20CSS-38BDF8)
![RBAC](https://img.shields.io/badge/access-granular%20RBAC-6b46c1)
![Status](https://img.shields.io/badge/status-active%20development-16a34a)

This repository is a **visual showcase** of the ENDPOINT Security platform — architecture, capabilities, and product screenshots. The full source lives in a **private repository** (see [Source code](#-source-code)).

---

## 🖥️ Overview

ENDPOINT Security unifies what usually takes five or six separate tools into one console: EDR, DLP, device & web control, vulnerability management, identity threat detection, privilege management, cloud & AI-usage governance, compliance automation, and a full SOC case-management workflow — all driven from a cross-platform lightweight agent.

![Overview dashboard](docs/screenshots/01-overview.png)

---

## ✨ Key capabilities

### Endpoints & detection
- **Asset inventory & health** across the fleet with live agent-component status.
- **EDR / threat detections** mapped to MITRE ATT&CK, with drill-in investigation drawers.
- **One-click response**: isolate, kill process, run script, scan, restart, and **remote assist** (remote desktop / terminal / file browser).
- **Vulnerability management** with EPSS + CISA KEV risk prioritization and firmware/UEFI posture.
- **Patch & software** deployment and compliance.

### Data protection & web control
- **DLP & insider-threat** monitoring with content inspection and incident workflow.
- **Source-code exfiltration** protection and secret detection.
- **Web & Firewall Control** — browser allow/block, category-based website blocking (adult, gambling, malware, phishing, anonymizers …) with a site library, plus **department-scoped browser & network firewall rules** and full browsing + file-access logs.

### Identity, privilege & deception
- **Identity Threat Detection & Response (ITDR)** with honeytokens and risky sign-in analytics.
- **Identity Security Posture** — over-privileged accounts, stale accounts, MFA gaps, service-account sprawl.
- **Endpoint Privilege Management** — remove standing admin, just-in-time elevation with approval flows.

### Cloud & AI security
- **Shadow AI & SaaS discovery** — govern which AI tools and SaaS apps are used, with prompt-level data-sharing controls.
- **Agentic-AI security** — inventory AI agents & MCP servers, block prompt-injection / data-exfil / tool-abuse.
- **Cloud & container workload protection** — misconfiguration findings, image scanning, posture scoring.
- **Attack-surface management** — external assets, exposed services, expiring certificates.

### Governance & operations
- **Continuous compliance** — SOC 2, ISO 27001, HIPAA, PCI DSS, CIS, GDPR, NIST CSF — with control mapping and evidence.
- **MITRE ATT&CK coverage** heat-mapping + **breach-&-attack simulation**.
- **Human risk management** — phishing simulation campaigns, per-user risk scoring, training.
- **Network Detection & Response (NDR)** and **SOC workflow** (cases, SLAs, threat hunts, escalations).
- **Automation & playbooks**, scheduled **reports**, and a full **audit log**.

### AI-assisted
- Built-in **AI Assistant** and **AI triage copilot** that analyze the live fleet posture and can run fully offline on a small local open-source model — no data leaves the host.

---

## 🔐 Granular role-based access control

Custom roles with a **per-page permission matrix** (no-access / view / manage) and capability flags — so, for example, a non-technical "User Manager" role can create console users without any other admin rights. The sidebar automatically hides pages a role cannot access.

![Role permission matrix](docs/screenshots/26-rbac-role-permissions.png)

---

## 📸 Screenshots

### Endpoint detail — inventory, response actions & remote assist
| Response actions, remote assist, hardware & security | Detections, patches, CVEs & software |
|---|---|
| ![Endpoint details](docs/screenshots/23-endpoint-details.png) | ![Endpoint deep detail](docs/screenshots/24-endpoint-remote-actions.png) |

### Threats & AI-assisted triage
| Threats / EDR + AI triage | AI Assistant |
|---|---|
| ![Threat AI triage](docs/screenshots/25-threat-ai-triage.png) | ![AI Assistant](docs/screenshots/07-ai-assistant.png) |

### Web & firewall control
| Web & Firewall Control | Department-wise firewall rule builder |
|---|---|
| ![Web & Firewall Control](docs/screenshots/04-web-firewall-control.png) | ![Firewall rule builder](docs/screenshots/27-firewall-new-rule.png) |

### Data protection, vulnerabilities & endpoints
| Data Protection / DLP | Vulnerabilities (EPSS/KEV + firmware) | Endpoints |
|---|---|---|
| ![Data Protection](docs/screenshots/05-data-protection.png) | ![Vulnerabilities](docs/screenshots/06-vulnerabilities.png) | ![Endpoints](docs/screenshots/02-endpoints.png) |

### Cloud & AI governance
| Shadow AI & SaaS | Agentic-AI Security | Cloud Workloads |
|---|---|---|
| ![Shadow AI](docs/screenshots/17-shadow-ai-saas.png) | ![AI Security](docs/screenshots/08-ai-security.png) | ![Cloud Workloads](docs/screenshots/14-cloud-workloads.png) |

### Governance & SOC operations
| Compliance | MITRE ATT&CK Coverage | SOC Workflow |
|---|---|---|
| ![Compliance](docs/screenshots/09-compliance.png) | ![ATT&CK Coverage](docs/screenshots/10-attack-coverage.png) | ![SOC Workflow](docs/screenshots/11-soc-workflow.png) |

### Identity, privilege & posture
| Identity & Deception | Identity Posture | Privilege Management |
|---|---|---|
| ![Identity & Deception](docs/screenshots/18-identity-deception.png) | ![Identity Posture](docs/screenshots/12-identity-posture.png) | ![Privilege](docs/screenshots/19-privilege.png) |

### More
| Network Detection (NDR) | Human Risk | Attack Surface |
|---|---|---|
| ![NDR](docs/screenshots/13-ndr.png) | ![Human Risk](docs/screenshots/15-human-risk.png) | ![Attack Surface](docs/screenshots/16-attack-surface.png) |

| Device Experience | Departments | Roles & settings |
|---|---|---|
| ![Device Experience](docs/screenshots/20-device-experience.png) | ![Departments](docs/screenshots/21-departments.png) | ![Settings](docs/screenshots/22-settings-roles.png) |

> A full-resolution set of all screens is in [`docs/screenshots/`](docs/screenshots).

---

## 🏗️ Architecture

```
                ┌──────────────────────────┐
                │   Web console (SPA)       │   React + TypeScript + Tailwind
                │   role-aware, dark/light  │
                └────────────┬─────────────┘
                             │  HTTPS / session
                ┌────────────┴─────────────┐
                │   Console backend (Go)    │   REST API, RBAC, audit,
                │   single self-contained   │   optional local AI (Ollama)
                │   binary                  │
                └────────────┬─────────────┘
                             │  mTLS ingest (heartbeat / telemetry)
                ┌────────────┴─────────────┐
                │   Endpoint agent (Go)     │   Windows · macOS · Linux
                │   watchdog-protected      │   OS-native enforcement
                └──────────────────────────┘
```

**Tech stack**
- **Agent & console:** Go — a single self-contained console binary embeds the dashboard; a lightweight cross-platform agent handles collection and OS-native enforcement.
- **Web UI:** React + TypeScript + Vite + Tailwind CSS.
- **AI (optional):** a small open-source model served locally via Ollama powers the AI Assistant and detection triage, with a deterministic offline fallback — no data leaves the host.
- **Design goal:** OS-native, already-signed enforcement (BitLocker, WDAC, Defender Device Control, USBGuard, MDM) wherever it exists — custom code only for the gaps.

---

## 📦 Source code

The complete application source (agent, console backend, and web UI) is maintained in a **private repository**:

**➡️ https://github.com/Mangaldeep12/endpoint-security** *(private — access available on request)*

This public repository intentionally contains **no source code** — only documentation and screenshots for showcase purposes.

---

## 👤 Author

**Mangaldeep Barai**
mangaldeepbarai2001@gmail.com

---

*ENDPOINT Security is an actively developed product. Screenshots depict seeded demonstration data.*
