# Triage (10 minutes)

1) Confirm scope
Host: WinTest10
User: WINTEST10\Admin
Time window: last 30 minutes around the alert

2) Validate persistence indicator
Wazuh shows Sysmon EID 11 creating:
...\Startup\AutoStart - TG.lnk

3) Validate execution
LimaCharlie timeline shows:
chrome.exe https://web.telegram.org/
execution under the same user context

4) Quick severity
Medium by default (persistence location). Escalate if user denies the change or if target is suspicious (unknown binary, unusual parent, odd timing).

5) Immediate actions
Collect StartupItems via Velociraptor
Capture process evidence (chrome command line)
Confirm attribution with user
