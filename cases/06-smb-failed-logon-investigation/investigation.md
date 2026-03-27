# Investigation

## Investigation Summary
The investigation confirmed repeated failed SMB logon attempts against `WinTest10` from `10.20.20.10`. The activity affected at least two domain user accounts and generated repeated Windows Security Event ID `4625` entries. FortiGate telemetry confirmed corresponding SMB traffic between the source and target hosts.

No relevant LimaCharlie detection was identified for this authentication activity in the reviewed evidence set.

## Timeline Overview
The reviewed event window showed clustered failed authentication attempts over SMB within a short time period. Wazuh surfaced repeated failed logon alerts, which were then validated in Windows Security logs and correlated with firewall telemetry.

## Wazuh Findings
Wazuh provided the initial detection context for the case. Alerts observed on `wintest` included:
- `Logon Failure - Unknown user or bad password`
- `Multiple Windows Logon Failures`

The event details showed:
- **Agent Name:** `wintest`
- **Agent IP:** `10.10.10.100`
- **Source IP:** `10.20.20.10`
- **Logon Type:** `3`
- **Target User:** `ops.user2`
- **Target Domain:** `ARATA.LAB`
- **Authentication Package:** `NTLM`
- **Status:** `0xc000006d`
- **SubStatus:** `0xc000006a`

These fields supported the conclusion that the failures were real Windows authentication events and not merely generic shell or process anomalies.

## Windows Security Log Findings
Windows Security Event ID `4625` provided the strongest evidence in this case.

Reviewed `4625` events showed:
- **TargetUserName:** `ops.user1`
- **TargetUserName:** `ops.user2`
- **TargetDomainName:** `ARATA.LAB`
- **WorkstationName:** `KALI`
- **IpAddress:** `10.20.20.10`
- **LogonType:** `3`
- **LogonProcessName:** `NtLmSsp`
- **AuthenticationPackageName:** `NTLM`
- **Status:** `0xc000006d`
- **SubStatus:** `0xc000006a`

### Interpretation
These fields indicate:
- the attempts were network logons rather than local interactive logons;
- the source of the activity was the host identified as `KALI`;
- multiple account authentication failures occurred against the same workstation;
- the credentials presented were invalid.

This evidence is consistent with repeated failed SMB authentication attempts and supports a password-spray-style or repeated unauthorized access interpretation.

## FortiGate Findings
FortiGate forward traffic logs showed repeated SMB connections:
- **Source:** `10.20.20.10`
- **Destination:** `10.10.10.100`
- **Application Name:** `SMB`
- **Policy ID:** `10 (ATTACK_TO_WORK)`

This network telemetry correlates with the Windows authentication failures and confirms that the observed activity was associated with real SMB traffic between the two hosts.

## LimaCharlie Findings
LimaCharlie was reviewed as an additional source during the investigation. No relevant auth-focused detection tied to the failed SMB logons was identified in the evidence collected for this case.

This did not materially weaken the investigation because the primary auth evidence came from:
- Wazuh alerting context,
- Windows Security Event ID `4625`,
- FortiGate traffic logs.

## Confirmed Findings
The following points were confirmed:
- repeated failed SMB logon attempts occurred against `WinTest10`;
- the activity originated from `10.20.20.10`;
- the source workstation was recorded as `KALI`;
- multiple domain user accounts were targeted;
- the failures were recorded as Windows Security Event ID `4625`;
- corresponding SMB traffic was present in FortiGate logs.

## Not Confirmed
Based on the evidence collected for this case, the following were **not confirmed**:
- successful authentication,
- interactive user logon,
- code execution on the target,
- persistence,
- post-authentication activity,
- lateral movement beyond the failed access attempts.

## Final Verdict
Multiple failed SMB logon attempts were observed against `WinTest10` from `10.20.20.10`. Windows Security logs confirmed repeated `4625` authentication failures involving multiple user accounts, and FortiGate telemetry confirmed corresponding SMB connections over the network.

The activity is best classified as:

**Suspicious repeated authentication failures consistent with password-spray-style activity or repeated unauthorized access attempts.**

At the time of investigation, no successful authentication or post-authentication activity was confirmed in the collected evidence.