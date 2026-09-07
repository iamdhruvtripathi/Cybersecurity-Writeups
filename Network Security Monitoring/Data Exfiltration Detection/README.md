<p align="center">
  <img src="https://assets.tryhackme.com/img/logo/tryhackme_logo_full.svg" width="150" alt="TryHackMe Logo">
</p>

# Data Exfiltration Detection
|  Room Name | Data Exfiltration Detection |
|----------|-------|
| Author | Dhruv Tripathi |
| Link | [Data Exfiltration Detection](https://tryhackme.com/room/dataexfildetection) |

# Room Information
```bash Type: Walkthrough
Difficulty: Medium
Tags: - 
Meta Tags: Walkthrough, Walk-through, Write-up, Writeup
Subscription type: Premium
Description:
Learn how to detect data exfiltration attempts in various network channels.
```
## Task 1

### Continue to the next task.

- Answer: `No answer needed`

## Task 2

### Connect with the lab.

- Answer: `No answer needed`

## Task 3
### Exfiltrating the data through HTTP comes under which technique?

- We can see which row exfiltrating data under HTTP comes under

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/37c88f94-6dad-4f63-ab08-ddbb48ca1454" />
</p>

- Answer: `Network-based`

## Task 4

### What is the suspicious domain receiving the DNS traffic?

- Using Wireshark, we can see a large number of suspicious DNS queries being sent to this particular domain. Furthermore, we use the filter below because malware may sometimes send DNS queries to nonexistent or unreachable domains, which can be an indicator of suspicious activity
```
dns && dns.flags.response == 0
```
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/f7ef7160-88a2-45dd-b558-05da410f4966" />
</p>

- Answer: `tunnelcorp.net`

### How many suspicious traffic/logs related to dns tunneling were observed?
- In Wireshark, since we know that the DNS queries are long, we can search for long queries specifically. We can then see the total number of displayed packets
```
dns && frame.len > 70
```
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/a3b592fc-06f9-49bb-be8b-5d8c0239a960" />
</p>

- Answer: `315`

### Which local IP sent the maximum number of suspicious requests?

- We can use Splunk to filter for this IP. However, we need to be careful because we need to remember that not all requests sent by these IP addresses are suspicious.  That's why I specified the length because other requests may be shorter

```
index="data_exfil" sourcetype="DNS_logs" | where len(query) > 30
```

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/38628d2e-6ca4-4d1b-8688-00e8dccecf67" />
</p>

- Answer: `192.168.1.103`

## Task 5

### How many connections were observed from the guest account?
- I scrolled down until I found the guest accounts
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/803bbf54-cca3-404c-b6b2-5c6e6461bc68" />
</p>

- Then, we can apply the `USER guest\r\n` as a filter
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/152f885d-69f6-40b2-a425-0e66d9909540" />
</p>

- We can now see how many guest accounts there are in total
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/d7eb697f-afea-4a43-9bc5-fd4a13c3b74f" />
</p>

- Answer: `5`

### Apply the filter; what is the name of the customer-related file exfiltrated from the root account?

- We can do the same thing here as the last question and apply a filter on `USER root\r\n`

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/f02952b4-1d60-4227-ba0e-9ae87f280755" />
</p>

- Hovering over the first packet, we see the file name

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/01fe7481-f536-4b23-927d-3ed9e8456f8e" />
</p>

- Answer: `customer_data.xlsx`

### Which internal IP was found to be sending the largest payload to an external IP?

- For this one, we can search for length of the frame greater than `90`. Looking at the filtered packets, we can see the largest length with the `USER` as `guest` and the associated IP address
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/8229378f-3ab9-4919-bffa-893db1db5e57" />
</p>

- Answer: `192.168.1.105`

### What is the flag hidden inside the ftp stream transferring the CSV file to the suspicious IP?

- We can follow the `TCP stream` and see the flag

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/ea08de20-bf01-4a5e-a28e-5b23806f1724" />
</p>

- Answer: `THM{ftp_exfil_hidden_flag}`

## Task 6
### Which internal compromised host was used to exfiltrate this sensitive data?

- Using the query, we can see this was the only internal host which had the largest payload size
```
index="data_exfil" sourcetype="http_logs" method=POST bytes_sent > 600 | table _time src_ip uri domain dst_ip bytes_sent | sort - bytes_sent
```
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/09ed0e12-a9e3-4346-9410-e7e2db30846c" />
</p>

- Answer: `192.168.1.103`

### What's the flag hidden inside the exfiltrated data?

- We can use Wireshark to find the flag. Here, we can search for frame length greater than `600`. We notice it is the same exact source and destination IP and uploading to the same place
```
http.request.method == "POST" and frame.len > 600
```

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/1d7cfb95-74bc-4f20-97d0-e1acd00c0d0c" />
</p>

- Following the `TCP Stream`, we get the flag
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/b9e7c757-9c1d-400e-bd8b-6e8b9f435634" />
</p>

- Answer: `THM{http_raw_3xf1ltr4t10n_succ3ss}`

### What is the flag found in the exfiltrated data through ICMP?

- We can search for large frame sizes and we can see the flag in one of the packets
<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/8d3df107-a2ba-4b34-bc5b-b238c20b1746" />
</p>

- Answer: `THM{1cmp_3ch0_3xf1ltr4t10n_succ3ss}`

## Skills Learned
- dentified signs of data exfiltration across different network protocols
- Analyzed suspicious DNS traffic and recognized potential DNS tunneling activity
- Investigated long and repeated DNS queries using Wireshark filters
- Applied Splunk queries to narrow down suspicious network activity and identify compromised hosts
- Correlated source IPs, destination IPs, and payload sizes to detect unusual traffic patterns
- Examined FTP traffic and followed TCP streams to uncover transferred files and hidden data
- Detected suspicious HTTP POST requests associated with large data transfers
- Investigated ICMP traffic for signs of data exfiltration
- Extracted hidden flags and information from network streams using Wireshark
- Distinguished between legitimate network traffic and potentially malicious activity based on traffic characteristics
- Identified suspicious hosts by analyzing unusually large payloads and repeated network requests
- Used packet size and protocol-specific filters to narrow down potentially malicious traffic

## Conclusion

This room provided hands-on experience with detecting data exfiltration through different network channels such as DNS, FTP, HTTP, and ICMP. Throughout the room, I analyzed network traffic with Wireshark, used Splunk to investigate suspicious logs, identified compromised internal hosts, and extracted hidden information from network streams. Overall, this room strengthened my ability to investigate suspicious network activity and recognize different techniques attackers can use to exfiltrate sensitive data
