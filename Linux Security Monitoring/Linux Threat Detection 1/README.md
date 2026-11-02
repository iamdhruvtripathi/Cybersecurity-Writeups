<p align="center">
  <img src="https://assets.tryhackme.com/img/logo/tryhackme_logo_full.svg" width="150" alt="TryHackMe Logo">
</p>

# Linux Threat Detection 1
|  Room Name | Linux Threat Detection 1 |
|----------|-------|
| Author | Dhruv Tripathi |
| Link | [Linux Threat Detection 1](https://tryhackme.com/room/linuxthreatdetection1) |

# Room Information
```bash Type: Walkthrough
Difficulty: Medium  
Tags: - 
Meta Tags: Walkthrough, Walk-through, Write-up, Writeup
Subscription type: Premium
Description:
Explore how attackers break into Linux systems and how you can detect this in logs.
```
## Task 1

### I'm ready to start!

- Answer: `No answer needed`

## Task 2

### When did the ubuntu user log in via SSH for the first time? Answer Example: 2023-09-16.

- We can filter the authentication logs using `cat /var/log/auth.log | grep "sshd" | grep "Accepted"`, where `cat` displays the contents of the authentication log, the first `grep "sshd"` filters entries related to the SSH service, and the second `grep "Accepted"` displays only successful SSH authentication attempts

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/a7dc19dc-d6d4-4829-99bb-48235ca9d7d5" />
</p>

- Answer: `2024-10-22`

### Did the ubuntu user use SSH keys instead of a password for the above found date? (Yea/Nay)

- We know this to be true because it says `Accepted publickey for ubuntu` instead of `Accepted password`. In Linux logs, `publickey` indicates that SSH keys were utilized for the authentication

- Answer: `Yea`
