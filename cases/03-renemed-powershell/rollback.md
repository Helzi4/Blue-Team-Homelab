# Rollback

After the Atomic Red Team simulation, the environment was restored to its original state.

Cleanup actions performed:

1. Deleted the masqueraded executable.

File path:

C:\Users\Admin\AppData\Roaming\taskhostw.exe

Command used:

Remove-Item "$env:APPDATA\taskhostw.exe"

2. Verified that the file no longer exists.

3. Reviewed potential persistence locations including:

Startup folder  
Scheduled tasks  
Registry Run keys

No persistence artifacts were identified.

The system was successfully returned to its original state.