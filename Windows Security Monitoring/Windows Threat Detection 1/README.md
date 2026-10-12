<p align="center">
  <img src="https://assets.tryhackme.com/img/logo/tryhackme_logo_full.svg" width="150" alt="TryHackMe Logo">
</p>

# Windows Threat Detection 1
|  Room Name | Windows Threat Detection 1 |
|----------|-------|
| Author | Dhruv Tripathi |
| Link | [Windows Threat Detection 1](https://tryhackme.com/room/windowsthreatdetection1) |

# Room Information
```bash Type: Walkthrough
Difficulty: Medium
Tags: - 
Meta Tags: Walkthrough, Walk-through, Write-up, Writeup
Subscription type: Premium
Description:
Explore common Initial Access methods on Windows and learn how to detect them.
```
## Task 1

### Let's begin!

- Answer: `No answer needed`

## Task 2

### Which MITRE technique ID describes Initial Access via a vulnerable mail server?

- This technique ID describes exploiting a vulnerability in an internet facing application, such as a vulnerable mail server to gain initial access to a network

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/ecc4db80-d336-4254-944c-27bd90d63c77" />
</p>

- Answer: `T1190`

### Which Initial Access method relies on a user opening a malicious email attachment?

- This is known as phishing, where an attacker tricks a user into opening a malicious email attachment. The attachment may install malware or give the attacker unauthorized access to the system

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/fb2eb120-8403-4990-8310-07fae7b4dbbb" />
</p>

- Answer: `Phishing`

## Task 3

### Which user seems to be most actively brute-forced by botnets?

- Botnets typically attempt to log in using many different passwords, resulting in numerous failed logon events recorded as Event ID `4625`
  
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/90f26135-5d54-490a-b2a8-d384264f9647" />
</p>

- We can see that password guesses were made just seconds apart, indicating automated activity rather than manual attempts. Furthermore, after reviewing the logs, I found numerous attempts targeting the `ADMINISTRATOR` account, each using a different password

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/2f0fbfef-869e-4b7f-9948-2078ba87b152" />
</p>

- Answer: `Administrator`

### Which IP managed to breach the host via RDP (Logon Type 10)?

- A successful Windows logon is recorded as Security Event ID `4624`. We can filter the logs for this event and examine the Logon Type field. Logon Type `10` indicates a RemoteInteractive logon, typically associated with RDP. By identifying the relevant event and examining its `Source Network Address` field, we can determine the IP address associated with the successful RDP login

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/dffc301d-172c-42a9-afa3-22e07923e086" />
</p>

- Answer: `203.205.34.107`

### Can you get the real Workstation Name (hostname) of the threat actor?

- To identify the originating workstation, we can look at the preceding Event ID `4624` with Logon Type `3`. Since this event has the same source IP address and occurred just ~3 seconds before the successful RDP logon (Logon Type `10`), it strongly suggests that both events are related. This can occur when Network Level Authentication (NLA) is enabled, as authentication may generate a Type `3` event before the full RDP session is established. We can then check the Type `3` event's `Workstation Name` field to identify the originating workstation, if recorded

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/f76c6bf3-5692-44f6-9adb-d683af799bf4" />
</p>

- Answer: `DESKTOP-QNBC4UU`

## Task 4

### Let's play the role of the untrained user and mindlessly open the COM file. Run the www.skype.com file from the Phishing Case 1 folder, which flag do you get?

- We can click on this `COM` file as if we were a untrained user

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/bee31365-b78a-4a2e-beab-3c65c724fbf5" />
</p>

- It opened command prompt and now we got our flag

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/121b0a8b-6973-443a-bbf7-e19f3806b1eb" />
</p>

- Answer: `THM{misleading_extension}`

### Continue with the second attachment from the Phishing Case 2 folder. From which URL does the malicious LNK download the next stage malware?

- First thing we need to do is extract the zip file and once we do that, we can click on the `New Store PC!` folder

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/2b364b8f-b5c6-4195-a358-ee12119077ea" />
</p>

- In the folder we can see a `.png` file and then the malicious `.lnk` file and right-clicking it and then selecting `Properties` we can see the URL in the `Target` field

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/cc82c943-5c44-4bf5-b18e-26eb4dd6d9dd" />
</p>

- Answer: `http://wp16.hqywlqpa.thm:8000/cgi-bin/f`

### Finally, move on to the Phishing Case 3 folder and review its content. What is the name of the double-extension file you see there?

- We can see the file at the top

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/7182414e-e3cf-41c6-bb56-d8556dde5ee1" />
</p>

- Answer: `best-cat.jpg.exe`

## Task 5

### Which file did the user download via the web browser?

- We can search for potentially downloaded files using Sysmon Event ID `11` (FileCreate), which records file creation and overwrite events that may indicate when new files are saved to the system

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/08af5ca4-8cc3-4d9c-baf8-233e7c17150f" />
</p>

- Here, we can see that the Sysmon Event `11` log shows that Microsoft Edge (`msedge.exe`) initiated a file creation for `top-cats.zip` in the user's `Downloads` folder, while the appended `:Zone.Identifier` Alternate Data Stream (ADS) means the file originated from the internet by triggering the Windows Mark of the Web

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/065e8230-6b2c-4561-a2cc-b237f4d4cfae" />
</p>

- We can even go one step further and look at Sysmon Event ID `15` (File stream created) in the log viewer and see that this file was indeed downloaded from the Internet because of the `ZoneId=3` part under the `Contents` section, which specifically indicates the Internet Zone identifier added by Microsoft's Mark-of-the-Web (MOTW) feature

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/469e9e90-e9a4-433f-addb-2e95e86a378a" />
</p>

- Answer: `C:\Users\Administrator\Downloads\top-cats.zip`

### In which folder did the user unarchive the suspicious file?

- I continued filtering for Sysmon Event ID `11` and observed that, just ~15 seconds later, `EXPLORER.exe` (Windows Explorer) extracted the suspicious file `best-cat.jpg.exe` into a different `Pictures` folder. Both events occurred on the same endpoint (`THM-PC`) and were executed under the same user session (`THM-PC\Administrator`)

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/fa625d4d-ae41-4dbb-af2a-bbcdce9c2379" />
</p>

- Answer: `C:\Users\Administrator\Pictures`

### What is the process ID of the launched phishing malware?

- Here we can filter the log for Sysmon Event ID `1` (Process Creation) to find signs of the malicious executable running

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/004bb601-3a92-4060-9e01-7d5058e3aaeb" />
</p>

- We can see here the active process in the `Image` field is `C:\Users\Administrator\Pictures\best-cat.jpg.exe` as the running binary. Furthermore, the `CommandLine:` field shows it ran directly from the `Pictures` folder location and it was executed ~23 seconds after the file was unarchived. Lastly, we can see the process ID in the `ProcessId` field

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/36d0c56f-91de-4461-80ba-930e11df3ba0" />
</p>

- Answer: `5484`

### Finally, which malicious domain did the malware try to connect to?

- For this we can search for Sysmon Event ID `22` as it tracks any DNS queries being made. We can see below that `ProcessId: 5484` and `Image:` both confirm that `best-cat.jpg.exe` is the process that made this request. The malware attempted to look up the domain `rjj.store` which is likely the attacker's C2 server or malicious hosting domain

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/7b6cabb8-5b64-4ab3-8e6a-626e71abd5f7" />
</p>

- Answer: `rjj.store`

## Task 6

### Which USB file was launched by the user?

- We can search for Sysmon Event ID `1`, which details process creation. Here, we can see the specific malicious executable (`.exe`) disguised as a SanDisk folder. Note that it ran directly from the `E:` drive, which is the letter usually assigned to plugged in USB drives

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/3a111c3e-b02e-4ed6-9969-d9857fd225fc" />
</p>

### Which suspicious file did the malware drop to the disk? (Format: full path to the file, e.g. C:\file.txt)

- File creation is tracked by Sysmon Event ID `11`. Here, we can see the file dropped by the malicious executable. The `Image:` line reads `E:\Open Sandisk 4GB USB.exe` (the fake USB program), which created and dropped a new file named `winupdate.exe` into the suspicious `C:\Users\Public\Documents\` directory

<p aign="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/c0fddafe-009f-4f1a-9585-3abff2282b3f" />
</p>

- Answer: `C:\Users\Public\Documents\winupdate.exe`

### To which other USB did the malware propagate? (Format: just the letter, e.g. X:)

- We can see here the malware trying to spread itself where it detected another USB drive was present and copied itself to that new drive and renamed the copy to `Open Data Traveler 32 GB USB.exe`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/c5071d4e-0b61-4b38-9845-1fd34cab3824" />
</p>

- Answer: `F:`
