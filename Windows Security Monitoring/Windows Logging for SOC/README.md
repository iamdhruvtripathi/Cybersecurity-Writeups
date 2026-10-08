<p align="center">
  <img src="https://assets.tryhackme.com/img/logo/tryhackme_logo_full.svg" width="150" alt="TryHackMe Logo">
</p>

# Windows Logging for SOC
|  Room Name | Windows Logging for SOC |
|----------|-------|
| Author | Dhruv Tripathi |
| Link | [Windows Logging for SOC](https://tryhackme.com/room/windowsloggingforsoc) |

# Room Information
```bash Type: Walkthrough
Difficulty: Easy
Tags: - 
Meta Tags: Walkthrough, Walk-through, Write-up, Writeup
Subscription type: Premium
Description:
Start your Windows monitoring journey by learning how to use system logs to detect threats.
```
## Task 1

### I'm ready to move on!

- Answer: `No answer needed`

## Task 2

### Looking at the last screenshot, which event ID describes a successful login? (Answer format: LogSource / ID, e.g. Application / 8194)

- TryHackMe gave a [page](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/) to visit and we can see that Event ID `4624` means a successful login

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/8a550fd3-db6e-42b8-8393-8aea0e96a6da" />
</p>

- We know that the login information is stored in the `Security` folder

- Answer: `Security / 4624`

## Task 3

### Open the "Practice-Security.evtx" file on the VM's Desktop. Which IP performed a brute force of the THM-PC?

- We can click on `Filter Current Log...` and, knowing that we're looking for brute force attempts against THM-PC, we should expect to see a large number of failed login attempts, indicated by Event ID `4625`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/9cb678a4-cd5a-4558-a6fb-b0be65738da7" />
</p>

- Clicking on one of the logs, we can see the `Source Network Address` under `Network Information`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/efa136ef-8b1f-4572-91f2-fadef17e4b46" />
</p>

- Answer: `10.10.53.248`

### Which user has been breached as a result of the attack?

- If a user has been compromised, we would expect to see a successful logon associated with that account, indicated by Windows Event ID `4624`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/f1c91f3e-cb9f-439e-85c6-2c0f7f920214" />
</p>

- Here, we look for `Logon Type 10`, which usually means the user logged in through RDP. This can show that the attacker successfully logged into the system using the compromised account. Note that by correlation of the timeline, we saw a burst of failed authentication attempts (Event ID `4625`) originating from the malicious IP address `10.10.53.248` from the last question. The continuous failures lasted right up until the latest attempt at `10:53:30` PM. We know that just a couple of seconds later, at `10:53:41` PM, the attacker got a successful connection (Event ID `4624`) occurs using `Logon Type 10` (Remote Desktop Protocol). Looking at the New Logon details for this specific successful event, the targeted account name is identified

### What was the Logon ID of the malicious RDP login? Note: The login you are looking for has a Logon Type 10.

- The Logon ID is underneath the `Account Domain`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/b0e84706-2350-4f22-b05c-ec9f378619d7" />
</p>

- Answer: `0x183C36D`

## Task 4
### Continue with the "Practice-Security.evtx" file on the VM's Desktop. Which user was created by the attacker soon after the RDP login?

- We know to search for Event ID `4624` and look for `Logon Type 10`, which indicates an RDP/Remote Interactive logon. I noted the Logon ID as `0x183C36D`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/290634f3-0e47-4287-b55f-ed718802d400" />
</p>

- Now, to search for a newly created user account, we can filter for Event ID `4720`. Even though there is only one event here, we can see that the Logon ID matches the previous `4624` event, allowing us to correlate the two events. We can also see the name of the newly created account. Note the timing as well where the account was created a couple of minutes after the login

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/341bf562-1ccd-42ea-82c9-b4efd4d62b00"/> 
</p>

- Answer: `svc_sysrestore`

### Which two privileged groups was the backdoor user added to? (Answer in alphabetical order, e.g. "Administrators, Power Users")

- To search for this, we can filter for Event ID `4732`, which records when a user is added to a security group. Attackers may use this to add an account to a privileged group, such as Administrators, to gain administrator privileges

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/05b38faa-bd4d-4ca5-baa2-4c0c90030724" />
</p>

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/f9399e61-893a-4ec7-a658-de86c2e3b4b8" />
</p>

- Answer: `Backup Operators, Remote Desktop Users`

### Does the Logon ID field match what you saw in the previous task (Yea/Nay)?

- Yes, the Logon ID does match because we found the Logon ID to be `0x183C36D` in both cases where we filtered for Event ID `4624` and Event ID `4720` or `4732`

- Answer: `Yea`

## Task 5

### Open the "Practice-Sysmon.evtx" file on the VM's Desktop. Which web browser does Sarah use to browse the web?

- To search Sysmon for which web browser she was using, there needs to be a web browser process logged. To look for processes, we can filter for Sysmon Event ID `1`, which records process creation events. Sure enough, when we filter for Event ID `1`, we find the web browser process she used

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/d57ffe36-2979-482c-86e0-0ac2e7b0ad39" />
</p>

- Answer: `Google Chrome`

### Which file did Sarah download from the browser?

- Looking at the events, we see one log where Sarah downloaded something and it was here in the `Downloads` folder

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/338b5a50-11ba-4b53-874b-c41042896bf7" />
</p>

- Answer: `C:\Users\sarah.miller\Downloads\ckjg.exe`

### Which URL was the file downloaded from? Note: Use other Sysmon events to find out!

- TryHackMe gave me this [page](https://isc.sans.edu/diary/Sysmon+and+Alternate+Data+Streams/26292.) to visit. The article explained that Sysmon can capture Alternate Data Streams (ADS), including the `Zone.Identifier` stream created when a file is downloaded, which can contain the `HostUrl` and `ReferrerUrl`. `ZoneId=3` means the file came from the Internet. To find the answer, we searched the Sysmon logs for Event ID `15` (`FileCreateStreamHash`), which records information about file streams. We then checked the `Zone.Identifier` information and found the `HostUrl`, which showed where the file was downloaded from and gave us the answer

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/7e766520-a1ca-4d36-ac05-6f18159ec2b0" />
</p>

- Answer: `http://gettsveriff.com/bgj3/ckjg.exe`

## Task 6

### Continue with the "Practice-Sysmon.evtx" file on the VM's Desktop. Which file was created by the downloaded malware to persist on the host?

- To see which process created the file, we can filter Sysmon for Event ID `11`, which tracks file creation and overwriting activity. By reviewing the events, we can identify the malware process that created the `DeleteApp.url` file

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/24725b66-8e89-4876-aef3-3710211561c2" />
</p>

- Answer: `C:\Users\sarah.miller\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\DeleteApp.url`


### What is the Command & Control server malware connected to? (Answer in format IP:Port, e.g. 1.1.1.1:80)

- To find the IP address and port the malware connected to, we can filter for Sysmon Event ID `3`, which records network connections made by processes. We can then check the `DestinationIp` and `DestinationPort` fields to identify the Command & Control (C2) server

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/74581fb9-6b00-401e-9ef3-6e13dbae8835" />
</p>

- Answer: `193.46.217.4:7777`

### Finally, which domain does the malicious IP correspond to?

- To search for DNS queries, we can filter for Event ID `22`. There are technically three domains we could choose from based on the first three events, but we know it’s the first one because it resolves to the same IP address that was identified as the C2 server in the previous task

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/59f0e730-9210-4579-91d8-29cec135939b" />
</p>

- Answer: `hkfasfsafg.click`
