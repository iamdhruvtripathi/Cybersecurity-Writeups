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
