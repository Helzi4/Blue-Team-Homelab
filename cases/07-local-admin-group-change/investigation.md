# Investigation

## Investigation Summary
The investigation confirmed that a standard domain user, `ARATA\ops.user2`, was added to the local `Administrators` group on `WinTest10`. Wazuh provided the initial command-line telemetry, Sysmon confirmed the explicit `/add` operation, and local host verification confirmed the resulting group membership.

Within the reviewed investigation window, no immediate post-change activity was identified for the newly added account. Because the privilege assignment itself materially increased risk, the event was handled as suspicious privilege escalation pending validation of administrative authorization.

## Timeline Overview
The reviewed evidence showed:
1. elevated command activity on `WinTest10`;
2. `net.exe` / `net1.exe` interaction with the local `Administrators` group;
3. explicit process telemetry showing the addition of `ARATA\ops.user2`;
4. local host confirmation that the user became a member of `Administrators`;
5. no confirmed immediate follow-on use of the newly granted local administrative access in the reviewed window.

## Wazuh Findings
Wazuh served as the initial analyst-facing detection source for the case.

The reviewed event details showed:
- **Agent Name:** `wintest`
- **Agent IP:** `10.10.10.100`
- **Process Image:** `C:\Windows\System32\net1.exe`
- **Command Context:** `localgroup administrators`
- **Integrity Level:** `High`

Wazuh telemetry was sufficient to identify suspicious administrative group interaction and justify escalation into deeper endpoint review.

## Sysmon Findings
Sysmon provided the strongest process-level confirmation of how the change occurred.

Reviewed Sysmon Process Create telemetry showed:
- **Image:** `C:\Windows\System32\net.exe`
- **CommandLine:** `"C:\Windows\System32\net.exe" localgroup administrators ARATA\ops.user2 /add`
- **CurrentDirectory:** `C:\Windows\system32\`
- **Computer:** `WinTest10.arata.lab`

### Interpretation
This evidence confirmed that the host executed a direct local administrative group membership change using the built-in Windows `net.exe` utility. The command line explicitly added `ARATA\ops.user2` to the local `Administrators` group.

## Host Verification Findings
Local host verification confirmed that `ARATA\ops.user2` was present in the local `Administrators` group after the command execution.

This validation established that the privilege change was not merely attempted or logged in isolation; the new administrative membership state was actually present on the endpoint.

## Post-Change Activity Review
After the group membership change was confirmed, the reviewed telemetry did not show immediate follow-on activity associated with the newly added account.

Within the reviewed investigation window, no additional evidence confirmed:
- interactive logon by `ARATA\ops.user2`;
- privileged session establishment using the newly granted access;
- further execution attributable to the added account;
- additional persistence actions;
- immediate lateral movement from the modified host.

Based on the collected evidence, the privilege change itself was confirmed, but immediate operational use of the newly granted administrative access was not observed.

## Supporting Security Context
Additional endpoint security context showed Chrome-related vulnerability findings on the asset. These findings are relevant because unpatched browser exposure can increase the risk of credential theft, administrative session compromise, or attacker access to privileged execution context.

However, these findings do **not** by themselves prove that browser exploitation caused the privilege change.

## Potential Initial Access Hypothesis
One plausible explanation is prior access to an administrative account or administrative execution context. A secondary hypothesis is that browser-related exposure on an administrative system or user context may have contributed to credential theft or session compromise.

This remains a theory only.

At the time of investigation, the collected evidence did **not** directly confirm:
- exploitation of Google Chrome vulnerabilities as the initial access vector;
- theft of administrative credentials through Chrome;
- confirmed compromise of a separate administrative workstation as the proven root cause of the group change.

These possibilities should therefore be documented as investigative leads rather than established facts.

## Confirmed Findings
The following points were confirmed:
- `ARATA\ops.user2` was added to the local `Administrators` group on `WinTest10`;
- Wazuh surfaced suspicious `localgroup administrators` command activity;
- Sysmon confirmed the explicit `/add` operation;
- local host verification confirmed the resulting administrative membership state.

## Not Confirmed
Based on the collected evidence for this case, the following were **not confirmed**:
- immediate logon by the newly added account;
- direct use of the newly granted administrative rights;
- persistence established after the group change;
- follow-on execution tied to `ARATA\ops.user2`;
- a proven root cause for how the privileged action became possible;
- confirmed exploitation of Google Chrome vulnerabilities.

## Final Verdict
A local administrative privilege change on `WinTest10` was confirmed. A standard domain user, `ARATA\ops.user2`, was added to the local `Administrators` group, and the change was validated through Wazuh telemetry, Sysmon process creation evidence, and host-side membership verification.

In the reviewed timeframe, no immediate follow-on use of the newly granted administrative access was confirmed.

In the absence of validated administrative authorization, the activity should be treated as suspicious privilege escalation and escalated for containment and credential review.

As a precautionary response, the affected account was disabled, the host was isolated, and privileged passwords were reset pending validation of potential credential exposure.