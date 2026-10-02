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

## Task 5
### What was the most frequently requested `uri`?

- We can type `index=main` to pull up all the logs. Then, under `Interesting Fields`, I noticed the `uri` field. We can click on it to see the most frequently requested URIs

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/8195c166-97d5-4925-bc43-4e692f70ea85" />
</p>

- Answer: `/search`

### Which `clientip` made the most requests to the target `uri`?

- We can search in the logs for `/search` since that was the most frequently requested URI

```
index=main uri="/search"
```

- Clicking on `clientip`, we can see the IP that made the most requests

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/167cb1ab-4b33-436e-bb1f-8cd2e5d4c4b7" />
</p>

- Answer: `203.0.113.7`

### How many IP addresses were part of the botnet that attacked your website?

- Since we know our website was under a DDoS attack, we expect to see lots of different IP addresses sending requests. We can look at the IP addresses that made requests to `/search` and see how many there were next to `clientip`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/b8d115d8-e5d9-40bc-8765-bf8f3179513a" />
</p>

- Answer: `60`

### Which `useragent` was most commonly used by the attacking traffic?

- Clicking on the `useragent` field, we can see the top `useragent` used

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/9616fe3f-54b3-44c3-98e3-2f2218b6b00a" />
</p>

- Answer: `Java/1.8.0_181`

### Use the `timechart` command to visualize the requests. What is the peak number of requests made per second during the attack?

- We can use `index="main" | timechart span=1s count` to see the peak number of requests made per second. The `timechart` groups the results into one second intervals, while `count` counts the number of requests in each interval, making it easy to identify the highest request rate
  
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/4f23faf1-03dd-4919-8463-cc19c677a356" />
</p>

- Answer: `207`

### Which legitimate (non-attacking) `clientip` received the first `503` response status post-attack?

- Here, we can filter down the results by searching for the status code `503`, the `clientup` is anything that doesn't start with `203` so it was the `10.10.10.0/24` subnet. Lastly, we can sort by `_time` and put it all into a table

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/5ad11414-7b93-4ea3-b266-bf5d14190257" />
</p>

- Answer: `10.10.0.27`

## Task 6

### What type of security challenge blocks bots by asking users to solve a simple puzzle?

- Websites can use challenges (CAPTCHA) to stop automated traffic

- Answer: `CAPTCHA`

### Which CDN feature spreads traffic across multiple servers to prevent overload?

- CDN's can provide load-balancing to make sure traffic is distributed across different servers making sure no single server is overloaded

- Answer: `Load-balancing`
