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

4. Configured the Required Parameters.
   
   ![image](https://github.com/user-attachments/assets/092bf293-432a-468d-a572-dd31f397a0c0)

**Username file contents:**

![image](https://github.com/user-attachments/assets/9ab13c9f-cd93-48f7-80ee-a6e508f6f233)

**Password file contents:**

![image](https://github.com/user-attachments/assets/70acf21b-11f1-459c-ad62-2eef24e09154)


6. Ran the exploit.
   This initiated a brute-force attempt across all username-password combinations from the provided files.

  ![image](https://github.com/user-attachments/assets/4d28bbb6-a222-4c4a-8176-d437d95bde9c)

Metasploit's scanner/ssh/ssh_login module works asynchronously and non-sequentially:
 It tries multiple username/password combinations at the same time (parallel requests).
As soon as it finds a valid credential, it reports success immediately (even if other attempts are still running).
It does not wait for all failures to print before showing success. Instead, it prints results in the order responses arrive.
 The login attempt for vagrant:vagrant simply completed faster than the others — that’s why success showed up first in output.
Meanwhile, the failed attempts were queued earlier but responded later. 


**Outcome:**
- Metasploit successfully logged in to the SSH service using the credentials vagrant:vagrant.
- An SSH session was opened, confirming access to the system with a valid shell.
- The uid=900(vagrant) and system information were displayed, proving the attack succeeded.


**Conclusion:**
This task demonstrates that systems configured with weak or default SSH credentials are highly vulnerable to brute-force attacks. Using Metasploit's ssh_login module, I was able to automate credential discovery and gain unauthorized SSH access.

This emphasizes the critical need for:
- Changing default credentials
- Implementing strong password policies
- Using SSH key-based authentication
- Applying account lockout mechanisms

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
