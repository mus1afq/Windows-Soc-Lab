# Windows SOC Lab with Sysmon

## Overview
This project demonstrates a Windows SOC lab built on a local Windows VM using Sysmon and native Windows Event Logs. The goal was to generate and investigate process creation activity and failed logon events.

## Tools Used
- Sysmon64a
- Windows Event Viewer
- PowerShell
- Command Prompt

## Detection Use Cases
1. Process and PowerShell activity review using Sysmon
2. Repeated failed logons using Windows Security Event ID 4625

## Key Evidence
- Sysmon Event ID 1 and Event ID 5 telemetry captured successfully
- Process creation events observed for whoami.exe, hostname.exe, ipconfig.exe, mmc.exe, and powershell.exe
- Multiple Security Event ID 4625 entries generated and reviewed after failed interactive logon attempts

## Notable Findings
- Interactive failed logons recorded with LogonType 2
- Failure details included Status 0xc000006d and SubStatus 0xc0000380
- Local source context showed IpAddress 127.0.0.1

## Screenshots
- security-event4625-overview
- security-event4625-details-top
- security-event4625-status-logontype
- sysmon-event1-whoami
- sysmon-event1-hostname
- sysmon-event1-ipconfig
- sysmon-event1-mmc-eventviewer
- sysmon-event1-backgroundtaskhost
- sysmon-event1-msedge
- sysmon-event1-taskhostw

## Outcome
The lab demonstrated basic host-based monitoring, process visibility, and authentication event investigation using Windows-native telemetry and Sysmon.
