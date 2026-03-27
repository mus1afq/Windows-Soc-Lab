# Detection: Repeated Failed Logons

## Objective
Identify failed authentication attempts that may indicate password guessing or unauthorized access attempts.

## Log Source
Windows Security Log

## Relevant Event ID
- `4625` — Failed logon

## Detection Logic
Monitor for multiple failed logon events over a short period and review the target account, logon type, process name, and source context.

## Why It Matters
Repeated failed authentication can indicate user error, password spraying, brute-force attempts or other unauthorized access attempts.

## Lab Evidence

The Security log was filtered to show Event ID 4625 entries after repeated incorrect password attempts.

![Security Event 4625 Overview](../screenshots/security-event4625-overview.png)

The event details provided the most useful investigation fields, including status codes, logon type, process name and source address.

![Security Event 4625 Status and Logon Type](../screenshots/security-event4625-status-logontype.png)

## Notable Fields
- `Status: 0xc000006d`
- `SubStatus: 0xc0000380`
- `LogonType: 2`
- `ProcessName: C:\Windows\System32\svchost.exe`
- `IpAddress: 127.0.0.1`

## Analyst Notes
A `LogonType` value of `2` indicates an interactive logon attempt, meaning the sign-in was made directly at the local console rather than through a network or remote service. In this lab, that matches the test method of entering an incorrect password on the VM login screen.

The `Status` code `0xc000006d` shows that the logon failed because of invalid credentials. The `SubStatus` value gives more detail on the failure condition and can help distinguish between incorrect passwords, account restrictions, or other authentication issues.

The `ProcessName` field showing `C:\Windows\System32\svchost.exe` is expected in this context because Windows authentication activity is often handled through system processes rather than a user-launched application. The `IpAddress` value `127.0.0.1` indicates the activity originated from the local machine, which is consistent with an interactive login test rather than an external remote attempt.

In a real investigation, an analyst would not stop at the failed logon event alone. Useful follow-up steps would include:
- checking for any `4624` successful logon events shortly after the failures
- reviewing whether the same account was targeted repeatedly over a longer period
- comparing the timestamps to determine whether the failures were isolated or part of a pattern
- checking whether other accounts were also targeted, which could suggest password spraying
- reviewing host context, session type and any related process activity around the same time
- confirming whether the source system, account and login behaviour were expected for that user

This kind of event becomes more concerning when it appears repeatedly, affects privileged accounts, is followed by a successful logon, or is seen across multiple systems or usernames. In a SOC environment, repeated `4625` events are often used as an early indicator for brute-force attempts, password spraying or unauthorized access activity.
