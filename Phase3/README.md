# Phase 3: Defensive Strategy Proposal

## Goal
Implement firewall defenses using `iptables` to protect SSH from brute-force attacks.

---

## Initial Firewall Status (BEFORE Defense)

1. Checked current firewall rules:
    ```bash
    sudo iptables -L
    ```
    ![image](https://github.com/user-attachments/assets/2570550d-4324-4556-8fa0-faa44318c67f)




2. Findings:
    - SSH connections were allowed from anywhere without restrictions.

3. Tested attack:
   
    ![image](https://github.com/user-attachments/assets/cd30d7e7-95af-40f2-8fb3-8d9873735fc9)
    ![image](https://github.com/user-attachments/assets/8f577856-07bc-4ba2-b2f1-4351ef0e0354)
  
    - attacker successfully connected.
 
---

## Defense Implementation: Blocking SSH Brute-Force Attempts

Added `iptables` rules:

1. Allow established connections:
```bash
sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
```
![image](https://github.com/user-attachments/assets/869bc5d1-b9a8-449b-8cd1-17f79662076e)

2. Track new SSH connections:
```bash
sudo iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --set
```
![image](https://github.com/user-attachments/assets/2763039e-9c7c-4582-96b4-352ad6767690)


3. Block after 2 attempts in 10 seconds:
```bash
sudo iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --update --seconds 10 --hitcount 3 -j DROP
```
![image](https://github.com/user-attachments/assets/3db03e89-e03f-45bd-9936-157be675ac88)


4. Allow SSH if under threshold:
```bash
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```
![image](https://github.com/user-attachments/assets/e09c9c34-a116-40ca-8da1-5ab34e6722de)


---

## Verification of Rules (AFTER Defense)

Verified added rules:
```bash
sudo iptables -L -n -v --line-numbers
```
![image](https://github.com/user-attachments/assets/e3a35610-0c6f-48c1-ab93-389fd37d282a)

 - Confirmed tracking and blocking rules were active.

---

## Attack Attempt AFTER Defense

Ran:
```bash
./ssh_attack.sh
```
![image](https://github.com/user-attachments/assets/709f7ceb-93bf-46f8-ba72-fcfa80545d42)


Result:
- First 2 login attempts: allowed
- Third and subsequent: blocked (connection timed out)

---

## Conclusion
- Successfully limited SSH login attempts to 2 tries per 10 seconds.
- Attack was blocked after reaching threshold.
- Defense reduced brute-force attack risk while maintaining access for legitimate users.
