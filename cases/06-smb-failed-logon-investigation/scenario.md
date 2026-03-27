# Case 06: SMB Failed Logon Investigation

## Summary
A Windows workstation generated repeated authentication failure events over SMB during a short time window. The activity affected multiple domain user accounts and originated from a host in a different network segment.

The case began as a suspicious authentication alert observed in Wazuh on `wintest` and was investigated using Windows Security logs and FortiGate traffic telemetry. Review of the available evidence confirmed multiple failed network logon attempts against the host, but did not confirm successful authentication or post-authentication activity.

## Reported Situation
The SOC observed repeated Windows logon failures on `WinTest10` involving multiple accounts in the `ARATA.LAB` domain. Because the failures originated from another subnet and targeted more than one user account over SMB, the activity was treated as suspicious and potentially consistent with password spraying or repeated unauthorized access attempts.

## Affected Asset
- **Hostname:** `wintest10`
- **IP Address:** `10.10.10.100`

## Source of Activity
- **Source Host:** `KALI`
- **Source IP:** `10.20.20.10`

## Accounts Observed
- `ops.user1`
- `ops.user2`

## Investigation Goal
Determine whether the observed authentication failures represented:
- routine user error,
- repeated unauthorized access attempts,
- or password-spray-style activity,

and verify whether any successful authentication or follow-on activity occurred.

## Scope
This case is limited to the reviewed alert window and the telemetry collected from:
- Wazuh
- Windows Security Event Log
- FortiGate
- LimaCharlie