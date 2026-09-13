# MITRE ATT&CK Analysis

This section documents how Wazuh maps detected security events to the MITRE ATT&CK framework.  
MITRE ATT&CK provides a standardized way to understand adversary behavior, techniques, and tactics observed during monitoring.

In this lab, repeated authentication failures and password‑guessing behavior were mapped to MITRE techniques, helping classify the activity within a recognized adversary model.

---

## 1. Credential Access (TA0006)

The primary tactic observed in this environment was **Credential Access**, which focuses on techniques attackers use to obtain valid credentials.

### Technique: T1110 – Brute Force

Wazuh mapped repeated failed login attempts to **MITRE Technique T1110 – Brute Force**.

### Evidence: MITRE Password Guessing Technique

![MITRE Password Guessing](../screenshots/15-mitre-password-guessing.png)

This dashboard shows:
- **Technique:** T1110 – Brute Force  
- **Tactic:** Credential Access  
- **Trigger:** Multiple failed authentication attempts  
- **Source:** WordPress VM agent logs  

This confirms that the authentication failures were consistent with adversary password‑guessing behavior.

---

## 2. Initial Access (TA0001)

WPScan probing activity aligns with **Initial Access**, where attackers attempt to gain entry into a system.

Although Wazuh did not directly detect WPScan, the behavior aligns with:
- XML‑RPC authentication attempts  
- Password guessing  
- Application probing  

This supports the MITRE classification of early‑stage adversary activity.

---

## 3. Discovery (TA0007)

Port changes and service enumeration behavior observed during the lab align with **Discovery** tactics.

Examples include:
- New ports opening or closing  
- Service restarts  
- Enumeration attempts during scanning  

These behaviors represent adversaries attempting to learn about the system and its services.

---

## 4. MITRE ATT&CK Tactic Coverage Summary

| MITRE Tactic | Description | Evidence Source |
|--------------|-------------|-----------------|
| **Credential Access (TA0006)** | Attempts to obtain valid credentials | Authentication failures, brute‑force mapping |
| **Initial Access (TA0001)** | Attempts to gain entry into the system | WPScan probing activity |
| **Discovery (TA0007)** | Identifying system information and services | Port changes, enumeration behavior |

---

## 5. Key Takeaways

- MITRE ATT&CK provides a structured way to interpret alerts beyond raw log data.  
- Wazuh successfully mapped authentication failures to **T1110 – Brute Force**.  
- WPScan activity aligns with **Initial Access** and **Credential Access** tactics.  
- Discovery‑related behavior highlights early reconnaissance activity.  
- MITRE mapping enhances SOC investigations by placing events in an adversary lifecycle context.

This MITRE analysis demonstrates how Wazuh enriches alert interpretation by aligning observed behavior with known adversary techniques.
