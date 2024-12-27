# DAY 1 

## Challenge Overview

The Instructions were concise, clear and to the point so I had no problem finishing the Challenge. For Incorrect Tangents and Clarifications I used the Help of the AI Bot here called `echo`. 

Our investigation into the YouTube to MP3 converter site uncovered serious risks disguised behind its clean design. Downloading files from the site revealed a suspicious `.lnk` file posing as an MP3. Using ExifTool, we found that it executed a malicious PowerShell command to disable security restrictions, download a remote script, and steal sensitive data like cryptocurrency wallets and browser credentials from Windows systems. The downloaded script even included a signature: "Created by the one and only M.M."

This signature became a critical clue. By searching for it on GitHub, we found repositories and issue discussions tied to the attacker. One issue thread had comments from a user named MM, who openly discussed modifying the malicious code. This careless reuse of their handle and public discussion made it easy to link their GitHub activity to the attack, exposing their involvement.

This is a classic example of poor OPSEC (Operational Security), which refers to the practices used to protect sensitive information and avoid leaving a trail that could reveal your identity. MM made common OPSEC mistakes like reusing identifiers and posting publicly, similar to real-world cases where attackers exposed themselves through predictable habits or carelessness. It’s a reminder that even the smallest slip-ups can unravel elaborate schemes and lead to accountability.The commands introduced and used here were  :

```bash
unzip
file
exiftool
```
The Link provided to us was: https://raw.githubusercontent.com/MM-WarevilleTHM/IS/refs/heads/main/IS.ps1

## Walkthrough 

Here were the Highlights of the Challenge and also the Images of the Answers to the Questions asked in the Task. 
![Screenshot (199)](https://github.com/user-attachments/assets/2497dd8d-e6d6-4d26-9d18-b55b4e1d0701)
![Screenshot (200)](https://github.com/user-attachments/assets/620376d0-529f-4303-a470-213db728e0e0)
![Screenshot (201)](https://github.com/user-attachments/assets/1e7c69cf-9995-4a79-8fb8-007ad52b29c5)
![Screenshot (202)](https://github.com/user-attachments/assets/1a38eea0-8d8a-438d-85f7-3d4386ff67a5)
![Screenshot (203)](https://github.com/user-attachments/assets/8c8ed830-7fc4-49cc-b594-917501697171)
![Screenshot (204)](https://github.com/user-attachments/assets/77cf54c8-5fc7-46f1-a2ea-73f53fc96bf3)
![Screenshot (206)](https://github.com/user-attachments/assets/67464993-3c9e-40db-9df7-6eac607313d2)
![Screenshot (209)](https://github.com/user-attachments/assets/488ed4ec-41f5-4be7-8b18-82743f0f20b6)....

Proof of the Completed Challenge :
![Screenshot (211)](https://github.com/user-attachments/assets/538e232b-f2b6-445b-97dc-0086a3a32bf8)
