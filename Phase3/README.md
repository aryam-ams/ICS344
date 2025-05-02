# Phase 3: Defensive Strategy Proposal

## Goal
Implement firewall defenses using `iptables` to protect SSH from brute-force attacks.

---

## 1️⃣ Initial Firewall Status (BEFORE Defense)

Checked current firewall rules:
sudo iptables -L


Findings:
- SSH connections were allowed from anywhere without restrictions.

- Tested attack → attacker successfully connected.

---

## 2️⃣ Defense Implementation: Blocking SSH Brute-Force Attempts

Added `iptables` rules:

1. Allow established connections:
sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT


2. Track new SSH connections:
sudo iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --set


3. Block after 2 attempts in 10 seconds:
sudo iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --update --seconds 10 --hitcount 3 -j DROP


4. Allow SSH if under threshold:
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT


---

## 3️⃣ Verification of Rules (AFTER Defense)

Verified added rules:
sudo iptables -L -n -v --line-numbers

✅ Confirmed tracking and blocking rules were active.

---

## 4️⃣ Attack Attempt AFTER Defense

Ran:
./ssh_attack.sh


Result:
- First 2 login attempts: ✅ allowed
- Third and subsequent: ❌ blocked (connection timed out)

---

## 📝 Conclusion
- Successfully limited SSH login attempts to 2 tries per 10 seconds.
- Attack was blocked after reaching threshold.
- Defense reduced brute-force attack risk while maintaining access for legitimate users.
