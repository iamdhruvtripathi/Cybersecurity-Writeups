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

## Task 3
### When did the SSH password brute force start? Answer Format: 2023-09-15.

- To find out when the SSH brute force attack started, we can look at the failed SSH login attempts. Assuming the attacker did not guess the correct password on the first try, we can use the multiple failed attempts across different accounts to identify when the attack began

```
cat /var/log/auth.log | grep sshd | grep "Failed"
```

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/00c23934-dbe8-432f-8767-cf5f3e06fc14" />
</p>

- Answer: `2025-08-21`

### Which four users did the botnet attempt to breach? Answer Format: Separate by a comma, in alphabetical order.

- We can see the four different accounts the botnet attempted to breach

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/77b9d4ed-6e12-4312-b16e-58b4bcc2b7ff" />
</p>

- Answer: `root, roy, sol, user`

### Finally, which IP managed to breach the root user?

- To look for successful SSH logins, we can filter via `cat /var/log/auth.log | grep sshd | grep "Accepted"`. Looking through the logs, we can see the one that says `Accepted password for root` and the IP address next to it

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/3c4cf420-51b4-484b-9a0c-4e7d6ddc8fb3" />
</p>

- Answer: `91.224.92.79`

## Task 4

### What is the path to the Python file the attacker attempted to open?

- We can see here evidence of command injection and at the bottom what python file the attacker tried to access

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/629b8580-237d-41a1-87c5-f215bbad3958" />
</p>

- Answer: `/opt/trypingme/main.py`

### Looking inside the opened file, what's the flag you see there?

- We can navigate to `/opt/trypingme/main.py` to get the flag

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/c68ce197-7f41-4c67-a49d-f23fb3b3c910" />
</p>

- Answer: `THM{i_am_vulnerable!}`
