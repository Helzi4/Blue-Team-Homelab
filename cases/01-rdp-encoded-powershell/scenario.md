# Case 01 — RDP logon + Encoded PowerShell (benign)

## Goal
Simulate a realistic SOC alert chain: remote logon -> suspicious PowerShell execution -> triage & evidence collection.

## Environment
- Attacker (compromised host): 10.20.20.10 (Kali)
- Victim: 10.10.10.100 (WinTest10, domain arata.lab)
- Telemetry: Sysmon, Windows Security logs, Wazuh, LimaCharlie, Velociraptor, FortiGate traffic logs

## Attack steps (safe)
1) RDP logon from 10.20.20.10 to WinTest10.
2) Execute benign encoded PowerShell:
   - Start-Process notepad via `powershell.exe -enc ...`

## Expected signals
- Windows Security: 4624 (LogonType 10), Source IP 10.20.20.10
- Sysmon: Event ID 1 with `powershell.exe` and `-enc`
- EDR/SIEM: detection on encoded PowerShell + correlation with prior logon
