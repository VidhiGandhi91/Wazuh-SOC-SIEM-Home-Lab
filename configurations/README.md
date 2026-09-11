# Wazuh & Agent Configuration

This section documents the core configurations applied to the Wazuh Manager, Wazuh Dashboard, and the Bitnami WordPress VM agent.  
These configurations establish secure communication, enable log collection, and prepare the environment for detection, investigations, and MITRE ATT&CK mapping.

---

## Wazuh Manager Configuration

The Wazuh Manager was configured to:

- Accept agent registrations
- Manage agent keys
- Apply default and custom rulesets
- Enable vulnerability detection modules
- Provide dashboard access for monitoring and analysis

### Wazuh Dashboard (Manager Overview)

![Wazuh Dashboard](../screenshots/09-wazuh-dashboard.png)

The dashboard provides visibility into:

- Agent status  
- Security events  
- Vulnerabilities  
- MITRE ATT&CK classifications  
- System health  

---

## Agent Registration & Connectivity

The Bitnami WordPress VM was configured as a Wazuh agent.  
Key steps included:

- Generating an agent key on the Wazuh Manager  
- Registering the agent using the manager’s IP  
- Verifying secure communication  
- Confirming active status in the dashboard

### Agent Installation

![Agent Installation](../screenshots/10-agent-installation.png)

### Agent Active Status

![Agent Active](../screenshots/11-agent-control-active.png)

Once active, the agent began forwarding:

- Authentication logs  
- System activity logs  
- Package inventory (for CVE detection)  
- Additional logs configured later in the project  

---

## Log Collection Configuration

The default Wazuh agent configuration enables:

- `/var/log/auth.log`  
- `/var/log/syslog`  
- Package inventory  
- OS security events  

These logs support:

- Authentication monitoring  
- Password guessing detection  
- Vulnerability assessment  
- MITRE ATT&CK mapping  

Additional log sources (e.g., Apache logs for WordPress) can be added in future enhancements.

---

## Security Modules Enabled

The following Wazuh modules were enabled and verified:

### ✔ Vulnerability Detector  
Collects package inventory and matches versions against CVE databases.

### ✔ System Audit  
Monitors OS-level security events.

### ✔ Threat Hunting  
Correlates logs with rules to generate alerts.

### ✔ MITRE ATT&CK  
Maps detected events to adversary techniques.

These modules form the foundation for the detection and investigation capabilities documented in later sections.

---

## Summary

This configuration module establishes the operational baseline of the SOC/SIEM environment:

- Wazuh Manager fully configured  
- Dashboard accessible and functional  
- Agent installed, registered, and actively forwarding logs  
- Core security modules enabled  
- Log collection ready for detection and investigations  

These configurations ensure that subsequent detection, vulnerability management, and MITRE ATT&CK mapping operate reliably across the environment.
