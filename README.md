# Wazuh SOC/SIEM Home Lab

A hands-on Security Operations Center (SOC) / Security Information and Event Management (SIEM) home lab built using **Wazuh, VirtualBox, Ubuntu, and WordPress**.

The project demonstrates endpoint monitoring, security event detection, vulnerability monitoring, attack simulation, alert investigation, and security analysis in an isolated lab environment.

## Lab Architecture

```text
VirtualBox NAT Network
        │
        ├── Ubuntu
        │   └── Wazuh Manager + Dashboard
        │       10.0.3.4
        │
        └── Bitnami WordPress
            └── Wazuh Agent
                10.0.3.5
```

## Objectives

* Deploy and configure Wazuh SIEM
* Monitor a Linux-based endpoint
* Detect authentication failures and password-guessing activity
* Perform controlled WordPress security testing
* Identify vulnerability findings
* Investigate Wazuh security alerts
* Map detected activity to MITRE ATT&CK
* Document detection gaps and improvement opportunities
* Develop a basic SOC investigation and incident-response workflow

## Key Findings

The lab demonstrated successful detection of **system-level authentication activity** through Wazuh.

A controlled WordPress password-guessing test also highlighted an important **application-layer detection gap**: WordPress login activity was not automatically visible through the default Wazuh configuration.

This led to further investigation into log integration and custom detection rules.

## Project Structure

| Folder                            | Description                          |
| --------------------------------- | ------------------------------------ |
| [`architecture`](./architecture/) | Lab architecture and security design |
| [`setup`](./setup/)               | VirtualBox, Wazuh, and agent setup   |
| [`screenshots`](./screenshots/)   | Lab implementation evidence          |

Additional documentation will cover detection engineering, vulnerability management, investigation, MITRE ATT&CK, and incident response.

## Technologies

* **Wazuh**
* **VirtualBox**
* **Ubuntu Linux**
* **Bitnami WordPress**
* **WPScan**
* **MITRE ATT&CK**

## Project Status

**In Progress**

The lab is being expanded with additional detection engineering, investigation, and incident-response scenarios.

## Author

**Vidhi Gandhi**

Master of Information Technology (Cybersecurity)
