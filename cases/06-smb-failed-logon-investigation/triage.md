# Initial Triage

## Initial Alert
Wazuh surfaced repeated authentication failure activity on `wintest` during the review window. The most relevant alerting context included:
- `Logon Failure - Unknown user or bad password`
- `Multiple Windows Logon Failures`

## Initial Assessment
At triage time, the activity appeared suspicious because:
- multiple failed logons were recorded close together;
- the activity affected multiple user accounts;
- the source was external to the target subnet;
- the access pattern was consistent with SMB network authentication attempts.

## Key Questions
The investigation focused on the following questions:
1. Were the failed logons isolated user mistakes or repeated unauthorized attempts?
2. Did the activity affect one account or multiple accounts?
3. Did any authentication succeed?
4. Was there any evidence of interactive access or follow-on activity after the failures?
5. Was the source internal administrative activity or suspicious hostile behavior?

## Immediate Pivots
The analyst pivoted into:
- Wazuh event details for source/target context,
- Windows Security Event ID `4625`,
- FortiGate SMB traffic logs,
- LimaCharlie for supporting endpoint context.

## Triage Findings
Initial review showed:
- repeated failed logons on `WinTest10`;
- source IP `10.20.20.10`;
- source workstation `KALI`;
- domain users `ops.user1` and `ops.user2` targeted;
- network logon activity over SMB.

## Initial Severity View
This activity warranted investigation because it represented repeated failed authentication attempts against a workstation from another network segment. At triage stage, the most appropriate working classification was:

**Suspicious authentication activity consistent with password spraying or repeated unauthorized access attempts.**

## What Was Not Yet Confirmed at Triage
At the start of triage, the following had not yet been confirmed:
- successful authentication,
- interactive access,
- execution on the target host,
- persistence,
- lateral movement beyond the failed attempts.