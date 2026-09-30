<p align="center">
  <img src="https://assets.tryhackme.com/img/logo/tryhackme_logo_full.svg" width="150" alt="TryHackMe Logo">
</p>

# Detecting Web DDoS
|  Room Name | Detecting Web DDoS |
|----------|-------|
| Author | Dhruv Tripathi |
| Link | [Detecting Web DDoS](https://tryhackme.com/room/detectingwebddos) |

# Room Information
```bash Type: Walkthrough
Difficulty: Easy
Tags: - 
Meta Tags: Walkthrough, Walk-through, Write-up, Writeup
Subscription type: Premium
Description:
Explore denial-of-service attacks, detection techniques, and strategies for protection.
```
## Task 1

### I understand the learning objectives and am ready to embark on a Denial-of-Service adventure!

- Answer: `No answer needed`

## Task 2
### What class of attack relies on disrupting the availability of a web service?

- Denial-of-service attacks overwhelm a website/app so that people can not use them. For example, an attacker may send a large number of requests to a website until the server becomes overloaded and stops responding normally

- Answer: `Denial-of-Service`

### What do we call the network of compromised machines that attackers use to launch DDoS attacks?

- Botnets are an army of compromised computers such as IoT devices, computers, servers infected with malware controlled by an attacker and often utilized in DDoS attacks

- Answer: `Botnet`

## Task 3

### Which attacker motive aims to make customers lose confidence in a company?

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/e8843aae-81fd-40ba-b0ed-92b594a14049" />
</p>

- Reputational damage can cause customers to lose trust in a company

- Answer: `Reputational Damage`

### Which motive most likely drove the 2023 DDoS attack against Microsoft?

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/701e91bd-b24a-475e-8595-1c12b8ebb302" />
</p>

- We know it was a hacktivist group

- Answer: `Hacktivism`

## Task 4
### What is the attacker’s IP address?

- Opening `access.log`, we can see that the attacker is rapidly sending numerous HTTP `GET /login` requests utilizing curl to automate the attack and we can see the IP address associated with those requests

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/4d6e109a-3cf8-4c2b-8891-4db07ddf9359" />
</p>

- Answer: `203.12.23.195`

### Which page is repeatedly targeted by the attacker’s requests?

- The page being targeted is listed after `GET`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/289968a8-698d-4fb4-a60c-2eecc2056f88" />
</p>

- Answer: `/login`

### After the attack, what error code do legitimate users receive?

- We can see here after the attacker executes the attack, the website/server returns a `503` error, meaning it has become unavailable

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/f3d7dd45-c751-4c18-86a4-bd9446ad83d2" />
</p>

- Answer: `503`
