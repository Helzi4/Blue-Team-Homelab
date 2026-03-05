# Triage (10 minutes)

1) Confirm scope
Host: WinTest10 (10.10.10.100)
Time: use the timestamps from Security 4624 and Sysmon EID 1 (see evidence)

2) Validate access vector
Security 4624 confirms a successful logon.
Check:
LogonType = 10 (RDP)
Source Network Address = 10.20.20.10
Account used = the RDP user

3) Validate execution
Sysmon Operational Event ID 1 shows:
Image = powershell.exe
CommandLine contains -Enc (EncodedCommand)

4) Quick severity
High suspicion when encoded PowerShell follows an interactive remote logon from a non-admin segment.

5) Immediate actions (production mindset)
Collect evidence (logs + VR collections)
Scope for similar executions on other endpoints
If confirmed malicious: isolate endpoint, reset credentials used in the logon
