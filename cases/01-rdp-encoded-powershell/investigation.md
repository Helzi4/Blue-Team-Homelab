# Investigation

## Velociraptor collections
- Windows.EventLogs.EvtxHunter
  Channels: Security and Microsoft-Windows-Sysmon/Operational
  Window: 10-15 minutes around the incident time
- Windows.Sys.Processes (confirm cmdline and parent process)
- Windows.Network.Netstat (check for suspicious network from the process)
- Windows.Sys.Users (confirm logged-on sessions)

## Questions answered
Who/where:
RDP logon to WinTest10 from 10.20.20.10 (Security 4624, LogonType 10)

What executed:
powershell.exe executed with -Enc (Sysmon EID 1, commandLine field)

Network/exfil:
Check Netstat for new outbound connections at the time of execution
No exfil validated in this benign simulation

Persistence:
Not expected in this case
Validated by checking StartupItems and absence of new scheduled tasks/services in the time window
