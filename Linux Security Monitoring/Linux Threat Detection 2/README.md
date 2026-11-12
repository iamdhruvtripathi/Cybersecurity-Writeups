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

## Task 3
### What is the path of the script that initiated the "hostname" command?

- We can build a mini process tree starting with `ausearch -i -x hostname`. We can see that the process has a `ppid` of `3771`. Next, we can search for that `PID` using `ausearch -i --pid 3771`. Here, we can see that a script named `debug.sh` was executed from the `/home/itsupport` directory

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/12bd9312-b98d-47bb-8b1b-dc4f050986ac" />
</p>

- Answer: `/home/itsupport/debug.sh`

### What was the last Discovery command launched by the script?

- To search for commands launched by this script we can filter via `ausearch -i --ppid 3771`. We can see that the script executed a `ps` command to list running processes, capturing their process ID, parent process ID, full command name, memory usage, and CPU usage, while sorting the results to place the most resource intensive programs at the top of the list

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/ef5cae86-fb03-4ad0-8120-1a8e126925aa" />
</p>

- Answer: `ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu`

### Looking at the script content, what's the email of the script author?

- We know that the script is located at `/home/itsupport/debug.sh`. However, when I initially tried to navigate to the `itsupport` directory using the `cd` command, I encountered a permission denied error. To fix this, I switched to the root user using `sudo su`, navigated to the directory, and used the `cat` command to view the contents of the script

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/28717693-64dc-4bb4-9d14-ccfa9467973c" />
</p>

- Answer: `greg@tryhackme.thm`

## Task 4
### From which domain was the Elastic agent downloaded?

- Attackers can use tools like `wget` or `curl` to download files from the internet. By running `ausearch -i -x wget`, we can search the audit logs and see that the Elastic agent was downloaded from the domain below

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/10bd7a29-8534-46ac-b023-4d016016a57b" />
</p>

- Answer: `artifacts.elastic.co`

### What is the full path to the downloaded "helper.sh" script?

- Similar to the last question, we can search for `curl` commands to identify the full path where `helper.sh` was downloaded, as specified by the `-o` flag

```
ausearch -i -x curl
```

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/dc57326a-219f-484d-9b48-43a641cf7d61" />
</p>

- Answer: `/var/tmp/helper.sh`

### Which of the downloaded files is more likely to be malicious: The one downloaded with curl or wget?

-  In this context, `curl` might be more malicious because attackers commonly use it to download suspicious files or malicious scripts. Here, `curl` may have downloaded a malicious file, while `wget` might have been used to download legitimate software, such as an Elastic Agent

- Answer: `curl`

## Task 5

### Which IP address managed to brute-force the exposed SSH?

- We can use `cat auth.log | grep "Accepted"` to filter for successful SSH authentication attempts. As shown below, one specific IP address appears multiple times, indicating repeated successful logins from the same source IP

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/53c99e3c-511c-4ea4-9a9f-2b1f63979313"/>
</p>

- Answer: `45.9.148.125`

### Which command did the attacker use to list the last logged-in users?

- We know that attackers can use different commands to learn more about a system. One of these commands is `last`, which shows the users who have logged in recently

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/49aa26b1-48ee-406d-91f7-d6a7fa2c3a2d" />
</p>

- Below, we use `ausearch -i -if /home/ubuntu/scenario/audit.log | grep last` to search the audit logs and see where the attacker used the `last` command

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/634f24a1-0d96-4917-bc46-59def554bc89" />
</p>

- Answer: `last`

### Which three EDR processes did the attacker look for with "egrep"? Answer Format: Separated by a comma, in alphabetical order.

- We can see in the `auditd` logs that the attacker used the `egrep` command multiple times to search for specific EDR processes. We can identify the three EDR processes the attacker was looking for

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/6ca6b825-f2b4-4245-9201-b89196f2b024" />
</p>

- Answer: `ds_agent,falcon,sentinel`

## Task 6

### What is the name of the malicious archive that was transferred via SCP?

- We can use `ausearch -i -if /home/ubuntu/scenario/audit.log | grep /tmp` to search for activity involving the `/tmp` directory, since attackers often use it to temporarily store and extract files and this can help us find suspicious file activity. Here, we can see that the attacker used the `tar` command to extract an archive into `/tmp/.apt`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/56c52c0c-dd5c-4631-aa53-03210ec4d6c1" />
</p>

- Answer: `kernupd.tar.gz`

### What was the full command line of the cryptominer launch?

- We can use `ausearch -i -if /home/ubuntu/scenario/audit.log | grep nohup` to search the audit logs for commands containing `nohup`. Attackers often use `nohup` to keep processes running in the background, even after closing the terminal

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/5aa2db77-e19c-490c-87e9-eca377481594" />
</p>

- Answer: `nohup /tmp/.apt/kernupd/kernupd`

### Which IP address range did the attacker scan for an exposed SSH? Answer Example: 10.0.0.1-10.0.0.126.

- We can see in the auditd logs that the attacker used a Bash loop with `nc` (Netcat) to scan multiple IP addresses for an exposed SSH service on port `22`. The command checks each IP address in the range and looks for successful connections, helping the attacker identify systems with SSH accessible

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/23adf9dd-57c7-4041-98a0-c33531c979d0" />
</p>

- Answer: `10.10.12.1-10.10.12.10`
## Skills Learned
- Identifying cloud and virtualization environments using `systemd-detect-virt`
- Enumerating running processes with `ps aux` to identify security tools, EDR agents, and antivirus software
- Analyzing Linux audit logs with ausearch to investigate suspicious commands and trace parent-child process relationships
- Reconstructing process execution chains to identify scripts responsible for launching system commands
- Inspecting shell scripts to identify their contents, authors, and potentially suspicious activity
- Investigating file downloads using `wget`, `curl`, and Linux audit logs
- Analyzing SSH authentication logs to identify successful logins and potential brute-force attacks
- Detecting attacker reconnaissance activities, including user enumeration and EDR process discovery
- Identifying suspicious files and archives transferred through `scp`
- Investigating persistence techniques and background process execution using nohup
- Recognizing cryptomining activity and identifying suspicious binaries running on compromised systems
- Detecting internal network reconnaissance and SSH port scanning using tools such as Netcat

## Conclusion
This room provided hands-on experience investigating post-compromise activities on a Linux system and understanding how attackers operate after gaining initial access. By analyzing authentication logs, auditd events, running processes, and downloaded files, I learned how to reconstruct attacker activity, identify suspicious commands, detect potential security tool discovery and evasion, and recognize malicious activities such as cryptomining and network scanning. Overall, this room strengthened my Linux threat detection and incident investigation skills while demonstrating the importance of properly collecting and analyzing system logs to identify and respond to security threats.
