Great, I see what the issue is. Your `README.md` is currently being **rendered as a code block**, which happens when you wrap the entire content in triple backticks (` ``` `). This makes it look like one big chunk of code instead of a properly formatted Markdown document.

---

### ✅ Fix: Remove the Backticks Around the Whole Document

**Incorrect:**
```markdown
```markdown
# Header
## Subheader
- List
```
```

**Correct:**
```markdown
# Header
## Subheader
- List
```

---

### ✅ Here's the Properly Rendered Version Without Code Block Wrapping

You can copy and paste this directly into your `README.md` file:

```markdown
# Phase 2: Visual Analysis with a SIEM Dashboard

## Task: Detecting and Visualizing SSH Brute-force Attacks via Splunk

---

### Environment Setup

- **Attacker VM**: Kali Linux  
- **Target VM**: Metasploitable3  
- **SIEM Tool**: Splunk Enterprise  

---

### Tools Used

- **Splunk Enterprise (SIEM)**
- **Splunk Forwarder**
- **/var/log/auth.log** (log file)
- **SSH brute-force simulation**

---

### Steps

#### 1. Install Splunk Enterprise on Kali (Attacker VM)
- Access the Splunk Web UI:  
  `http://<SIEM_IP>:8000`  
- Login as `admin`.

#### 2. Enable Receiving on Port 9997 in Splunk

#### 3. Install Splunk Forwarder on Metasploitable3

#### 4. Connect the Forwarder to Splunk Server

```bash
sudo /opt/splunkforwarder/bin/splunk list forward-server
```

#### 5. Monitor the SSH Log File

```bash
sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/auth.log
```

#### 6. Simulate SSH Brute-force Attack

#### 7. View Logs in Splunk

- Go to: `http://localhost:8000`
- Navigate:  
  `Search & Reporting > Data Summary > Hosts > metasploitable3 > /var/log/auth.log`

##### Search Queries

```spl
index=* source="/var/log/auth.log" "Failed password"
```

```spl
index=* source="/var/log/auth.log" "Accepted password"
```

---

### Visualization and Analysis

- Created bar charts to visualize SSH login attempts.
- Identified brute-force behavior clearly via Splunk.

---

### Outcome

- Splunk successfully collected logs from Metasploitable3.
- SSH attack data was easy to identify.
- Dashboards improved visibility and response.

---

### Conclusion

Using Splunk as a SIEM tool enabled us to:
- Detect SSH brute-force attacks in real-time
- Centralize and analyze logs effectively
- Enhance incident response capabilities
```

---

Would you like me to create a downloadable `.md` file version of this for convenience?
