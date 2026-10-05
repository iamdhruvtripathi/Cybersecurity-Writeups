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

- Here, we look for `Logon Type 10`, which usually means the user logged in through RDP. This can show that the attacker successfully logged into the system using the compromised account

### What was the Logon ID of the malicious RDP login? Note: The login you are looking for has a Logon Type 10.

- The Logon ID is underneath the `Account Domain`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/b0e84706-2350-4f22-b05c-ec9f378619d7" />
</p>

- Answer: `0x183C36D`
