<p align="center">
  <img src="https://assets.tryhackme.com/img/logo/tryhackme_logo_full.svg" width="150" alt="TryHackMe Logo">
</p>

# Snort
| Room Name | Snort |
|----------|-------|
| Author | Dhruv Tripathi |
| Link | [Snort](https://tryhackme.com/room/snort) |

# Room Information
```bash Type: Walkthrough
Difficulty: Medium
Tags: - 
Meta Tags: Walkthrough, Walk-through, Write-up, Writeup
Subscription type: Premium
Description:
Learn how to use Snort to detect real-time threats, analyse recorded traffic files and identify anomalies.
```
## Task 1

### Read the task above.

- Answer: `No answer needed`

## Task 2

### Navigate to the Task-Exercises folder and run the command "./.easy.sh" and write the output

- Navigating to the terminal, we can type `./.easy.sh` to get the answer

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/26f4be1d-4e36-4a2d-b5b4-d9c143e57c25" />
</p>

- Answer: `Too Easy!`

## Task 3

### Which IDS or IPS type can help you stop the threats on a local machine?

- It is a `HIPS` or `Host-based Intrusion Prevention System` that can help stop threats on a local machine
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/0a56510f-3855-4aaa-8433-0187bfeee7f7" />
</p>

- Answer: `HIPS`

### Which IDS or IPS type can help you detect threats on a local network?

- It is a `NIDS` or `Network-based Intrustion Detection System` that can help us detect threats on a local network

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/2c478c24-5536-4e76-8313-839b57bfb136" />
</p>

- Answer: `NIDS`

### Which IDS or IPS type can help you detect the threats on a local machine?

- It is a `HIDS` or `Host-based Intrustion Detection System` that can help us detect threats on a local machine

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/d3ea187e-7535-4ee8-9917-5ebbb593e3c5" />
</p>

- Answer: `HIDS`

### Which IDS or IPS type can help you stop the threats on a local network?

- It is a `NIPS` or `Network-based Intrustion Prevention System` that can help us stop threats on a local network

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/e68a3437-1fb9-413c-b984-dda23d7b44c2" />
</p>

- Answer: `NIPS`

### Which described solution works by detecting anomalies in the network?

- A `Behavior based IPS` monitors network traffic protecting an entire subnet and if an anomaly is identified, the connection is terminated

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/31e78997-58a8-44d3-a970-5c1969253904" />
</p>

- Answer: `NBA`

### According to the official description of the snort, what kind of NIPS is it?

- We can see the description below

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/88007c6e-11a3-4053-b6e6-cf70745450bb" />
</p>

- Answer: `full-blown`

### NBA training period is also known as ...

- `Behavior-based IPS` requires training to learn the baseline of what normal traffic looks like and how it can differentiate from malicious traffic

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/9beb4cbc-7c12-447a-8739-ae8644e12b55" />
</p>

- Answer: `baselining`

## Task 4
### Run the Snort instance and check the build number.

- Running `snort -V`, we can see the build number

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/f76a6149-6d65-483e-9f68-adefba7e1059" />
</p>

- Answer: `149`

### Test the current instance with "/etc/snort/snort.conf" file and check how many rules are loaded with the current build.

- We can test the current instance with `snort -c /etc/snort/snort.conf -T` and we can see the number of rules loaded

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/96450d4b-5839-4963-a95f-a21adfb19ae9" />
</p>

- Answer: `4151`

### Test the current instance with "/etc/snort/snortv2.conf" file and check how many rules are loaded with the current build.

- Running `snort -c /etc/snort/snortv2.conf -T` gives us the number of rules

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/554eb830-7c05-47e5-b48c-a924af0ee874" />
</p>

- Answer: `1`

## Task 5

### You can practice the parameter combinations by using the traffic-generator script.
- Answer: `No answer needed`

## Task 6



## Task 7
## Task 8
## Task 9
## Task 10
