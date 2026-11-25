<p align="center">
  <img src="https://assets.tryhackme.com/img/logo/tryhackme_logo_full.svg" width="150" alt="TryHackMe Logo">
</p>

# ❄️ Snow Trail

| **Information** | **Details** |
|---|---|
| Room | Snow Trail |
| Platform | TryHackMe |
| Event | Advent of Cyber 2026 |
| Type | 🎯 Warmup Challenge |
| Challenge Day | Pre-event |

## Introduction

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/7bd35b90-fc79-4511-98ce-ced367fa2d3d" />
</p>

Before the festive hacking season officially begins, it's time to get warmed up!

Snow Trail is a pre-event room for TryHackMe's Advent of Cyber 2026. It gives participants a chance to sharpen their skills and get into the spirit of things before the main event kicks off on December 1st.

## Solution

- I just got a briefing from my Digital Assistant, letting me know that evidence from a compromised system has been sent to my inbox and tasking me with reading each file's details, picking the right workstation to process them, and uncovering five clues to identify the attacker. Before diving into that first email, the tutorial has me walking over to the hot cocoa station, making a mug, bringing it back to my desk, freeing my hands, and opening up my phone to get settled in

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/002403ef-635f-4c8a-96c1-8a461def80a1" />
</p>

- I just walked over to the hot cocoa station and brewed myself a fresh mug of Hot Cocoa in a festive Christmas tree cup. Next, I need to exit focus mode, pick up the mug, and carry it back to my desk before checking my phone

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/b9d2871a-2faa-480a-ad08-43e59d77917f" />
</p>

- I just sat down at my desk with my hot cocoa and opened my first email for `Task 1: Repair 4k footage`, where I need to repair a massive 4K surveillance video to find the exact time of the breach. Since the file is extremely large, I need to send it to a workstation in the lab that can process it quickly without slowing down

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/7dffec63-850d-4b5a-9c8e-2b9d4ce32ce3" />
</p>

- I clicked `Send to device` and chose the `Workstation` from the device menu, since it's the right machine to handle repairing that massive 4K surveillance footage without slowing down. Now it's time to head over to the desktop and analyze the video for the exact time of the breach

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/4708cffd-11ce-430d-aaad-478e2d21256d" />
</p>

- I walked over to the workstation and opened the video processor app, where the corrupted surveillance footage is loaded and ready to go. Now I'm clicking `Process` to clean up the video so I can find the exact time of the breach

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/1442d49b-fe88-42d7-962b-6cc0a514c73f" />
</p>

- The repair is complete, and we can see a clear shot of a shadowy intruder in the office on `CAM 07 at 2026-12-01 05:43:27`. Now I'm clicking `Add to case file` to lock in our very first clue and move on to the next task

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/4c02e027-f3c3-4fe7-a670-db19124f3673" />
</p>

- With 1/5 Clues found, I opened the next email for `Task 2: Search the network log`, which asks us to find the IP address the hacker connected from in the office network's visitor record, so we can copy the search command and double check which machine we need to run it on

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/818220c9-7e5b-43ab-b197-b3de3a0a2d35" />
</p>

- I checked the devices in the office guide inside the case file to confirm we're using the right machine, and the server is specifically listed as being used for storing shared files and handling network records

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/947e60fb-f596-4c82-bec7-159136bd534a" />
</p>

- I walked over to the server terminal, where the `grep "05:43" /var/log/network.log` search command is queued up to filter the visitor logs around the time of the breach. Now we can click `Paste and Run` to execute the command and pinpoint the attacker's IP address

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/9108fa37-d99a-4549-bf8f-ad5c087f149f" />
</p>

- I ran the search command and the terminal processed the logs, uncovering the `Hacker IP: 197.45.82.16`. Now we can click `Add to case file` to lock in our second clue and move on to Task 3

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/7d9e4230-0c57-4fd7-9f8d-b134c283f31e" />
</p>

- With 2/5 Clues found, I opened the next email for `Task 3: Recover browser profile`, which tells us there's an immovable damaged computer in the meeting room from the breach. To pull the hacker's alias from its evidence files, we need to grab a portable, battery powered Laptop and bring it over to connect to the damaged case

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/71dd7c9e-7b48-4223-a243-352dee886528" />
</p>

