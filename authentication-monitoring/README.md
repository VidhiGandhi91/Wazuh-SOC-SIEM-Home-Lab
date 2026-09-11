# Authentication Monitoring

This section documents system-level authentication monitoring performed on the Bitnami WordPress virtual machine.  
The goal is to validate Wazuh’s ability to detect failed login attempts, correlate them in the Threat Hunting dashboard, and classify them under relevant MITRE ATT&CK techniques.

---

## Overview

The Bitnami VM is monitored by a Wazuh agent that forwards operating system authentication logs to the Wazuh Manager.  
To test detection capability, multiple incorrect login attempts were intentionally generated on the VM.  
These failures were captured by Wazuh and surfaced as authentication-related security events.

---

## Failed Login Attempts (Bitnami VM)

Multiple incorrect username/password combinations were entered at the Bitnami VM login prompt to simulate unauthorised access attempts.

![Failed Login Attempts](../screenshots/failed-login-attempts.png)

These repeated failures create a clear pattern of suspicious authentication activity that a SIEM should detect.

---

## Detection in Wazuh Threat Hunting

Wazuh successfully ingested and analysed the authentication logs forwarded by the agent.  
The Threat Hunting dashboard displayed multiple events originating from the Bitnami VM, including:

- `authentication failure`
- `login failed`
- repeated invalid credential attempts

![Authentication Failures in Wazuh](../screenshots/auth-failures-threat-hunting.png)

These events confirm that Wazuh is actively monitoring system-level authentication activity.

---

## MITRE ATT&CK Classification

Wazuh mapped the repeated authentication failures to the **Password Guessing** technique under the **Credential Access** tactic.

![MITRE Password Guessing](../screenshots/mitre-password-guessing.png)

This classification demonstrates Wazuh’s ability to correlate raw log events with standardised adversary techniques.

---

## Log Source

Authentication events were collected from the Bitnami VM’s system logs, typically located at:
/var/log/auth.log

The Wazuh agent forwards these logs to the manager, where built-in rules identify suspicious authentication patterns.

---

## Summary

This authentication monitoring module demonstrates:

- Real failed login attempts generated on the Bitnami VM  
- Successful ingestion and correlation by Wazuh  
- Clear visibility of authentication failures in the Threat Hunting dashboard  
- Automatic MITRE ATT&CK mapping to Password Guessing  
- Effective baseline monitoring for credential-based attacks  

This forms the foundation for more advanced detection engineering and attack simulation documented in later stages of the project.

