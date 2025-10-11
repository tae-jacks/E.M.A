# E.M.A
Event Monitoring Audit
# 🛡 Windows Event Log Monitoring – Failed Logon Analysis (Event ID 4625)

# Objective
This project demonstrates how to monitor and analyze **Windows Security Event Logs**, specifically focusing on **failed logon attempts (Event ID 4625)**.  
The purpose is to simulate a SOC analyst workflow by detecting suspicious authentication attempts and assessing potential brute-force or unauthorized access activity.

# Tools Used
- **Windows Event Viewer** – Log collection and filtering  
- **PowerShell** – Exporting logs for analysis  
- **Excel / CSV** – Parsing events for reporting  
- **(Future Work)** SIEM integration with Splunk / ELK  

# Event Details (Redacted for Security)
- **Log Name:** Security  
- **Source:** Microsoft Windows Security Auditing  
- **Event ID:** 4625  
- **Task Category:** Logon  
- **Keywords:** Audit Failure  
- **Failure Reason:** Invalid credentials (0xC000006D / 0xC0000380)  
- **Caller Process:** `C:\Windows\System32\svchost.exe`  
- **Source Network Address:** [REDACTED]  
- **Source Port:** 0  

# Executive Summary
During routine log monitoring, multiple failed logon attempts (Event ID 4625) were observed.  
While occasional failures may result from user error, repeated failures within a short timeframe can indicate:  
- **Brute-force attacks**  
- **Unauthorized lateral movement attempts**  
- **Credential stuffing or password spraying**  

# Analysis
- Status codes confirm failed authentication due to invalid credentials.  
- **svchost.exe** is legitimate, but attackers may abuse system processes for logon attempts.  
- The source network address (redacted) requires correlation with firewall/IDS logs to confirm origin.  
- Rapid multiple failures may indicate brute-force behavior. 

# Potential Impact
- **Unauthorized Access Risk:** Malicious actors attempting entry.  
- **Service Disruption:** Repeated failures may lock accounts, affecting legitimate users.  
- **Weak Security Posture:** Indicates possible gaps in lockout policy or monitoring.  

# Recommendations
- **Correlate Logs:** Check firewall/IDS for connections tied to the source address.  
- **Review Authentication Attempts:** Look for Event ID **4624** (successful logons) around the same timeframe.  
- **Account Lockout Policy:** Enforce limits after repeated failed attempts.  
- **User Monitoring:** Validate that no suspicious accounts were created or logged in.  
- **Escalation:** If external or repeated attempts continue, escalate to Tier 2 SOC or Incident Response.  

# Conclusion
Event ID 4625 logs highlight **failed logon attempts due to invalid credentials**.  
While some failures are harmless, repeated or patterned activity may signal a **potential security incident**.  
By correlating **Event ID 4625 (failed)** with **Event ID 4624 (successful)**, SOC analysts can better distinguish between **normal user error** and **malicious attempts**.

# Screenshots
*(All sensitive details redacted)*

![Failed Logon] 
<img width="1483" height="834" alt="Screenshot (6)" src="https://github.com/user-attachments/assets/e697cfaa-ba17-4ebf-878b-9df4597e893c" />
<img width="1920" height="1080" alt="splunk table" src="https://github.com/user-attachments/assets/f1f29a4a-eb66-4a3d-95af-58d6a6bbb9d7" />

---

# References
- [Microsoft Event ID 4625 Documentation](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4625)  
- [MITRE ATT&CK – Valid Accounts](https://attack.mitre.org/techniques/T1078/)  
