# Initial Triage

## Initial Alert
Wazuh surfaced suspicious command activity on `WinTest10` involving `net.exe` / `net1.exe` and the `localgroup administrators` command sequence.

This was treated as a potentially high-risk event because it suggested either:
- privileged discovery against the local administrators group, or
- direct modification of local administrative membership.

## Initial Assessment
At triage time, the activity was concerning because:
- it referenced the local `Administrators` group directly;
- it occurred under elevated context on a workstation;
- it could represent unauthorized privilege escalation through administrative group membership assignment.

## Key Questions
The investigation focused on the following questions:
1. Was a standard user actually added to local `Administrators`?
2. Which account executed the change?
3. Was the change part of approved administrative work?
4. Was the newly added account used after privilege assignment?
5. Was there evidence of broader compromise or follow-on activity?

## Immediate Pivots
The analyst pivoted into:
- Wazuh document details for command-line context,
- Sysmon Process Create telemetry,
- local host verification of the `Administrators` group,
- supporting security context on the endpoint.

## Triage Findings
Early review showed:
- command execution involving `localgroup administrators`;
- Wazuh telemetry tied to `net1.exe`;
- supporting Sysmon evidence showing the `/add` operation for `ARATA\ops.user2`;
- subsequent host confirmation that the domain user had been added to the local `Administrators` group.

## Initial Severity View
The event was treated as a high-risk privilege change because it granted local administrative access to a standard domain user. Even without immediate evidence of follow-on use, the change created a materially elevated risk condition on the host.

## What Was Not Yet Confirmed at Triage
At the start of triage, the following were not yet confirmed:
- whether the privilege change was authorized;
- whether the added account was later used interactively;
- whether the action originated from prior credential compromise;
- whether the event was part of a larger intrusion chain.