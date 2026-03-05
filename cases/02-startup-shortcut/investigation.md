# Investigation

Collections
Velociraptor:
- Windows.Persistence.StartupItems (confirm item, path, timestamps)
- Windows.Sys.Processes (confirm chrome cmdline and user)
- Windows.EventLogs.EvtxHunter (Sysmon + Security in time window)

Findings
- Persistence: AutoStart - TG.lnk exists in user Startup folder
- Execution: chrome.exe launched with https://web.telegram.org/
- Attribution: activity matches logged-in user context (WINTEST10\Admin) and timing

Conclusion
Likely user-initiated convenience autostart. No evidence of malware or additional persistence in this case.
