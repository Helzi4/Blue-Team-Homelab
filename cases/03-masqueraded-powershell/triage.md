# Triage

## Alert Source

Wazuh SIEM generated alerts related to suspicious command execution and executable file creation in a user directory.

Detected alerts included:

- Executable file dropped in folder commonly used by malware
- Suspicious Windows cmd shell execution
- Windows command prompt started by an abnormal process

Alert Severity:

Level 15

## Initial Observations

The following command was captured:

cmd.exe /c copy %windir%\System32\WindowsPowerShell\v1.0\powershell.exe %APPDATA%\taskhostw.exe /Y

Shortly after, the following executable was launched:

C:\Users\Admin\AppData\Roaming\taskhostw.exe

Key suspicious indicators:

- System process name executed outside System32
- Executable created inside a user writable directory
- Immediate execution after file creation
- Temporary PowerShell script creation inside Temp directory

## Initial Hypothesis

Potential masquerading activity where a legitimate Windows binary is renamed and executed to evade detection mechanisms.

Further investigation required to determine the origin, intent, and impact of the activity.