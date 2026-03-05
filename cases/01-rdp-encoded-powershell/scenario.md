# Case 01 — RDP logon + Encoded PowerShell (benign)

## Goal
Simulate a common SOC pattern: interactive remote logon followed by suspicious PowerShell encoded execution.

## Environment
Source: Kali 10.20.20.10 (HOME)
Victim: WinTest10 10.10.10.100 (WORK), domain arata.lab
Telemetry: Windows Security, Sysmon, Wazuh, LimaCharlie, Velociraptor, FortiGate

## Steps (safe)
1) RDP logon from 10.20.20.10 to WinTest10
2) Execute benign encoded PowerShell to start notepad
3) Collect evidence from SIEM, EDR, DFIR tools

## Expected signals
Security: 4624 (LogonType 10, Source Network Address 10.20.20.10)
Sysmon: Event ID 1 (powershell.exe with -Enc in commandLine)
Wazuh: Sysmon event mapped to data.win.eventdata.commandLine
EDR: LimaCharlie timeline/detection for encoded PowerShell
Network: FortiGate traffic showing src/dst activity during the case window
