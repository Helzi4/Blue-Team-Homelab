# Blue Team Homelab (SOC / DFIR)
Enterprise-like homelab for SOC Analyst practice and a public case portfolio

## What this repo is
This repository documents a blue-team focused lab and a set of repeatable incident-style cases.
Each case follows the same workflow:
attack simulation (safe) -> detection -> triage -> investigation -> remediation -> rollback

No external exposure of lab services. Access is only internal or via VPN.

## Lab snapshot
| Area | Component | Purpose |
| --- | --- | --- |
| Hypervisor | Proxmox | Virtualization and snapshots for repeatable cases |
| Network edge | FortiGate 40F | VLAN segmentation, policy enforcement, traffic logging, SSL-VPN |
| Identity | Windows Server 2022 DC01 (arata.lab) | AD DS, DNS, GPO, LDAPS, certificate services |
| SIEM | Wazuh | Log collection, correlation, dashboards |
| DFIR | Velociraptor | Live response, hunts, artifact-based collections |
| EDR | LimaCharlie | Endpoint telemetry and detections |
| Endpoints | Windows clients | Victims for realistic SOC scenarios |
| Attack host | Kali (isolated) | Safe simulation source for case generation |

## Network layout
| Segment | CIDR | Notes |
| --- | --- | --- |
| MGMT | 192.168.50.0/24 | FortiGate and Proxmox management |
| WORK | 10.10.10.0/24 | SOC stack and domain-joined endpoints |
| HOME | 10.20.20.0/24 | Compromised-host simulation zone (Kali lives here) |

Policy intent: allow only what is needed for case generation, keep SOC infrastructure protected, log allow and deny for evidence.

## Telemetry sources used in cases
| Source | Where it appears | Why it matters |
| --- | --- | --- |
| FortiGate traffic logs | Network perspective | Source and destination validation, segmentation evidence |
| Windows Security logs | Host perspective | Logon events, user and privilege changes |
| Sysmon | Host process visibility | Process tree, command line, persistence signals |
| Wazuh | SIEM workflow | Alerting, dashboards, correlation |
| LimaCharlie | EDR workflow | Detection signals, timeline pivoting |
| Velociraptor | DFIR workflow | Evidence collection, hunts, artifact queries |

## How to use this repo
### Add a new case (fast path)
1) Copy folder `cases/_template` into `cases/NN-short-title`
2) Update text inside scenario, detection, triage, investigation, remediation, rollback
3) Put screenshots and exports into `cases/NN-short-title/evidence/`
4) Keep the case repeatable using VM snapshots

### Evidence quality bar
Minimum evidence set per case:
FortiGate log view for src and dst
one relevant Windows Security event
one relevant Sysmon event
one Wazuh or LimaCharlie view showing the signal
one Velociraptor collection result that supports the conclusion

## Case index
| ID | Title | Status |
| --- | --- | --- |
| 01 | RDP logon + Encoded PowerShell (benign) | In progress |

## Roadmap
Goal: 20 realistic cases with safe simulations, no malware, no destructive testing.
Coverage targets: execution, persistence, identity and logon, discovery, lateral movement, defense evasion, DFIR collections.

## Safety and constraints
No services exposed to the internet
No bridging office network into the lab domain
Snapshots before critical changes and before each case
