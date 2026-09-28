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
### Access the shell and determine which account you have access to by running the `whoami` command.

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

## Task 4
### What is the part of the URL that associates values to parameters and can be a valuable indicator of web shell activity?

- Query strings can be suspicious as information such as commands can be added to the end of the URL and or it can also be encoded

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/f7a69765-2635-42f4-a5b7-0b887af7011a" />
</p>

- Answer: `query strings`

### What auditd syscall would confirm that a file was written to disk following a suspicious POST request to `/upload.php`?

- An example such as `creat /uploads/webshell.php user=www-data` can tell us that the web server actually created the file

- Answer: `creat`

### What command would you use to locate `.php` files in the `/var/www/` directory?

- Using the command below, we are looking inside `/var/www/` and all its subfolders, and looking at every file that ends in `.php.`. Note that `/var/www/` is a common place for web application files, so it can contain a web shell if a server has been compromised

- Answer: `find /var/www/ -type f -name "*.php"`

### Which Wireshark filter would you use to search specifically for `PUT` requests?

- The below command can be used to upload a web shell

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/a20bebd3-75b0-4a34-b536-295ca09085bf" />
</p>

- Answer: `http.request.method == "PUT"`

## Task 6
### Which IP address likely belongs to the attacker?

- I first navigated to `/var/log/apache2` and used `cat access.log | grep 404` to look for files or directories the attacker was trying to access that did not exist. The repeated requests may show that the attacker was searching for a place to upload or run a web shell. We can see dozens of repeated `GET` requests with `404` status codes. On the left, we can also see the IP address associated with the requests

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/8e9e1be2-e40d-46e9-a3f9-56209812a27f" />
</p>

- Answer: `203.0.113.66`

### What is the first directory that the attacker successfully identifies?

- Knowing that the attacker is searching for pages/directories that exist, we know it must return a `200` HTTP status response code and we can see it returned `200` for one particular page

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/e511ad54-93e1-4050-a458-def090b8979a" />
</p>

- Answer: `/wordpress`

###  What is the name of the `.php` file the attacker uses to upload the web shell?

- The attacker uses a `POST` request to upload the web shell. Knowing this, we can search for `POST` requests specifically via `grep POST`. We can see the attacker uploaded `shadyshell.php` and the specific page it was uploaded on

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/3a894f88-f7ed-4759-aae8-e996b80c9b32" />
</p>

- Answer: `upload_form.php`

### What is the first command run by the attacker using the newly uploaded web shell?

- Often times keywords such as `cmd` may be included in `GET` requests and so we can use `grep cmd` to filter the output. We can see the first command on the top

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/12ac9199-5926-4818-9352-bacf426a8ab0" />
</p>

- Answer: `whoami`

### After gaining access via the web shell, the attacker uses a command to download a second file onto the server. What is the name of this file?

- We can see the bottom most command where the attacker downloads a secondary file from their remote server onto the victim machine

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/9b12216b-a8b7-4627-b57b-8b06cab899f4" />
</p>

- Answer: `linpeas.sh`

### The attacker has hidden a secret within the web shell. Use `cat` to investigate the web shell code and find the flag.

- We know the web shell was uploaded in `wordpress/wp-content/uploads`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/e51d79e9-7b71-446b-8fa5-9f6f1148419d" />
</p>

- Since we know where the web shell is, we can just navigate to that directory and look inside the web shell to find the hidden flag

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/3deb15a7-2ffd-4867-8de9-42a3678be739" />
</p>

- Answer: `THM{W3b_Sh3ll_Int3rnals}`
Got it — those should be described as concepts learned rather than hands-on skills

 ## Skills Learned

- Recognized common web shell file extensions such as `.aspx` and `.php`
- Used commands such as `whoami`, `ls`, and `cat` to investigate a web shell
- Analyzed Apache access logs to identify suspicious activity and attacker IP addresses
- Used HTTP status codes to identify successful directory discovery
- Used `grep` to filter logs for suspicious HTTP requests and commands
- Identified suspicious `POST` requests used to upload web shells
- Used `find` to locate potentially malicious PHP files within web directories
- Learned how auditd syscalls such as `creat` can help confirm files being written to disk
- Learned how Wireshark filters such as `http.request.method == "PUT"` can be used to identify suspicious HTTP requests
- Traced attacker activity from initial reconnaissance through web shell deployment
- Identified commands executed through a compromised web shell
- Identified the use of `linpeas.sh` after web shell access was established
- Inspected web shell source code to locate hidden information and flags

## Conclusion

- This room provided practical experience with detecting and investigating web shells using web server logs, file system analysis, and command line tools. I learned how attackers can discover accessible directories, upload a web shell, execute commands, and download additional tools after gaining access to a server. The room also introduced how auditd and Wireshark can be used to support web shell investigations by identifying file creation activity and suspicious HTTP requests, although these were mainly covered through theory in this room. Overall, I gained a better understanding of how to trace web shell activity and identify signs of compromise from both logs and the file system
