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

## Task 4

### According to the VM's package manager logs, which version of unzip was installed on the system?

- To find the installed version of unzip, we can navigate to /var/log/apt, which stores package management history on Debian-based systems. Then, we can run cat history.log | grep -A 3 unzip to search for entries related to unzip, including installation or upgrade details.


<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/314edc8d-6053-467c-bbf4-6d53faab9157" />
</p>

- Answer: `6.0-28ubuntu4.1`

### What is the flag you see in one of the users' bash history?

- To find the flag I looked at the current user's bash history and there was no flag here but I noticed they had switched to the root user via `sudo su` which made me think the flag might be in the root user's bash history

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/aa31a5fc-eb90-409c-babd-4e9d7af51794" />
</p>

- I typed `sudo su` and checked the bash history and found the flag

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/73839dc9-a2b9-4c54-adca-3deebff946ed" />
</p>

- Answer: `THM{note_to_remember}`

## Task 5

### Which Linux system call is commonly used to execute a program?

- This is called the `execve` system call, where the shell hands a program's file path over to the kernel and asks it to take control, allocate memory, and run that tool on the computer's hardware

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/f9780dae-5a55-4615-8dcf-5f80e81de9e3" />
</p>

- Answer: `execve`

### Can a typical program open a file or create a process bypassing system calls? (Yea/Nay)

- A typical program cannot bypass system calls because the hardware strictly prevents it. Only the kernel is allowed to talk directly to your hard drive to open files or manage CPU cores to create processes. The only way a normal program can do these things is by talking to the kernel using a system call

- Answer: `Nay`
