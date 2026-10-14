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

### Looking at Sysmon logs, what is the first command the invoice.pdf.exe executes?

- We can go to the `Task 3` folder and run the `invoice.pdf.exe` binary

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/96c34b32-9388-4b60-97e8-fdabfa9e1e03" />
</p>

- We can filter for Sysmon Event ID `1` since we're looking for process creation events. Most of these discovery commands run as standalone processes, so Event ID `1` is the easiest way to catch them all in action

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/ff5525db-e860-4c76-93bf-4c43a10a564d" />
</p>

- Scrolling down we can see the that this log captures the initial execution of the malware, showing `invoice.pdf.exe` launching at `3:23:40 AM` with a unique `ProcessId` of `3392`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/c608e855-80f1-4e09-b007-b17e39e283ab" />
</p>

- Below, this log captures `whoami.exe` running as the very first discovery command spawned by the malware at `3:23:41 AM`. By looking at the details pane, we can verify it is directly tied to the initial infection because its ParentProcessId is `3392`, which matches the `ProcessId` of the `invoice.pdf.exe` process that ran earlier

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/efa0e496-92c1-47d4-9767-c46c8de3bf87" />
</p>

- Answer: `whoami`

### Which command did the malware use to check the presence of MS Defender EDR?

- Going through the logs we find the command used to check the presence of MS Defender EDR

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/162448ff-7752-4e7d-a41b-967b5efa28ef" />
</p>

- Answer: `cmd /c "tasklist /v | findstr MsSense.exe || echo No MS Defender EDR"`

### To which domain did the malware send the discovered data?

- We can filter for Sysmon Event ID `22` since it captures DNS queries. This lets us see exactly what external domains the malware is trying to communicate with or exfiltrate data to

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/af7f970e-6a68-429c-92ca-a6a545b0a0d3" />
</p>

- Answer: `exfil.beecz.cafe`
