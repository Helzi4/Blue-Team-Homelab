# Remediation

Decision
No removal performed. Change was treated as potentially legitimate and validated first.

User verification
Ask the user:
Did you intentionally add Telegram/Chrome to Startup?
Was this needed for work?

If user confirms
Document as approved startup behavior.
Optional hardening:
limit who can write to Startup in high-risk endpoints, or alert only when target is not allowlisted.

If user denies
Remove the Startup item, isolate endpoint, and hunt for additional persistence locations.
