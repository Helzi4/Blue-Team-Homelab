# Detection

## Detection Logic
This scenario can be detected by identifying:

- one source host
- one destination host
- multiple destination services or ports
- a short time window
- Windows-oriented services such as:
  - RPC
  - SMB
  - RDP

## Primary Telemetry
- FortiGate firewall logs
- LimaCharlie endpoint network telemetry

## Detection Opportunities
- Alert when an internal source touches multiple Windows service ports on a single host within a short interval
- Increase priority when the source host is not part of known administrative infrastructure
- Correlate firewall and endpoint network telemetry for higher confidence

## Detection Tuning Note
This pattern can be noisy in environments with legitimate admin tooling, vulnerability scanning, or management systems.

To reduce false positives:
- allowlist approved admin or scanner hosts
- baseline expected internal scanning behavior
- correlate with successful authentication or follow-on execution before escalating severity