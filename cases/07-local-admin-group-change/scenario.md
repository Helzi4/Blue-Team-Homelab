# Case 07: Local Administrators Membership Change Investigation

## Summary
A suspicious local privilege change was identified on `WinTest10` after a standard domain user was added to the local `Administrators` group. The activity was reviewed using Wazuh, Sysmon, local host verification, and supporting security context from the endpoint.

The case focused on determining whether the privilege assignment represented authorized administrative work or suspicious privilege escalation. The reviewed evidence confirmed the group membership change, but did not confirm immediate follow-on use of the granted administrative access during the investigation window.

## Reported Situation
Security telemetry on `WinTest10` showed command execution consistent with local administrative group enumeration and modification. Further review identified a command that added a standard domain user to the local `Administrators` group.

Because granting local administrative rights materially changes host security posture, the event was treated as suspicious until administrative authorization could be validated.

## Affected Asset
- **Hostname:** `WinTest10`
- **Role:** Windows workstation

## Affected Account
- **Added User:** `ARATA\ops.user2`

## Investigative Goal
The investigation aimed to determine:
- whether a standard domain user was actually added to the local `Administrators` group;
- how the change was executed;
- whether the account was used immediately after the change;
- and whether the event should be classified as suspicious privilege escalation.

## Scope
This case is limited to the reviewed activity on `WinTest10` and the available evidence from:
- Wazuh
- Sysmon
- local host verification
- supporting endpoint security context

## Analyst Context
At the time of review, the available evidence supported the privilege change itself. However, the root cause of how the administrative action became possible was not directly established from the collected artifacts.