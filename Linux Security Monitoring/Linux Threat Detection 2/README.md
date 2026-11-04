<p align="center">
  <img src="https://assets.tryhackme.com/img/logo/tryhackme_logo_full.svg" width="150" alt="TryHackMe Logo">
</p>

# Linux Threat Detection 2
|  Room Name | Linux Threat Detection 2 |
|----------|-------|
| Author | Dhruv Tripathi |
| Link | [Linux Threat Detection 2](https://tryhackme.com/room/linuxthreatdetection2) |

# Room Information
```bash Type: Walkthrough
Difficulty: Medium  
Tags: - 
Meta Tags: Walkthrough, Walk-through, Write-up, Writeup
Subscription type: Premium
Description:
Explore the first actions of attackers after breaching a Linux server and learn how to detect them.
```
## Task 1

### I'm ready to learn!

- Answer: `No answer needed`

## Task 2

### Run `systemd-detect-virt` to detect the system's cloud. What is the command's output you discovered?

- `systemd-detect-virt` is a tool that detects whether Linux is running on physical hardware, a virtual machine, or inside a container. The output below means Linux has detected that it's running in an Amazon Web Services (AWS) virtualized environment, typically an EC2 instance

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/868bc10e-e674-4548-85ed-c4f412c15e87" />
</p>

- Answer: `Amazon`

### Now run `ps aux` and look for EDR or antivirus processes. What is the full path to the detected antimalware binary?

- We can look for related keywords such as `security`, `scan`, `edr` or `malware`. The full command ran was `ps aux | grep scan`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/b80815f8-e0c9-42c1-82ec-6a3213e2dd80" />
</p>

- Answer: `/var/lib/ultrasec/malscan`
