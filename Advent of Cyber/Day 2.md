# Day 2
## Challenge Walkthrough
### Summary of the Process:

The task involves investigating suspicious activity using **Elastic Security Information and Event Management (SIEM)**. The investigation begins by identifying suspicious behavior flagged by security alerts, such as failed login attempts and encoded commands. We set a specific time frame (e.g., December 1st, 2024, between 9:00 and 9:30 AM) in Elastic's "Discover" dashboard to filter events. Using filters, they focus on details like usernames (e.g., `service admin`), event categories (e.g., authentication), and source IP addresses. These steps reveal a series of failed login attempts, indicating potential brute-force activity.

For Further analysis we extend the timeline to find the attack's origin. By removing irrelevant filters, the team identifies an external source IP (`10.0.255.1`) responsible for multiple failed login attempts. These events suggest a **password-spraying attack**, where an attacker systematically tries numerous password combinations against one account. The attacker gains access to a default `service admin` account and executes an encoded PowerShell command across multiple systems. By decoding the Base64-encoded command using CyberChef, we discover the command's intent: installing Windows updates.

This process highlights the importance of **threat hunting** in cybersecurity. It showcases how attackers exploit weak default credentials and tools like PowerShell to execute remote commands. Brute force attacks, especially password spraying, are common techniques used to compromise accounts. Organizations use SIEM tools like Elastic to detect, analyze, and respond to such threats by correlating logs and filtering suspicious activity. The task reveals that the attack's intent (installing updates) was a non-malicious attempt to save the world.

## Gallery 
![Screenshot (215)](https://github.com/user-attachments/assets/5d5ee4d3-91f3-4200-8f05-6a620eea12b8)
![Screenshot (227)](https://github.com/user-attachments/assets/1d4608d3-4acd-4afe-ab00-ff873a0093e7)
![Screenshot (225)](https://github.com/user-attachments/assets/4e58a1ca-7790-411d-b98e-7b6da61a28a5)
![Screenshot (224)](https://github.com/user-attachments/assets/4ebbbcf4-0680-45a4-aa9f-6e1c2db4ec97)
![Screenshot (222)](https://github.com/user-attachments/assets/03459d98-509f-4b62-8cd2-dd9518d0e429)
![Screenshot (219)](https://github.com/user-attachments/assets/412e283b-e7b2-4663-97f4-5b26e7fe98df)
![Screenshot (216)](https://github.com/user-attachments/assets/37cc819c-5e4b-42f0-818a-daf204a9ab43)
![Screenshot (228)](https://github.com/user-attachments/assets/f71db7c2-6949-432d-a999-ddd391ad4e4b)

The Final Answers that led us to completing these Tasks:

![Screenshot (229)](https://github.com/user-attachments/assets/1d036dad-374a-487f-a9f9-a70d567fbf9f)

