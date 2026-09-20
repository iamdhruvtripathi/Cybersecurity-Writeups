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

### Investigate the traffic with the default configuration file with ASCII mode. `sudo snort -dev -K ASCII -l .` Execute the traffic generator script and choose "TASK-6 Exercise". Wait until the traffic ends, then stop the Snort instance. Now analyse the output summary and answer the question. `sudo ./traffic-generator.sh` Now, you should have the logs in the current directory. Navigate to folder "145.254.160.237". What is the source port used to connect port 53?

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

### Use snort.log.1640048004. Read the snort.log file with Snort; what is the IP ID of the 10th packet? `snort -r snort.log.1640048004 -n 10`

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

### Investigate the traffic with the default configuration file. `sudo snort -c /etc/snort/snort.conf -A full -l .` Execute the traffic generator script and choose "TASK-7 Exercise". Wait until the traffic stops, then stop the Snort instance. Now analyse the output summary and answer the question. `sudo ./traffic-generator.sh`What is the number of the detected HTTP GET methods?

- We can run both these commands in separate terminals where in the left terminal, `-A` is alert mode and we want `full` where Snort displays all possible information about the alert

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/dc73d7e5-cb96-4e7e-858f-81baa8a59c43" />
</p>

- Note that I selected `TASK-7 Exercise` to generate the traffic
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/82e9fc33-9860-4b0b-81e2-b50a631e6265" />
</p>

- After clicking `Ctrl + C`, we can see summary and the number of detected HTTP GET methods
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/8bc09b42-7e0f-4abd-9276-7caef9e99bda" />
</p>

- Answer: `2`

### You can practice the rest of the parameters by using the traffic-generator script.

- Answer: `No answer needed`

## Task 8

### Investigate the mx-1.pcap file with the default configuration file. `sudo snort -c /etc/snort/snort.conf -A full -l . -r mx-1.pcap` What is the number of the generated alerts?

- Running `sudo snort -c /etc/snort/snort.conf -A full -l . -r mx-1.pcap`, we can see how many alerts Snort generated under `Action Stats:`
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/09749479-9886-4e74-afb6-95a2e72aa255" />
</p>

- Answer: `170`

### Keep reading the output. How many TCP Segments are Queued?

- We can see how many TCP segments are queued
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/c8ec6159-2ce8-4a78-be0f-cecd00993758" />
</p>

- Answer: `18`

### Keep reading the output.How many "HTTP response headers" were extracted?

- Scrolling down a bit, we can see how many `HTTP response headers` were extracted
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/4ef993fa-35b9-408f-8cd4-e4b5ce0e5517" />
</p>

- Answer: `3`

### Investigate the mx-1.pcap file with the second configuration file. `sudo snort -c /etc/snort/snortv2.conf -A full -l . -r mx-1.pcap` What is the number of the generated alerts?

- Under `Action Stats:`, we can see how many alerts there are
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/1b3009cd-6dcf-4bd4-bb33-bc95b10c9af0" />
</p>

- Answer: `68`

### Investigate the mx-2.pcap file with the default configuration file. `sudo snort -c /etc/snort/snort.conf -A full -l . -r mx-2.pcap` What is the number of the generated alerts?

- We do the same thing here but with a different `.pcap` file

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/65775767-bbdd-4b3e-92e9-6305dfd1ed10" />
</p>

- Answer: `340`

### Keep reading the output. What is the number of the detected TCP packets?

- Under `Breakdown by protocol`, we can see the number of detected TCP packets

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/290e3fbd-18ab-4a24-8056-4ecb91809ca5" />
</p>

- Answer: `82`

### Investigate the mx-2.pcap and mx-3.pcap files with the default configuration file. `sudo snort -c /etc/snort/snort.conf -A full -l . --pcap-list="mx-2.pcap mx-3.pcap"` What is the number of the generated alerts?

- Same thing here but with a different `.pcap` file

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/f0b7bbbb-fbe9-4488-a588-db0f807d5ef9" />
</p>

- Answer: `1020`

## Task 9

### Use "task9.pcap". Write a rule to filter IP ID "35369" and run it against the given pcap file. What is the request name of the detected packet? You may use this command: "snort -c local.rules -A full -l . -r task9.pcap"

- We can edit `local.rules` and add our own rules here. Here, to filter out for a particular IP ID, we can simply add `id:35369`. Note that we have to be in the `TASK-9` folder
```
sudo gedit local.rules 
```
```
alert icmp any any <> any any (msg: "Packet ID 35369 detected"; id:35369; sid:1000001; rev:1;)
```

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/e0a7adcb-d167-43dd-ab45-95354be7755f" />
</p>

- We see that our Snort log file is generated and can read it via `sudo snort -r [file name here]`. At the top, we see only one packet and the request name

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/1cef021b-b37a-49c4-8382-aef1cf76413e" />
</p>

- Answer: `TIMESTAMP REQUEST`

### Clear the previous alert file and comment out the old rules. Create a rule to filter packets with Syn flag and run it against the given pcap file. What is the number of detected packets?

- In the same folder, we can add our own rule here but instead this time we have the `flags:S` where we filter for the `SYN` TCP flag and change `icmp` to `tcp`

```
alert tcp any any <> any any (msg: "SYN flag test"; flags:S; sid: 1000001; rev:1;)
```

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/894aff59-b27b-4918-bc60-68e9ee309ecb" />
</p>

- Reading the Snort log file, we can see there is only a single TCP packet

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/35a1d542-e52f-46a4-9a4e-970fe9da4361" />
</p>

- Answer: `1`

### Clear the previous alert file and comment out the old rules. Write a rule to filter packets with Push-Ack flags and run it against the given pcap file. What is the number of detected packets?

- Here, we do the same thing but instead of just having one flag, we have two and can just put them side by side

```
alert tcp any any <> any any (msg: "PUSH-ACK flag test"; flags:PA; sid: 1000001; rev:1;)
```

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/5340a4c3-d800-4d9a-80a6-0e0f52088ccc" />
</p>

- Once we read the Snort log file, we see how many packets Snort processed

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/e4ea9269-cdee-4231-881c-afbf487a13b0" />
</p>

- Answer: `216`

### Clear the previous alert file and comment out the old rules. Create a rule to filter UDP packets with the same source and destination IP and run it against the given pcap file. What is the number of packets that show the same source and destination address?

- This one was a bit tricky but the idea is to use `sameip` here where we filter the source and destination IP addresses for duplication
```
alert udp any any <> any any (msg: "Same source/destination IP"; sameip; sid: 1000001; rev:1;)
```

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/488b082c-d4d1-4410-b64e-d0c45adf0797" />
</p>

- Reading the Snort log file, we can see how many packets it processed with the same source and destination IP

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/29ae9048-8bfe-4da4-9841-3bb3aa7b639a" />
</p>

- Answer: `7`

### Case Example - An analyst modified an existing rule successfully. Which rule option must the analyst change after the implementation?

- Answer: `rev`

## Task 10

### Read the task above.

- Answer: `No answer needed`

## Skills Learned

## Conclusion
