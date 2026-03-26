# Investigation

## Step 1 — Confirm Source and Destination
FortiGate logs showed traffic from `10.20.20.10` to `10.10.10.100`.

## Step 2 — Identify the Services Targeted
The firewall telemetry showed connection attempts associated with:
- DCE-RPC
- RDP
- SAMBA
- SMB

This indicated probing of common Windows-accessible services.

## Step 3 — Validate on the Endpoint
LimaCharlie endpoint telemetry on `WinTest10` confirmed inbound network activity associated with the same source IP `10.20.20.10`.

Relevant events included:
- `NETWORK_CONNECTIONS`
- traffic involving `svchost.exe`
- Windows services such as `TermService` and `RPCSS`
- connections involving ports `139` and `445`

This provided host-side confirmation that the scan reached the destination endpoint.

## Step 4 — Normalize Timestamps
FortiGate and LimaCharlie displayed different timestamps, likely due to timezone or display setting differences.  
Before building the final timeline, timestamps were normalized to account for this offset.

## Step 5 — Look for Follow-on Activity
During the reviewed investigation window, no evidence was found of:
- successful RDP logon
- authenticated SMB session
- command execution
- payload delivery
- persistence creation

## Conclusion
The observed activity was consistent with internal network service discovery against a Windows host.

The investigation confirmed reconnaissance behavior but did not confirm successful exploitation or follow-on compromise during the reviewed timeframe.