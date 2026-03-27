# Detection Notes

## Detection Objective
Identify suspicious repeated failed authentication attempts against a Windows workstation, especially where:
- the activity originates from another subnet,
- multiple accounts are targeted,
- and the failures occur over a short time window.

## Primary Detection Source
**Wazuh** served as the initial analyst-facing detection source for this case.

Relevant alert descriptions observed in the reviewed window included:
- `Logon Failure - Unknown user or bad password`
- `Multiple Windows Logon Failures`

These alerts were sufficient to trigger triage and justify pivoting into native Windows authentication logs.

## Supporting Evidence Sources
- **Windows Security Log**
  - Event ID `4625`
- **FortiGate**
  - SMB traffic from `10.20.20.10` to `10.10.10.100`
- **LimaCharlie**
  - reviewed during investigation, but no relevant authentication detection was identified for this activity

## Why the Activity Was Suspicious
The activity was suspicious because:
1. repeated failed logons occurred within a short time window;
2. more than one domain user account was targeted;
3. the source was a host in a different network segment;
4. the protocol involved SMB network access rather than a local interactive mistake.

This combination is consistent with behavior commonly triaged as:
- repeated unauthorized access attempts, or
- password-spray-style activity.

## Key Windows Security Fields
The most important fields observed in Event ID `4625` were:
- `TargetUserName`
- `TargetDomainName`
- `IpAddress`
- `WorkstationName`
- `LogonType`
- `AuthenticationPackageName`
- `Status`
- `SubStatus`

## Detection Limitations
Based on the evidence collected for this case:
- Wazuh provided the initial signal and useful alert context;
- Windows Security logs provided the strongest evidentiary detail;
- LimaCharlie did not provide a useful auth-focused detection for this activity.

## Tuning Notes
This type of detection can be strengthened by:
- correlating multiple `4625` events by source IP over a short time window;
- elevating severity when multiple accounts are targeted from the same source;
- differentiating between single-user mistypes and multi-account spray-like behavior;
- enriching alerts with source IP, workstation name, and logon type.