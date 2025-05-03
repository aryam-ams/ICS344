# Phase 1: Setup and Compromise the Service

## Task 1: Compromising Metasploitable3 via SSH

**Targeted Service:**
- Service: SSH
- Port: 22
- Target: Metasploitable3 VM
- IP Address: 192.168.8.169

**Tools Used:**
- Metasploit Framework (Kali Linux)
- Module: `auxiliary/scanner/ssh/ssh_login`

**Steps:**
1. Launched Metasploit.
   
   ![image](https://github.com/user-attachments/assets/0999886e-b5fd-42f2-b0ff-8038e7f52837)

3. Used the `ssh_login` scanner module.
   
   ![image](https://github.com/user-attachments/assets/76c344e4-3d93-4238-a44e-7ef86b5d34dc)

4. Configured parameters (IP, credentials).
   
   ![image](https://github.com/user-attachments/assets/09971e66-7257-4d6b-92db-04d6475f058a)

6. Ran the exploit.

   ![image](https://github.com/user-attachments/assets/b8f8be1e-904f-46bf-ba52-20db932c5565)


**Outcome:**
Metasploit successfully logged into SSH using `vagrant:vagrant`.
Example output:
 ```bash

[+] 192.168.8.169:22 - Success: 'vagrant:vagrant'
[*] Command shell session 1 opened ...
uid=900(vagrant) gid=900(vagrant) groups=900(vagrant),27(sudo)
Linux metasploitable3-ub1404 3.13.0-170-generic ...
````

**Conclusion:**
This task showed how weak/default credentials (`vagrant:vagrant`) allowed SSH access via Metasploit. It highlights the importance of:
- Changing default passwords.
- Hardening SSH configurations.

---

## Task 2: Compromising SSH with a Custom Script

**Targeted Service:**
- Service: SSH
- Port: 22
- Target IP: 192.168.8.169
- Known credentials: `vagrant:vagrant`

**Tools & Methods:**
- Kali Linux
- Bash Script (`ssh_attack.sh`)
- `sshpass` utility

**Steps:**
1. Created a Bash script to automate SSH login attempts.
   

![image](https://github.com/user-attachments/assets/7a4b7279-f8d8-4d42-9576-1a831d9057fc)

2. Executed the script against the target.

   
   ![image](https://github.com/user-attachments/assets/608a6130-a896-4d6f-ae85-4f90b6e5a080)
   
   ![image](https://github.com/user-attachments/assets/6a716b07-5632-4ee4-bd9e-7f7db3fa245f)




**Outcome:**
The script found valid credentials `vagrant:vagrant` and confirmed access 

Example output:    
````bash
SUCCESS
vagrant
````

**Conclusion:**
This task demonstrated how automated scripts can exploit weak/default credentials. It reinforces the need to:
- Change default credentials immediately.
- Enforce strong passwords.
- Limit SSH login attempts using rate-limiting or MFA.
