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

### What is the PPID of the suspicious whoami command?

- To search for the PPID of `whoami`, we can use `ausearch -i -x whoami` where `-i` interprets numeric values into human readable text, while `-x` filters audit logs by the executable name `whoami`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/1fb7e7c6-825b-4053-9544-0cfc751612e8" />
</p>

- Answer: `1018`

### Moving up the tree, what is the PID of the TryPingMe app?

- To find the PID of the app, we can move up the process tree until we get to `pid 1` building out a process tree starting with the `whoami` execution under pid `1020`, which was spawned by the shell process running the combined string under pid `1018`, which was spawned  by the parent Python application hosting `main.py` at pid `577`, which itself was directly spawned by the system's root init process at `pid 1`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/a481d354-ba42-4a19-abdc-caad13062769" />
</p>

- Answer: `577`

### Which program did the attacker use to open a reverse shell?

- To find this out we can filter via the command `ausearch -i --ppid 577` where we list all the processes spawned by this main process. Looking through the logs we can see `ppid `577 spawning a shell session that executes a Python reverse shell payload under `pid 1029`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/13d75558-8c47-4075-977b-bf2f28ac8d30" />
</p>

- Answer: `Python`

## Task 6

### Which Initial Access technique is likely used if a trusted app suddenly runs malicious commands?

- Attackers compromise a trusted software vendor or application and inject malicious code into a legitimate software update. When users install the update, the malicious code runs on their systems

- Answer: `Supply Chain Compromise`

### Which detection method can you use to detect a variety of Initial Access techniques?

- Defenders monitor the sequence of processes running on a system to identify suspicious parent-child relationships. By analyzing which processes launch other processes and the commands they execute, defenders can detect signs of malicious activity associated with various initial access techniques

- Answer: `Process Tree Analysis`

## Skills Learned

- Analyzing Linux authentication logs to identify successful and failed SSH login attempts
- Detecting SSH brute force attacks and identifying targeted user accounts
- Identifying suspicious IP addresses involved in unauthorized access
- Investigating command injection attempts through system logs
- Using audit logs and `ausearch` to investigate suspicious process execution
- Understanding PID and PPID relationships to trace process trees
- Identifying suspicious child processes spawned by legitimate applications
- Understanding supply chain compromise as an initial access technique
- Using process tree analysis to detect suspicious behavior and potential intrusions

## Conclusion

This room provided hands-on experience with Linux threat detection by investigating authentication and audit logs to identify suspicious activity. I learned how to recognize SSH brute force attacks, trace unauthorized access, investigate command injection, and follow process relationships to identify malicious commands and reverse shell activity. Overall, this room improved my understanding of Linux log analysis and how defenders can use process tree analysis and system monitoring to detect potential compromises and respond to threats effectively
