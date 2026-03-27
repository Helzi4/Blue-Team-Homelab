# Detection Notes

## Detection Objective
Identify suspicious local privilege changes on Windows endpoints, especially when:
- a non-privileged domain user is added to the local `Administrators` group;
- local group modification is performed via `net.exe` or `net1.exe`;
- the activity occurs without clear operational or change-management context.

## Primary Detection Source
**Wazuh** served as the initial analyst-facing source for this case.

The reviewed telemetry showed process activity associated with:
- `net.exe` / `net1.exe`
- `localgroup administrators`
- local administrative group enumeration and modification behavior

The command-line evidence surfaced in Wazuh justified immediate investigation because the activity affected local administrative privilege on the workstation.

## Supporting Evidence Sources
- **Sysmon**
  - Event ID `1` (Process Create)
- **Local Host Verification**
  - confirmation of membership in the local `Administrators` group
- **Supporting Endpoint Security Context**
  - Chrome-related vulnerability findings present on the host

## Why the Activity Was Suspicious
This activity was suspicious because:
1. it involved modification of the local `Administrators` group;
2. the affected user was a standard domain account rather than an established local administrator;
3. local administrative group changes materially increase risk even when no immediate follow-on action is observed;
4. privilege assignment without validated authorization must be treated as suspicious by default.

## Key Fields and Artifacts
The most important evidence points for this case were:
- process image: `net.exe` / `net1.exe`
- command line containing `localgroup administrators`
- specific add operation targeting `ARATA\ops.user2`
- host-side confirmation that the account was present in local `Administrators`

## Detection Considerations
This case highlights that process-based detections can be highly valuable for privilege change triage, especially when:
- Windows Security group management events are noisy, missing, or not surfaced cleanly in the SIEM;
- analysts need to pivot quickly from process telemetry into host validation.

## Tuning Notes
Detection logic can be improved by:
- flagging `net.exe` / `net1.exe` when used with `localgroup administrators`;
- increasing priority when `/add` is present;
- enriching alerts with:
  - initiating account,
  - target host,
  - added account,
  - and whether the account was already a known admin;
- correlating group membership changes with subsequent logon events by the newly added account.