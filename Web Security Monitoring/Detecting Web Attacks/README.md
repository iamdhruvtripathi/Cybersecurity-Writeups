<p align="center">
  <img src="https://assets.tryhackme.com/img/logo/tryhackme_logo_full.svg" width="150" alt="TryHackMe Logo">
</p>

# Detecting Web Attacks
|  Room Name | Detecting Web Attacks |
|----------|-------|
| Author | Dhruv Tripathi |
| Link | [Detecting Web Attacks](https://tryhackme.com/room/detectingwebattacks) |

# Room Information
```bash Type: Walkthrough
Difficulty: Easy
Tags: - 
Meta Tags: Walkthrough, Walk-through, Write-up, Writeup
Subscription type: Premium
Description:
Explore web attacks and detection methods through log and network traffic analysis.
```
## Task 1

### I understand the learning objectives and am ready to learn about detecting web attacks!

- Answer: `No answer needed`

## Task 2

### What class of attacks relies on exploiting the user's behavior or device?

- Client-side attacks are those that rely on abusing weaknesses in user behavior or on the user's device. These attacks exploit vulnerabilities in browsers/tricking users to perform unsafe actions. These attacks target the client's computers, phone, browser, etc.

- Answer: `Client-Side`

### What is the most common client-side attack?

- One of the most common client-side attack is XSS

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/43a454bb-b74a-46b0-a3bf-c420cf250f2e" />
</p>

- Answer: `XSS`

## Task 3
### What class of attacks relies on exploiting vulnerabilities within web servers?

- Server-side attacks are those that exploit weaknesses within a web server, application's code, or the backend that supports the website/web app. These exploit flaws in server logic, misconfigurations, input handling, etc.

- Answer: `Server-Side`

### Which server-side attack lets attackers abuse forms to dump database contents?

- SQL injection attacks targets the database that sits behind a website and occurs when applications build queries via string concatenation instead of using parameterized queries

- Answer: `SQLi`

## Task 4

### What is the attacker's User-Agent while performing the directory fuzz?

- Accessing `access.log`, we can see in the first couple of lines there is a tool called `FFUF` which is a web fuzzing tool written in Go used to discover hidden files, directories, parameters, and virtual hosts on web servers and this is the `User-agent`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/37380614-cf9b-4155-9f77-de5916f85db3" />
</p>

- Answer: `FFUF v2.1.0`

### What is the name of the page on which the attacker performs a brute-force attack?

- We can see here the attacker is brute forcing `/login.php` via Hydra which performs rapid, automated dictionary and brute-force attacks against network login pages and services in a live setting

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/ddf7bfd1-8319-4724-8859-c6e2291090bc" />
</p>

- Answer: `/login.php`

### What is the complete, decoded (opens in new tab) SQLi payload the attacker uses on the /changeusername.php form?

- After logging in, the attacker now attempts to do an SQL injection presumably in the change username form. We can copy and paste this into Cyberchef as directed

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/d65bbe62-0a75-448b-acfc-dccdaa8663f4" />
</p>

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/cc609983-5151-483b-9671-dcd273129664" />
</p>

- Answer: `%' OR '1'='1`

## Task 5

### What password does the attacker successfully identify in the brute-force attack?

- We know from the last task that when the HTTP status code `302` was returned, the attacker had gotten the password successfully and logged in because they were most likely redirected to the user's dashboard. Knowing that we can directly search for the status code `302` and see the password. Note that I right clicked on the packet and followed the `HTTP Stream`

```
http && http.response.code == 302
```

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/57f49497-04a9-47ca-bfaf-453fcdcb5c61" />
</p>

- Answer: `astrongpassword123`

### What is the flag the attacker found in the database using SQLi?

- For ease, I added the `User-agent` as a column and we can see where the attacker tries an SQL injection

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/390e1140-c42b-4d69-a5c0-107806fd7bf8" />
</p>

- I right clicked on the packet and followed the `HTTP Stream` and we can see the flag present

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/f0acd27c-4db7-4aac-b40f-87e2d771d334" />
</p>

- Answer: `THM{dumped_the_db}`

## Task 6
### What do WAFs inspect and filter?

- WAFs inspect and decide whether to allow a web request or block it entirely based on predefined rules

- Answer: `Web Request`

### Create a custom firewall rule to block any `User-Agent` that matches `"BotTHM"`

- Below, the structure to create a firewall rule is `IF field-name CONTAINS value THEN action`

- Answer: `IF User-Agent CONTAINS "BotTHM" THEN block`
