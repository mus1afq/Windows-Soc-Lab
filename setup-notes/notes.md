# Setup Notes

## Environment
- Platform: Windows VM on ARM

## Tools Installed
- Sysmon64a
- Event Viewer
- PowerShell

## Log Locations
- Sysmon: `Applications and Services Logs > Microsoft > Windows > Sysmon > Operational`
- Security: `Windows Logs > Security`

## Initial Validation
- Confirmed Sysmon installation
- Observed Sysmon Event ID 1 and Event ID 5 telemetry
- Logged process activity for `whoami.exe`, `hostname.exe`, `ipconfig.exe`, `mmc.exe` and `powershell.exe`
- Generated multiple failed interactive logon attempts and confirmed Security Event ID 4625 entries

## Goal
Use Windows and Sysmon telemetry to investigate:
- failed logons
- process and PowerShell activity
