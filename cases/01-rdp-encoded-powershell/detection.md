# Detection

## Trigger
RDP logon to WinTest10 from 10.20.20.10 followed by PowerShell execution with EncodedCommand.

## Wazuh
Filter:
agent.name:wintest

Look for:
1) RDP logon evidence
data.win.system.eventID:4624

2) Encoded PowerShell execution (Sysmon EID 1)
data.win.system.channel:"Microsoft-Windows-Sysmon/Operational" AND data.win.system.eventID:1 AND data.win.eventdata.image:*powershell.exe* AND data.win.eventdata.commandLine:*Enc*

Notes:
If searching for "-enc" returns nothing, search for "Enc" or query the commandLine field directly because "-" may behave like a NOT operator.

## LimaCharlie
Signal:
PowerShell execution with encoded command line (process = powershell.exe, command_line contains -Enc)

Validate fields:
process path, command_line, user, parent process, timestamp

## Likely false positives
Legitimate admin automation can use encoded PowerShell. Context matters:
remote logon source, unusual account, unusual parent process, execution time, and frequency.
