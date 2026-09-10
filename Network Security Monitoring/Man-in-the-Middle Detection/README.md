<p align="center">
  <img src="https://assets.tryhackme.com/img/logo/tryhackme_logo_full.svg" width="150" alt="TryHackMe Logo">
</p>

# Man-in-the-Middle Detection
| Room Name | Man-in-the-Middle Detection |
|----------|-------|
| Author | Dhruv Tripathi |
| Link | [Man-in-the-Middle Detection](https://tryhackme.com/room/mitmdetection) |

# Room Information
```bash Type: Walkthrough
Difficulty: Easy
Tags: - 
Meta Tags: Walkthrough, Walk-through, Write-up, Writeup
Subscription type: Premium
Description:
Learn what MITM attack is, and how to identify the footprints of this attack in the network traffic.
```
## Task 1

### Continue to the next room.

- Answer: `No answer needed`

## Task 2

### Connect with the lab.

- Answer: `No answer needed`

## Task 3

### How many ARP packets from the gateway MAC Address were observed?

- Knowing the gateway's IP and MAC address, we can use the filter to figure out how many ARP packets there are

```
arp && arp.src.proto_ipv4 == 192.168.10.1 && eth.src == 02:aa:bb:cc:00:01
```

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/c9b41450-085c-4089-841c-999fb891c01f" />
</p>

- Answer: `10`

### What MAC address was used by the attacker to impersonate the gateway?

- Looking here, we can see the attacker starts associating the router's IP address to their MAC address tricking other devices in sending information to them

```
arp.opcode == 2 && arp.src.proto_ipv4 == 192.168.10.1
```

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/18bfb9a4-ba89-48fa-87aa-ab5d70bdaa35" />
</p>

- Answer: `02:fe:fe:fe:55:55`

### How many Gratuitous ARP replies were observed for 192.168.10.1?

- Using the IP address given, we can filter out for gratuitous ARP replies. Note that a gratuitous ARP (GARP) is a unsolicited ARP request or reply sent by a device to announce its own IP address and MAC address mapping to the rest of the local network but no device asked for this information

```
arp.src.proto_ipv4 == 192.168.10.1 &&  arp.isgratuitous
```

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/dbcb0b62-0e0a-45a7-9d18-8eee3d9ea9e5" />
</p>

- Answer: `2`

### How many unique MAC addresses claimed the same IP (192.168.10.1)?

- As we can see, two different MAC addresses claimed the same IP address

 <p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/18ffa3bc-f78b-4882-bb17-98c722b03df1" />
</p>

- Answer: `2`

### How many ARP spoofing packets were observed in total from the attacker?

- We can filter for the duplicated addresses and see how many times the attacker sent these ARP spoofing packets

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/3bb5acab-c39c-44b1-8f2e-21e9c674214b" />
</p>

- Answer: `14`
