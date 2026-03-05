# Case {{ID}} — {{TITLE}}

## Goal
{{ONE_LINE_GOAL}}

## Environment
- Attacker/Source: {{SRC_HOST}} ({{SRC_IP}})
- Victim: {{VICTIM_HOST}} ({{VICTIM_IP}}, {{DOMAIN}})
- Telemetry: Sysmon, Security, Wazuh, LimaCharlie, Velociraptor, FortiGate

## Steps (safe)
1) [](./cases/temp_photo/image.png)

2) {{STEP_2}}
3) {{STEP_3_OPTIONAL}}

## Expected signals
- Security: {{SECURITY_EVENTS}}
- Sysmon: {{SYSMON_EVENTS}}
- Network: FortiGate src={{SRC_IP}} dst={{VICTIM_IP}}
