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

## Investigate the traffic with the default configuration file with ASCII mode. `sudo snort -dev -K ASCII -l .` Execute the traffic generator script and choose "TASK-6 Exercise". Wait until the traffic ends, then stop the Snort instance. Now analyse the output summary and answer the question. `sudo ./traffic-generator.sh` Now, you should have the logs in the current directory. Navigate to folder "145.254.160.237". What is the source port used to connect port 53?

- We can run both commands below

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/1906c85e-833f-40da-a4fc-6f0293a8b2e0" />
</p>

- Note that when I ran `sudo ./traffic-generator.sh`, I selected `TASK-6 Exercise`
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/4b2c4b6c-9dd3-4774-8c7c-2565ed9698a5" />
</p>

- We can see here snort split it up by IP addresses and the one we are interested in is the `145.254.160.237` folder and we can see the source port there
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/c6e21597-3edd-4f74-b42c-fd4b056f479b" />
</p>

- Answer: `3009`

## Use snort.log.1640048004. Read the snort.log file with Snort; what is the IP ID of the 10th packet? `snort -r snort.log.1640048004 -n 10`

- I first navigated into the `TASK-6` folder and then ran `snort -r snort.log.1640048004 -n 10`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/986c09f4-4c17-401f-b30d-14ca96af8e2c" />
</p>

- Scrolling down to the tenth packet, we can see the IP ID
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/bb0fdd3e-92c0-484d-b6f6-5af8778ef6b6" />
</p>

- Answer: `49313`

### Read the "snort.log.1640048004" file with Snort; what is the referer of the 4th packet?

- For this, I ran `snort -r snort.log.1640048004 -n 10 -X` because it would be helpful to display the full packet details and scrolling down to the fourth packet, we can see the referrer
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/4c44be79-dc0f-4d44-b480-b0bb9e27695b" />
</p>

- Answer: `http://www.ethereal.com/development.html`

### Read the "snort.log.1640048004" file with Snort; what is the Ack number of the 8th packet?

- Scrolling down to the eight packet, we can see the ACK number
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/46ea3fed-bdcb-43c1-9407-e396055e0e01" />
</p>

- Answer: `0x38AFFFF3`

### Read the "snort.log.1640048004" file with Snort; what is the number of the "TCP port 80" packets?

- For this one we can use something called a berkeley packet filter (BPF). This filter allows us to tell Snort which packets we want to see
```
snort -r snort.log.1640048004 tcp and port 80
```

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/3cc2a56c-c210-4ad7-9308-a3adfd92d950" />
</p>

- Answer: `41`

## Task 7
## Task 8
## Task 9
## Task 10
