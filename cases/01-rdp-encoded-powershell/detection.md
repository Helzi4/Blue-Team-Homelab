# Detection

## Trigger
{{WHAT_TRIGGERS_ALERT}}

## Wazuh
- Filter: agent={{VICTIM_HOST}}
- Look for: {{WAZUH_LOOKFOR_1}}, {{WAZUH_LOOKFOR_2}}

## LimaCharlie
- Rule/Signal: {{LC_RULE}}
- Validate fields: {{LC_FIELDS}}

## Notes
- Likely false positives: {{FP_NOTES}}
