# Scenario

A Windows workstation (`10.10.10.100`) received multiple inbound connection attempts from an internal host (`10.20.20.10`) over a short time window.

The targeted services included:
- DCE-RPC
- SMB / SAMBA
- RDP

The goal of the investigation was to determine whether the activity was benign internal administration or suspicious internal reconnaissance consistent with network service discovery.