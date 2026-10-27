<p align="center">
  <img src="https://assets.tryhackme.com/img/logo/tryhackme_logo_full.svg" width="150" alt="TryHackMe Logo">
</p>

# Linux Logging for SOC
|  Room Name | Linux Logging for SOC |
|----------|-------|
| Author | Dhruv Tripathi |
| Link | [Linux Logging for SOC](https://tryhackme.com/room/linuxloggingforsoc) |

# Room Information
```bash Type: Walkthrough
Difficulty: Easy
Tags: - 
Meta Tags: Walkthrough, Walk-through, Write-up, Writeup
Subscription type: Premium
Description:
Explore key Linux log sources and learn how to use them in your SOC triage.
```
## Task 1

### Let's start!

- Answer: `No answer needed`

## Task 2

### Use the /var/log/syslog file on the VM to answer the questions. Which time server domain did the VM contact to sync its time?

- We can first `cd` into the `/var/log` folder and use `grep timesync` to search for domain we need

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/e4f43fd4-25f1-47bb-88cb-e7c0eb4b0da1" />
</p>

- Answer: `ntp.ubuntu.com`

### What is the kernel message from Yama in /var/log/syslog?

- This one was pretty simple as we can use `grep Yama` in the syslog file

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/706e46b2-178d-43cd-bf8d-cc2b81f38d83" />
</p>

- Answer: `Becoming mindful.`

## Task 3

### Continue with the VM and use the /var/log/auth.log file. Which IP address failed to log in on multiple users via SSH?

- To search for failed logins via SSH, we can use `cat auth.log | grep "sshd" | grep -E "Accepted|Failed"`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/f32e7e39-1ab5-4220-867c-6ffcb4bad6bc" />
</p>

- Answer: `10.14.94.82`

### Which user was created and added to the "sudo" group?

- We can search for user creation via `useradd` and the user being added to the group via `usermod` where the command is `grep -E "useradd|usermod" auth.log`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/3394da57-1b3a-4c8c-b664-8ffc8ec493f3" />
</p>

- Answer: `xerxes`
