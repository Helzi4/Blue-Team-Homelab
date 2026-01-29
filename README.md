# Blue Team Homelab (SOC / DFIR) — Proxmox + OPNsense + Wazuh

A hands-on SOC/DFIR homelab built to practice detection engineering, log analysis, and incident investigations.
The focus is on producing repeatable case reports (attack → alert → investigation → tuning) and documenting the lab design.

---

## Goals

- Build a realistic blue-team environment on bare metal (no cloud dependencies).
- Collect host + network telemetry and turn it into actionable detections.
- Practice investigations: timelines, triage, pivoting, and evidence-driven analysis.
- Maintain a portfolio: detections, tuning notes, and case reports.

---

## High-Level Architecture

**Hypervisor:** Proxmox VE  
**Edge:** OPNsense (routing, firewall, VPN)  
**SOC Core:** Wazuh Manager + Dashboard  
**Endpoints:** Windows / Linux VMs

### Network Layout (sanitized example)
- **WAN / upstream network:** `10.0.0.0/24`
- **Lab LAN:** `10.20.20.0/24`
- **SOC server (Wazuh Manager):** `10.20.20.10`
- **VPN subnet (WireGuard):** `10.6.0.0/24`

> Note: All IP ranges shown here are examples. Real environment details are intentionally omitted.

### Remote Access Model
WireGuard is hosted on OPNsense and provides access to the lab LAN.
The lab is not exposed directly to the public internet; access is performed through a secured VPN entry path.

---

## What’s Inside

### OPNsense (Edge)
- Routes traffic between WAN and Lab LAN
- Stateful firewall
- WireGuard for secure remote access
- (Planned) Forward network telemetry (firewall/DHCP/DNS) into the SOC stack

### Wazuh (SOC Core)
- Centralized event collection and alerting
- Dashboard for hunting and analytics
- Agents on endpoints:
  - **Windows:** Security/System/Application + Sysmon (Operational)
  - **Linux:** auth/journal (+ auditd where useful)

---

## Repository Structure

- `docs/` — architecture notes, diagrams, data flows
- `detections/` — custom rules/decoders, Sigma notes, tuning
- `cases/` — investigation write-ups (attack → alert → investigation → tuning)
- `infra/` — deployment notes and automation (later: Ansible/IaC)

---

## Current Status

- [x] Proxmox + segmented lab networking
- [x] OPNsense routing/firewall baseline
- [x] WireGuard access into Lab LAN
- [x] Wazuh deployed and reachable
- [x] First Windows endpoint enrolled (events + Sysmon visible)
- [ ] Add a Linux endpoint agent
- [ ] Ingest OPNsense logs into Wazuh (syslog)
- [ ] First case report: Windows persistence via Scheduled Task

---

## Security Notes

- This is a learning environment.
- No private keys, passwords, tokens, or sensitive identifiers are stored in this repository.
- Configuration examples are sanitized when necessary.
