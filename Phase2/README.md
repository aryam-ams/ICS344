
# Phase 2: Visual Analysis with a SIEM Dashboard

## Task: Detecting and Visualizing SSH Brute-force Attacks via Splunk

---

### Targeted Scenario:

- **Objective**: Detect SSH brute-force attacks
- **Log Source**: `/var/log/auth.log` on Metasploitable3
- **SIEM Tool**: Splunk Enterprise
- **Attacker Machine**: Kali Linux

---

### Tools Used:

- **Splunk Enterprise** (Kali Linux)
- **Splunk Forwarder** (Metasploitable3)
- **SSH Brute-force Simulation**
- **Splunk Search Queries**

---

### Steps:

1. **Installed Splunk Enterprise** on Kali Linux  
   ![image](https://github.com/user-attachments/assets/bd429e25-9ece-445e-9054-b15f3c1e240e)


2. **Enabled receiving on port 9997 in Splunk**  
   ![image](https://github.com/user-attachments/assets/a079342d-3f21-43c4-872a-083df4ed907b)


3. **Installed Splunk Forwarder on Metasploitable3**  
   ![image](https://github.com/user-attachments/assets/7b51f0c0-ba23-4c81-88b8-d2e3f851a8d5)


4. **Connected the Forwarder to the Splunk Server**  
   ```bash
   sudo /opt/splunkforwarder/bin/splunk add forward-server 192.168.8.170:9997
   ```
   ![image](https://github.com/user-attachments/assets/853deec8-6e3d-4d84-846c-8b68371d1677)

   ```bash
   sudo /opt/splunkforwarder/bin/splunk list forward-server
   ```
   ![image](https://github.com/user-attachments/assets/c34e1944-f620-489d-a819-42c50a23d326)

5. **Monitored the SSH log file on the target**  
   ```bash
   sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/auth.log
   ```
   ![image](https://github.com/user-attachments/assets/20538edc-9ed2-451b-bc43-30425a48039b)


6. **Ran SSH brute-force attack against Metasploitable3**  
   ![image](https://github.com/user-attachments/assets/37f3b4a3-81f4-479c-bdc2-920431dfde00)
   ![image](https://github.com/user-attachments/assets/742fdcfa-fbdb-4e02-bad6-2c0081968c63)


7. **Searched logs in Splunk**:  
   - Open: `http://localhost:8000`
   - Navigate to:
     `Search & Reporting > Data Summary > Hosts > metasploitable3 > /var/log/auth.log`

   Example search queries:
   ```spl
   index=* source="/var/log/auth.log" "Failed password"
   ```
   ![image](https://github.com/user-attachments/assets/82d8d7de-e0cd-417f-bca7-50f96eec3e06)

   ```spl
   index=* source="/var/log/auth.log" "Accepted password"
   ```
   ![image](https://github.com/user-attachments/assets/2343d678-1271-43bf-bb75-661b1d60aeda)

    ```spl
   attack visualization and analysis.
   ```
   ![image](https://github.com/user-attachments/assets/dfcaf9d3-e357-4906-a17b-5268429afffd)

---

### Outcome:

Splunk successfully ingested logs from Metasploitable3. SSH attack patterns such as failed and successful login attempts were clearly visible.

---

### Conclusion:

This task demonstrated how Splunk can effectively:

- Detect brute-force attacks through centralized logging.
- Visualize authentication behavior in real-time.

