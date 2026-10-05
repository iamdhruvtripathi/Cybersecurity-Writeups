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

- 
