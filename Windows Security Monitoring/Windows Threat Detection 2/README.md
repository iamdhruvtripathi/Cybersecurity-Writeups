<p align="center">
  <img src="https://assets.tryhackme.com/img/logo/tryhackme_logo_full.svg" width="150" alt="TryHackMe Logo">
</p>

# Windows Threat Detection 2
|  Room Name | Windows Threat Detection 2 |
|----------|-------|
| Author | Dhruv Tripathi |
| Link | [Windows Threat Detection 2](https://tryhackme.com/room/windowsthreatdetection2) |

# Room Information
```bash Type: Walkthrough
Difficulty: Medium
Tags: - 
Meta Tags: Walkthrough, Walk-through, Write-up, Writeup
Subscription type: Premium
Description:
Discover how to detect and analyze the first steps of threat actors after breaching Windows.
```
## Task 1

### Let's start!

- Answer: `No answer needed`

## Task 2

### Open CMD and type "net user Administrator". Which privileged group does the user belong to?

- We can run `net user Administrator` which shows information about the Windows account named `Administrator`. We can see below that they belong to the `Administrator` local group

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/c87a482a-fedb-45ac-ba01-94c8f921a549" />
</p>

- Answer: `Administrators`

### Open Event Viewer and try to find your command in Sysmon logs. What is the "Image" field of the net command you just run?

- Firstly, I had to go to `Applications and Services Logs` > `Microsoft` > `Windows` > `Sysmon` and then click on `Operational` to find the logs. Then I filtered for Sysmon Event ID `1` which searches for process creation. We target Event ID `1` because running a command-line tool like net triggers the system to launch a brand new executable process. Then, I looked through the logs as I had recently ran it and we can see the `Image` and our net command that we just ran

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/f9cf105a-d54a-4964-896e-fe6f2b98dc83" />
</p>

- Answer: `C:\Windows\System32\net.exe`

## Task 3