- I grabbed the laptop and brought it over to the meeting room table, connecting it directly to the damaged computer case. Now that the `Recovery` app is showing up on the laptop screen, we can open it up and search the evidence files for the hacker's alias

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/9b7c4bcc-9973-4598-b16e-f8a19da95e0b" />
</p>

- I opened the SSD Recovery tool on the laptop, which immediately detected the damaged 512 GB drive from the breached computer. Now we can click `Recover` to extract the data and track down the hacker's alias

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/a492a840-f876-4b61-a30c-36f91e0b9c04" />
</p>

- The SSD recovery finished and shows Recovery complete on the 512 GB drive. Now we can click `Open folder` to dig through the recovered browser profile files and uncover the hacker's alias

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/80f22f36-1ed5-45e1-8ad1-7a28c166ba55" />
</p>

- I opened the recovered `evidence_alias.txt` file, which reveals the suspect's profile and uncovers the `Hacker Alias: GBies`. Now we can click `Add to case file` to lock in our third clue and move on to Task 4

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/fcf32bbb-424a-4072-84c0-709de5b543ec" />
</p>

- With 3/5 Clues found, I opened the next email for `Task 4: Restore evidence image`, which includes a scrambled image file that needs to be rebuilt to reveal where it was taken

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/1bb489f5-1397-4dbe-8cb3-023b883856cd" />
</p>

- After checking the case file to confirm which machine is built for rebuilding recovered image files, we can click `Send to device` to route it over to the desktop

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/8d6b3265-f51e-4580-bc6b-027b05c69216" />
</p>

- I walked over to the desktop and ran the I`mage Rebuilder tool`, which finished unscrambling the photo to reveal a map location pinned right on `Wareville`. Now we can click `Add to case file` to lock in our fourth clue and move on to the final task

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/1684b948-e3cf-4623-a2e3-293fe589d304" />
</p>

- With 4/5 Clues found, I opened the final email for `Task 5: Scan QR code`, which mentions a QR code sticker recovered from the breach scene is attached to the physical case file on my desk. We can click `Open camera` on my phone so we can head over to the desk, scan it, and uncover the hacker's machine serial number

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/a43f66c7-4196-4c23-ac6b-f32c0844c5e4" />
</p>

- Uh oh... scanning that QR code was a trap as my Digital Assistant just hopped on speaker to warn me that the last email was actually sent by the hacker, who has now hijacked most of the office devices over the network. Now the mission has shifted to 0/3 devices disconnected, where I need to track down the three Wi-Fi connected IoT devices in the office (without confusing them with offline embedded devices) and disconnect them before the hacker can do any more damage

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/36e1a885-d729-402f-8015-d404a120a523" />
</p>

- I checked the Devices in the Office guide inside the case file and narrowed down the five remaining appliances on the right to isolate the three network-connected IoT devices which are the Thermostat, Printer, and Smart Speaker while skipping the offline Digital Clock and the Coffee Machine. We can track down those three smart devices around the lab and disconnect them before the hacker can cause any more damage

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/5490f9ea-95f6-4ad1-adcf-fc4984502e49" />
</p>

- I tracked down our first target which was the smart Thermostat mounted on the wall and tapped the Wi-Fi icon to pull up the red `DISCONNECT` button. Now I'm hitting disconnect to knock it off the network for 1/3 devices disconnected before hunting down the Printer and Smart Speaker

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/0baa635e-8219-4c4b-89a1-eadd3d7cc08d" />
</p>

- I tracked down our second target which was the network-connected Printer and clicked `DISCONNECT`. Now that I've hit disconnect to knock it offline for 2/3 devices disconnected, let's hunt down our final smart device

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/76b15474-7130-44a0-9082-7df8725bf697" />
</p>

- The lab ended before I could get a screenshot here but I tracked down our third and final target which was the snowman Smart Speaker sitting next to the cocoa machine and clicked `DISCONNECT` to disconnect it from the network to hit 3/3 devices disconnected. With all three IoT devices safely offline and the attacker cut off from the office network, we finished the lab

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/c3bc6880-7a3a-40ed-873c-d0d9f3277ad0" />
</p>

- The completion screen popped up confirming `Endpoint secured. McSkidy owes you one`, marking the Advent of Cyber 2026 pre-event lab complete

<p align="center">
<img width="90%" height="90%" alt="image" src="https://github.com/user-attachments/assets/dd528074-a4de-4e65-9cf6-8a5d85733d23" />
</p>
