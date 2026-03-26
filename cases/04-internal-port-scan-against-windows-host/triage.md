# Triage

## Initial Alert Context
The activity was first identified through FortiGate firewall telemetry showing multiple connections from `10.20.20.10` to `10.10.10.100` within the same second.

## Why It Was Suspicious
The source host contacted several Windows-related service ports in a short burst:
- RPC
- SMB
- RDP

This pattern was consistent with internal service enumeration rather than normal single-service usage.

## Initial Hypotheses
1. Authorized internal administrative check
2. Lab-generated validation traffic
3. Suspicious internal reconnaissance prior to further access attempts

## Priority
Medium

## Scope at Triage Stage
- One source host: `10.20.20.10`
- One destination host: `10.10.10.100`
- Multiple Windows service targets