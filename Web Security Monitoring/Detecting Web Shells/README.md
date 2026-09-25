<p align="center">
  <img src="https://assets.tryhackme.com/img/logo/tryhackme_logo_full.svg" width="150" alt="TryHackMe Logo">
</p>

# Detecting Web Shells
|  Room Name | Detecting Web Shells |
|----------|-------|
| Author | Dhruv Tripathi |
| Link | [Detecting Web Shells](https://tryhackme.com/room/detectingwebshells) |

# Room Information
```bash Type: Walkthrough
Difficulty: Easy
Tags: - 
Meta Tags: Walkthrough, Walk-through, Write-up, Writeup
Subscription type: Premium
Description:
Explore web shell detection by analyzing logs, file systems, and network traffic.
```
## Task 1

### I understand the learning objectives and am ready to embark on a web shell adventure.

- Answer: `No answer needed`

## Task 2 
### Which MITRE ATT&CK Persistence sub-technique are web shells associated with?

- I opened up the MITRE ATT&CK Matrix for this task and we can scroll down looking at the `Persistence` column

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/608a58be-b2b0-4b9d-b092-131fe7cc1a38" />
</p>

- Hovering over `Web Shell`, we can see the technique ID

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/57313af2-b244-489f-90db-14a29b7cf2af" />
</p>

- Answer: `T1505.003`

### What file extension is commonly used for web shells targeting Microsoft Exchange?

- In the examples TryHackMe gave us, we can see the file extension commonly used

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/338d005e-676f-4477-905d-32df9c24b34f" />
</p>

- Answer: `.aspx`
