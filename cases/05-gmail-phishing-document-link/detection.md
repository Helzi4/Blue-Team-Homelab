# Detection

## Detection Source
Initial case awareness came from a user-reported suspicious email.

## Validation Sources
The reported phishing interaction was validated through:
- Gmail message evidence
- Gophish campaign telemetry
- LimaCharlie endpoint network telemetry
- Browser-side evidence showing that the decoy page was opened

## Detection Logic
This type of case can be detected or escalated when:
- a user reports a suspicious email,
- the message contains a link-based lure,
- the user opens the message,
- the user clicks the embedded link,
- and the endpoint establishes an outbound browser connection to an unexpected host or URL.

## Detection Tuning Note
This scenario did not rely on a native SIEM or EDR alert as the initial trigger.
Instead, it began with user reporting and was then validated through available telemetry.

To improve future detection:
- prioritize user-reported emails containing invoice or document-sharing themes,
- correlate browser outbound connections with suspicious or newly observed destinations,
- enrich investigations with URL reputation or email-security telemetry when available.