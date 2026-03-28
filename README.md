# Blue Team Homelab (SOC / DFIR)

Enterprise-style Blue Team homelab focused on alert triage, investigation, evidence collection, and repeatable SOC case writeups.

## Scope

Hi

This repository documents practical SOC / DFIR investigations built in a segmented internal lab.

Core focus:
- alert triage
- Windows log analysis
- endpoint telemetry correlation
- host validation
- containment and remediation logic
- clear separation between confirmed facts and unconfirmed theory

## Lab Stack

| Area | Technology |
|---|---|
| Virtualization | Proxmox VE |
| Firewall / Segmentation | FortiGate 40F |
| Identity | Windows Server 2022 Domain Controller |
| SIEM | Wazuh |
| EDR / Telemetry | LimaCharlie |
| DFIR | Velociraptor |
| Endpoint Telemetry | Sysmon |
| Native Protection | Microsoft Defender |
| Simulation Host | Kali Linux |
| Endpoints | Domain-joined Windows clients |

## Network Layout

| Segment | Subnet | Purpose |
|---|---|---|
| MGMT | 192.168.50.0/24 | Management and security infrastructure |
| WORK | 10.10.10.0/24 | Windows endpoints and internal workstation activity |
| HOME | 10.20.20.0/24 | Isolated simulation segment |

## Investigation Method

Each case is documented with the same structure:

- `scenario.md`
- `detection.md`
- `triage.md`
- `investigation.md`
- `remediation.md`
- `rollback.md`

Each writeup is built from actual lab telemetry and supporting screenshots.

## Case Index

| ID | Case | Status | Primary Focus | Main Question Answered |
|---|---|---|---|---|
| 01 | RDP Encoded PowerShell | Complete | Remote logon + suspicious PowerShell execution | Was the remote PowerShell activity malicious or benign? |
| 02 | Startup Shortcut | Complete | Persistence false positive investigation | Did the startup artifact represent real persistence or benign software behavior? |
| 03 | Masqueraded PowerShell | Complete | Masquerading / suspicious process identity | Was the observed PowerShell-related process behavior deceptive or expected? |
| 04 | Internal Port Scan Against Windows Host | Complete | Internal reconnaissance | Did the host experience suspicious internal discovery activity? |
| 05 | Gmail Phishing Document Link | Complete | Phishing-style user interaction | Did the user interaction lead to confirmed compromise or only suspicious exposure? |
| 06 | SMB Failed Logon Investigation | Complete | Authentication failures / password-spray-style investigation | Were the failed logons isolated mistakes or suspicious repeated unauthorized attempts? |
| 07 | Local Admin Group Change | Complete | Privilege escalation / local admin rights change | Was local administrative access granted without validated authorization? |

## What the Cases Cover

| Category | Covered |
|---|---|
| Suspicious execution | Yes |
| False positive investigation | Yes |
| Process masquerading | Yes |
| Internal reconnaissance | Yes |
| Phishing-style activity | Yes |
| Repeated failed authentication | Yes |
| Privilege escalation | Yes |

## Evidence Sources Used

Depending on the case, evidence may include:

- Wazuh alerts and event details
- Windows Security Event Logs
- Sysmon process and host telemetry
- LimaCharlie process / endpoint context
- FortiGate network logs
- Velociraptor collections
- local host verification

Not every case uses every tool. Evidence is included only when it adds value to the conclusion.

## Repository Layout

```text
.
├── README.md
└── cases/
    ├── 01-rdp-encoded-powershell/
    ├── 02-startup-shortcut/
    ├── 03-masqueraded-powershell/
    ├── 04-internal-port-scan-against-windows-host/
    ├── 05-gmail-phishing-document-link/
    ├── 06-smb-failed-logon-investigation/
    ├── 07-local-admin-group-change/
    ├── _template/
    └── temp_photo/