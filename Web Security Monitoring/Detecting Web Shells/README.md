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

## Task 3
- Access the shell and determine which account you have access to by running the `whoami` command.

- We can access the web shell via browser

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/9d411512-9bdd-403e-a567-8eccac677d0a" />
</p>

- We can type `whoami` in the form and click `Run` and we get the output back

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/ac0c65c3-0a5c-4d2d-8adf-572b1e7f9fcb" />
</p>

- Note that `www-data` is the default name of the web server's account

- Answer: `www-data`

### List the directory contents and find the flag using the ls and cat commands.

- Typing `ls` gets us `flag.txt`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/b7bc2f6b-69b9-49d3-b2fe-7f5282a3c0a0" />
</p>

- Running `cat flag.txt` gets us the flag

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/03e4a453-7a69-42d2-b5fe-838e99fd3569" />
</p>

- Answer: `THM{W3b_Sh3ll_Usag3}`
