<p align="center">
  <img src="https://assets.tryhackme.com/img/logo/tryhackme_logo_full.svg" width="150" alt="TryHackMe Logo">
</p>

# Windows Threat Detection 3
|  Room Name | Windows Threat Detection 3 |
|----------|-------|
| Author | Dhruv Tripathi |
| Link | [Windows Threat Detection 3](https://tryhackme.com/room/windowsthreatdetection3) |

# Room Information
```bash Type: Walkthrough
Difficulty: Medium
Tags: - 
Meta Tags: Walkthrough, Walk-through, Write-up, Writeup
Subscription type: Premium
Description:
Learn how threat actors manage to maintain access to the breached Windows hosts.
```
## Task 1

### Let's go!

- Answer: `No answer needed`

## Task 2

### Which suspicious archive did the user download?

- We can filter for Sysmon Event ID `15` to monitor the creation of Alternate Data Streams (ADS). In this example, the logs show the creation of a `Zone.Identifier` stream associated with the suspicious file `URGENT!.zip`. The `ZoneId=3` value indicates that the file originated from the Internet zone

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/cab76ed2-eb25-4c18-acba-f81842405612" />
</p>

- Answer: `URGENT!.zip`

### Where did the attackers hide the C2 malware file?

- We can see through Sysmon Event ID `1` that PowerShell executed a malicious command to download the payload via `Invoke-WebRequest` from the external IP address `10.14.97.15`. The log tracks the script saving the file to the hidden `AppData` folder and immediately launching it using `Start-Process`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/4f42962c-00d4-463e-b8b5-d38544f28590" />
</p>

- We can see that the dropped file `update.exe` was successfully executed on the system. The log tracks it running with a `ProcessId` of `3140`, which matches the ID of the malicious PowerShell process that downloaded it

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/6537dd12-1dbc-4907-b599-03a074d0c298" />
</p>

- Answer: `C:\Users\Administrator\AppData\Roaming\update.exe`

### What is the domain of the Command and Control server?

- Filtering for Sysmon Event ID `22`, we can see that the executed malware `update.exe` started a network connection by making a DNS lookup request. The log tracks the program attempting to contact the external domain `route.m365officesync.workers.dev`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/6d749a97-bf58-4dc3-b7b8-4c46a99a00bc" />
</p>

- Answer: `route.m365officesync.workers.dev`
