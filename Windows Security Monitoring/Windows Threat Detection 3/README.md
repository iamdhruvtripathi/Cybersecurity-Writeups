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

## Task 3

### How many times did the threat actor fail to log in to the Administrator?

- To search for failed logins, we can filter for Windows Event ID `4625`. Below we can see there are `6` failed login attempts corresponding to the `Administrator` account

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/7104b081-414f-4dab-ad20-14f73bd9c02f" />
</p>

- Answer: `6`

### After the successful login, which backdoor user did the attacker create?

- We can see the attacker successfully logged in over the network as detected by Windows Event ID `4624`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/2facb340-d3ff-458f-892c-7bfa605e3d1c" />
</p>

- To search for backdoor accounts created, we can filter for Windows Event ID `4720` (A user account was created)

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/724dc4cb-7e7c-478a-92ce-fa6465f5d46d" />
</p>

- Answer: `support`

### Which privileged group was the backdoor user added to?

- For this we can filter for Windows Event ID `4732` to identify which group the backdoor account was added to

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/736a0d09-f943-4ffd-ad7b-277c98b0eb2f" />
</p>

- Answer: `Administrators`

## Task 4

### Which Windows service was created to persist the Nessie malware?

- To search for suspicious Windows services installed, we can filter for Windows Event ID `4697` which logs service installations (creations)

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/7344d35d-4a5a-4022-aae7-096e2523678c" />
</p>

- Answer: `Data Protection Service`

### Which scheduled task was created to persist the Troy malware?

- To detect suspicious scheduled task creation, we can filter for Windows Security Event ID `4698` which logs when a new scheduled task is created

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/5d695942-bc2b-4916-b3e6-754df3fa24c8" />
</p>

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/13fe6313-ee58-45e4-a92e-4d9ec8b2912e" />
</p>

- Answer: `AmazonSync`

### What flag do you get after finding and running the Troy malware?

- We can navigate to the path that was in the `<Command>`. I went to `Local Disk (C:)` > `Program Files` > `Common Files`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/8da4ff6d-be78-49fb-a33f-5547752ea8f4" />
</p>

- However we need to find the parent command line first to get the flag

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/5b2f8e22-ee91-40a7-a5ed-85a6c2c6bf7d" />
</p>

- To find the parent command line we can take a look at Sysmon Event ID `1` as it records process creation events. While standard Windows Security logs might just show a process started, Sysmon Event ID `1` shows extra, more detailed info by showing fields like `ParentImage`, `ParentProcessId`, `ParentCommandLine`, etc.

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/aa454b7e-151f-4464-bf0f-4e473a49583a" />
</p>

- Entering the parent command line, we get the flag

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/dfe2d8c6-03a6-48a3-9a7c-f793a49c0ec6" />
</p>

- Answer: `THM{c2_is_on_schedule!}`

## Task 5

### What is the parent process image of the "Odin" malware?

- We can go to the `Sysmon (After Reboot)` logs and filter for Sysmon Event ID `1` as it records when processes are launched showing detailed information such as `ParentImage`, `ParentCommandLine`, etc. Then, we can check the `ParentImage` field to identify which program launched the `Odin` malware


<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/ea2a8026-c021-494a-ae2e-5aec22a73011" />
</p>

- Answer: `C:\Windows\explorer.exe`

### What is the last line that the "Odin" malware outputs?

- I navigated to where the file was located using the path in the screenshot above

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/b29992e1-3752-41b0-b40a-b9701bf70561" />
</p>

- However, I tried clicking and running the file but it opened and closed really fast so I couldn't properly see the last line. However, we can search for this process launch in the logs via filtering for Sysmon Event ID `1`. The log shows the command prints text to mimic a bad script. First, it displays `Doing bad stuff...` and loops 10 times to print random numbers. Finally, it prints `Done doing bad stuff!` right before closing

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/0cf29394-a03b-4768-8555-f8b91bc0e674" />
</p>

- Answer: `Done doing bad stuff!`

### What flag do you get after finding and running the "Kitten" malware?

- The `Kitten` malware is located here

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/96964615-0658-4a10-baa6-7a5539aede95" />
</p>

- However, we first have to answer the question before we can get the flag

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/bb48fabb-3840-45db-a5c5-936d0641c19e" />
</p>

- We can filter for Sysmon Event ID `13` as it tracks any creation/modification of run keys in the `Sysmon (Before Reboot)` logs and we see the value created. The log shows a new value named `Basket` was added to the Windows run persistence key. This key points directly to an executable file located at `C:\Users\Public\kitten.exe`. This registry change ensures the program automatically runs whenever the user logs on

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/645b308a-2db4-4338-b317-6e78bdfe9e2c" />
</p>

- Typing the value name in, we get the flag

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/49351d66-f937-4855-a8b0-a4e573933464" />
</p>

- Answer: `THM{persisting_in_basket!}`

## Task 6

### What is the biggest threat to most corporate Windows networks?

- Active Directory is important because it connects and manages many systems. If hackers compromise it, they may be able to use that access to cause widespread damage with ransomware

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/f253affc-37a3-4739-91a8-878728c30dda" />
</p>

- Answer: `Ransomware`

### At which stage is it best to detect and stop the attack (e.g. Exfiltration)?

- All complex attacks start from a simple single breach but then slowly turn into a big beach. The best stage to detect and stop an attack is ideally right after initial access

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/22fc01a3-ca58-4738-b170-e0758644e1cd" />
</p>

- Answer: `Initial Access`

## Skills Learned

- Analyzing Sysmon logs to investigate suspicious activity and process execution
- Identifying downloaded malware and Alternate Data Streams (ADS) using Event ID 15
- Tracing malicious PowerShell commands, malware downloads, and C2 connections
- Investigating failed and successful logins using Event IDs 4625 and 4624
- Detecting backdoor accounts and unauthorized group membership changes using Event IDs 4720 and 4732
- Identifying malware persistence through Windows services and scheduled tasks using Event IDs 4697 and 4698
- Analyzing registry Run keys using Event ID 13 to detect persistence mechanisms
- Examining parent processes and command-line arguments using Event ID 1
- Investigating suspicious DNS queries using Event ID 22 to identify potential C2 domains
- Correlating Windows Security and Sysmon logs to reconstruct attack timelines
- Understanding the importance of early threat detection to prevent ransomware attacks

## Conclusion

- This room provided hands-on experience in detecting Windows threats by analyzing Sysmon and Windows Security logs to identify malware execution, suspicious downloads, Command and Control activity, unauthorized account creation, and persistence techniques. It strengthened my understanding of how attackers maintain access to compromised systems and highlighted the importance of early threat detection to prevent further compromise and ransomware attacks
