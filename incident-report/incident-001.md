# Incident 001: Failed Logon Activity

## Summary
Multiple failed logon attempts were generated and reviewed on the Windows host during lab testing.

## Objective
The aim of this investigation was to identify and review failed authentication activity using native Windows Security logs and document the evidence in a SOC-style format.

## Data Source
- Windows Security Log
- Event ID `4625`

## Investigation Steps

### 1. Generate failed logon activity
Repeated incorrect password attempts were made on the local Windows VM to generate failed authentication events.

### 2. Review the Security log
The Windows Security log was filtered for Event ID `4625` to identify failed logon activity.

![Security Event 4625 Overview](../screenshots/security-event4625-overview.png)

### 3. Review event details
The event details confirmed failed interactive logon attempts and provided useful investigation fields such as status codes, logon type, process name, and IP address.

![Security Event 4625 Details Top](../screenshots/security-event4625-details-top.png)

![Security Event 4625 Status and Logon Type](../screenshots/security-event4625-status-logontype.png)

## Findings
Three failed logon events were identified after repeated incorrect password attempts on the local Windows VM.

Notable values observed:
- **Status:** `0xc000006d`
- **SubStatus:** `0xc0000380`
- **LogonType:** `2`
- **ProcessName:** `C:\Windows\System32\svchost.exe`
- **IpAddress:** `127.0.0.1`

## Assessment
This pattern is consistent with repeated interactive logon failure on the local machine. In a real environment, similar activity could indicate password guessing, user login failure or unauthorized access attempts.

## Recommended Actions
- Review the affected account
- Check whether any successful logon followed the failed attempts
- Review source session or workstation context
- Consider account lockout and MFA controls in enterprise environments

## Outcome
The lab successfully demonstrated how Windows Security logs can be used to detect and investigate failed authentication activity.
