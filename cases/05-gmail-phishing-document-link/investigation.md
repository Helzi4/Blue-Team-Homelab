# Investigation

## Step 1 — Confirm Email Delivery
The suspicious email was present in the user's Gmail inbox with the subject:

`Updated invoice shared with you`

The sender address and the message content were captured as evidence.

## Step 2 — Confirm User Interaction
Gophish campaign telemetry confirmed the following:
- email delivered,
- email opened,
- link clicked.

This validated that the user interacted with the phishing-style lure.

## Step 3 — Confirm Endpoint Network Activity
LimaCharlie timeline telemetry showed `chrome.exe` on `WinTest10` establishing an outbound TCP connection from `10.10.10.100` to `10.10.10.101:8080`.

This confirmed that the click resulted in a browser connection to the decoy host.

## Step 4 — Confirm Decoy Page Access
The browser on the endpoint displayed the internal decoy page titled `Invoice Preview`, confirming successful navigation to the hosted phishing simulation page.

## Step 5 — Check for Follow-on Activity
The reviewed evidence did not confirm:
- credential submission,
- file download,
- script execution,
- persistence creation,
- or second-stage payload activity.

## Conclusion
The investigation confirmed phishing-style user interaction with a successful link click and browser connection to the decoy page.

No evidence of credential theft, malware execution, persistence, or broader host compromise was identified during the reviewed timeframe.