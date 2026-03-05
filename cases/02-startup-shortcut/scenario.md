# Case 02 — Startup persistence via user shortcut (Telegram Web)

Goal
Validate and investigate user-level persistence created by a typical employee: adding an app shortcut to Startup for convenience.

Environment
Victim: WinTest10 (wintest10.arata.lab), user: WINTEST10\Admin
Persistence location: User Startup folder (shell:startup)
Telemetry: Sysmon, Wazuh, LimaCharlie, Velociraptor

Start
Thursday, March 5, 2026 6:21:28 PM

End
Persistence confirmed and attributed to the logged-in user. No removal performed (user-confirmed change).
