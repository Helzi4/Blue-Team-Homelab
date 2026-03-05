# Investigation

## Velociraptor collections
- Windows.Sys.Processes (cmdline/parent)
- Windows.Network.Netstat (connections)
- Windows.EventLogs.EvtxHunter (Security + Sysmon in {{TIME_WINDOW}})
- Windows.Persistence.StartupItems / ScheduledTasks (if applicable)

## Questions answered
- Who/where: {{Q1_ANSWER}}
- What executed: {{Q2_ANSWER}}
- Network/exfil: {{Q3_ANSWER}}
- Persistence: {{Q4_ANSWER}}
