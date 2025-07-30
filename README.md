# Insider-Threat

## Objective
This work demonstrates the work a Cybersecurity or SOC analyst would do in day to day tasks. The Insider Threat project is aimed to simulate a digital forensics investigation using a disk image from an insider's workstation. This project shows malicious behavior, credential dumping, privilege escalation, lateral movement, and data exfiltration. The goal is to identify the OS, the tools used, the method of attack, and the insider's intentions and targets. 

### Skills Learned

- Identifying Linux distrubiton and system configuration via kernel logs
- Extracting cryptographic hashes (MD5/SHA1) of log files
- Interperting .bash_history to trace user actions, including downloads and script execution
- Identifying filesystem artifacts that point to secret files and attack tools
- Correlating authenitication logs (auth.log) to user identity, timestamp, and privilege escalation events
- Using metadata and evidence artifacts to connect insider access to external targets

### Tools Used

- FTK Imager to navigate the disk image to access file systems and logs and artifacts
- Bash history to trace executed commands
- System logs used to look at authentication events
- Hashing tools
- Binwalk used to analyze a suspicious image files for embedded executeables

## Step 1
I opened the simulated lab in FTK Imager to explore the file system structure. I navigated to the syslog file and found the /var/log/installer to confirm that Kali Linux is being used.

![Step 1 - Insider Threat](https://github.com/user-attachments/assets/84624e9b-c4d9-4528-a583-a1534a763aca)
## Step 2
I then located /var/log/apache2/access.log and exported the has list. I then inspected the ouput of the hash.

![Step 2 - Insider Threat](https://github.com/user-attachments/assets/4e5bcc9b-25f4-4e02-8476-577f32418e94)
## Step 3
Next I browsed over to /root/Downloads which contains mimikatz_trump.zip, which confirms that a credential dumping tool was downloaded.

![Step 3 - Insider Threat](https://github.com/user-attachments/assets/460032d8-ccbe-479b-8fb3-2bc229f9140a)
## Step 4
Next, I examined /root/.bash_history to see the commands. This includes the command touch snky snky > /root/Desktop/SuperSecretFile.txt that captures the absolute file path.

![Step 4 - Insider Threat](https://github.com/user-attachments/assets/5d8c97f8-f06a-4be0-8059-7892ab814d75)
## Step 5
I stayed in .bash_history to locate binwalk didyouthinkwemakeiteasy.jpg that indicates an embedded file analysis.

![Step 5 - Insider Threat](https://github.com/user-attachments/assets/09ebccad-3127-4437-80cd-eb0783afa610)
## Step 6
I navigated to /root/Desktop and located a checklist file that revealed the insider's goals with this attack, which was profit. 

![Step 6 - Insider Threat](https://github.com/user-attachments/assets/13973ded-9d5b-4007-98ae-cc4f5be1c2c6)
## Step 7
Next, I looked at the access.log which is an empty file and determined that the apache did not run at all.

![Step 7 - Insider Threat](https://github.com/user-attachments/assets/51443229-7e14-4a58-bcc3-ca646cee88fd)
## Step 8
In the root directory, I noticed irZLAohL.jpeg screenshot showing another user's desktop. This shows remote access and possible lateral movement.

![Step 8 - Insider Threat](https://github.com/user-attachments/assets/6a506ce3-3618-400c-8059-4253fffffee9)
## Step 9
Next, I wanted to find who was taunted in the bash script. In /root/Documents/myfirsthack/firstscript_fixed, the script echo statements revealed the name Young as the target being taunted.

![Step 9 - Insider Threat](https://github.com/user-attachments/assets/909a42f6-ea47-4cb4-9e7e-e5e04176ab46)
## Step 10
Next, I wanted to inspect the authentication logs and searched the timestamps at 11:26 and find that the user postgres used the su command multiple times.

![Step 10 - Insider Threat](https://github.com/user-attachments/assets/ed18c4f9-077a-4984-9df1-a191b7d7f954)
## Step 11
This last step determines the current working directory and confirms the correct insider threat.

![Step 11 - Insider Threat](https://github.com/user-attachments/assets/36891781-b775-4bf9-81b0-ff6f22440a90)

