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
2. Used the `ssh_login` scanner module.
3. Configured parameters (IP, credentials).
4. Ran the exploit.

**Outcome:**
Metasploit successfully logged into SSH using `vagrant:vagrant`.

Example output:
[+] 192.168.8.169:22 - Success: 'vagrant:vagrant'
[*] Command shell session 1 opened ...
uid=900(vagrant) gid=900(vagrant) groups=900(vagrant),27(sudo)
Linux metasploitable3-ub1404 3.13.0-170-generic ...


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
2. Executed the script against the target.

**Outcome:**
The script found valid credentials `vagrant:vagrant` and confirmed access by running `whoami`.

Example output:
SUCCESS
vagrant


**Conclusion:**
This task demonstrated how automated scripts can exploit weak/default credentials. It reinforces the need to:
- Change default credentials immediately.
- Enforce strong passwords.
- Limit SSH login attempts using rate-limiting or MFA.
