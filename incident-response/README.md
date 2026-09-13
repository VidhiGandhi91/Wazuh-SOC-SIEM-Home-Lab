# Incident Response

This section documents the incident response workflow performed in the Wazuh SOC/SIEM Home Lab.  
The goal is to demonstrate how alerts were validated, correlated, and acted upon using a structured SOC methodology.

The incident response process followed the standard lifecycle:

1. **Detection**
2. **Analysis**
3. **Containment**
4. **Eradication**
5. **Recovery**
6. **Lessons Learned**

---

## 1. Detection

Wazuh generated multiple alerts related to:

- Authentication failures  
- Password guessing attempts  
- WPScan probing activity  
- Port changes and service behavior  

These alerts were visible through:

- Security Events  
- Threat Hunting  
- MITRE ATT&CK dashboard  

The detection phase confirmed suspicious activity targeting the WordPress server.

---

## 2. Analysis

During analysis, the following observations were made:

### Authentication Failures
Repeated failed login attempts indicated potential brute-force behavior.

### Password Guessing (MITRE T1110)
MITRE mapping confirmed the activity aligned with **Credential Access** tactics.

### WPScan Activity
WPScan probing matched the time window of authentication failures, confirming external enumeration and password guessing attempts.

### Port Changes
Unexpected port changes suggested service enumeration or automated scanning.

### Correlation
All events aligned with early-stage adversary behavior:
- Initial Access  
- Credential Access  
- Discovery  

This validated the presence of a simulated attack scenario.

---

## 3. Containment

Containment actions included:

- Reviewing WordPress authentication logs  
- Verifying no unauthorized access was successful  
- Ensuring XML-RPC remained restricted  
- Monitoring agent activity for escalation attempts  

Since the attack was simulated and unsuccessful, no emergency containment was required.

---

## 4. Eradication

Eradication focused on removing potential attack vectors:

- Disabled unnecessary WordPress plugins  
- Ensured strong passwords were enforced  
- Verified firewall rules  
- Confirmed no malicious processes were running on the WordPress VM  

No persistent threats were found.

---

## 5. Recovery

Recovery actions included:

- Restarting affected services (Apache, SSH)  
- Revalidating Wazuh agent connectivity  
- Confirming normal authentication behavior resumed  
- Ensuring no further brute-force attempts were detected  

The environment returned to a stable state.

---

## 6. Lessons Learned

### ✔ Application-layer logs are essential  
Apache and WordPress logs must be ingested to detect WPScan and web attacks more accurately.

### ✔ Custom Wazuh rules improve detection  
Rules for XML-RPC, login anomalies, and WordPress-specific events would enhance visibility.

### ✔ MITRE mapping strengthens investigations  
Understanding tactics and techniques helps classify alerts into meaningful adversary behavior.

### ✔ Threat Hunting is critical  
Pivoting across events provides deeper insight into attack patterns.

### ✔ Strong authentication controls matter  
Password policies and XML-RPC restrictions significantly reduce brute-force risk.

---

## Summary

This incident response demonstrates a complete SOC workflow:

- Alerts were detected  
- Events were analyzed and correlated  
- Attack behavior was confirmed  
- Environment was secured  
- Improvements were identified  

The response process shows how Wazuh can be used not only for detection, but also for structured incident handling and continuous security improvement.
