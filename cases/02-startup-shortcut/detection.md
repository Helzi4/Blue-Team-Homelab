# Detection

Trigger
High-fidelity persistence indicator: file created in user Startup folder (Startup .lnk).

Wazuh (Sysmon)
Primary signal:
Sysmon Event ID 11 (FileCreate) where targetFilename contains:
\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\

Example query
agent.name:wintest AND data.win.system.eventID:11 AND data.win.eventdata.targetFilename:*\\Programs\\Startup\\*.lnk

LimaCharlie
Confirm execution:
chrome.exe started with command_line containing https://web.telegram.org/
Context:
user, parent process, timestamp close to logon

Notes
This can be legitimate (user convenience) or malicious (persistence). Requires verification and user confirmation.
