# Remediation

Contain
In production I would isolate the endpoint via EDR and preserve volatile evidence.

Credentials
Reset or rotate credentials used for the remote logon.
Review recent logons for the same account across endpoints.

Cleanup
No malicious artifacts were created in this benign simulation.
If this was real: remove any dropped files, scripts, and suspicious scheduled tasks.

Hardening
Restrict RDP exposure, enforce MFA where possible, limit admin rights, and monitor remote logons from unusual segments.

Tuning
Increase fidelity by correlating:
Security 4624 LogonType 10 (remote logon) + Sysmon EID 1 (powershell -Enc) within a short time window.
