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

- To identify the originating workstation, we can look at the preceding Event ID `4624` with Logon Type `3`. Since this event has the same source IP address and occurred just ~3 seconds before the successful RDP logon (Logon Type `10`), it strongly suggests that both events are related. This can occur when Network Level Authentication (NLA) is enabled, as authentication may generate a Type `3` event before the full RDP session is established. We can then check the Type `3` event's Workstation Name field to identify the originating workstation, if recorded

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/f76c6bf3-5692-44f6-9adb-d683af799bf4" />
</p>

- Answer: `DESKTOP-QNBC4UU`
