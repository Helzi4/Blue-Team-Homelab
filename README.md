# Blue Team Homelab (SOC / DFIR)

Hi, I’m Arata. This repo is my SOC Analyst portfolio built around an enterprise-style homelab and a set of repeatable incident cases. I use it to practice the day-to-day SOC workflow and to show how I think, what I collect, and how I justify conclusions with evidence.

If you are hiring, the fastest way to review me is
1) read the architecture notes
2) open a case folder under `cases/`
3) check the evidence and the Velociraptor collections that support the writeup

## What I am building
A realistic blue team environment with clear segmentation, identity, endpoint telemetry, and DFIR tooling. I focus on practical detection engineering, triage, investigation, and response steps that a SOC analyst actually does.

Everything is internal. No services are exposed to the internet. Access is only inside the lab or through VPN.

## Stack
Compute
Proxmox VE for virtualization and snapshots

Network
FortiGate 40F for VLAN segmentation, policy enforcement, and traffic logging

Identity
Windows Server 2022 DC (arata.lab) with DNS, GPO, LDAPS, AD CS

Security platforms
Wazuh for SIEM workflows and dashboards  
LimaCharlie for EDR telemetry and detections  
Velociraptor for DFIR collections, hunts, and evidence gathering

Endpoints
Domain-joined Windows clients with Sysmon and Defender enabled

Attack simulation
Kali in an isolated segment used only for safe simulation and case generation

## Network layout
MGMT 192.168.50.0/24  
WORK 10.10.10.0/24  
HOME 10.20.20.0/24

Design intent
SOC infrastructure stays protected
Simulation traffic is controlled and logged
Cases are repeatable and evidence is preserved

## What I practice here
Detection engineering
I generate signals safely, validate telemetry, and tune rules to reduce noise while keeping coverage.

Triage
I confirm scope, source, affected hosts, timestamps, and initial severity using SIEM and EDR pivots.

Investigation
I collect artifacts with Velociraptor and correlate them with logs to build a timeline and answer what happened, how it happened, and what changed.

Remediation
I document containment and cleanup actions I would take in production, plus improvements to prevent recurrence.

Repeatability
I snapshot victims before each run and document rollback steps so the same case can be reproduced.

`cases/`  
Each case is a compact IR-style writeup with the same file set

`cases/_template/`  
My template used to create new cases quickly and consistently

Each case follows the same flow
scenario -> detection -> triage -> investigation -> remediation -> rollback -> evidence.

## Evidence standards
For every case I try to capture at least
FortiGate traffic log showing src, dst, and time
one relevant Windows Security event
one relevant Sysmon event
a Wazuh or LimaCharlie view showing the signal
a Velociraptor collection result that supports the conclusion

## Roadmap
Goal: 20 realistic SOC cases using safe simulations only, no malware, no destructive testing.
Coverage targets: execution, persistence, identity and logon activity, discovery, lateral movement patterns, defense evasion signals, DFIR collections.

If you want a deeper review, look at the template folder to see how consistent the case format is across the repo.
