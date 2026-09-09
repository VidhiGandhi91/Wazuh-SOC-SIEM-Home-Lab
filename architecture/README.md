# SOC/SIEM Home Lab Architecture

## Overview

This home lab demonstrates the design and operation of a small Security Operations Center (SOC) environment using Wazuh as the primary Security Information and Event Management (SIEM) and endpoint security platform.

The lab is designed to simulate a realistic security monitoring environment where endpoint telemetry is collected, analysed, and investigated for suspicious or malicious activity.

## Lab Objectives

The architecture is designed to demonstrate:

* Centralised security event collection
* Endpoint monitoring
* Security event analysis
* Threat detection
* Vulnerability monitoring
* MITRE ATT&CK technique mapping
* Security investigation and alert analysis
* Incident response workflows
* Practical SOC analyst activities

## Core Components

| Component        | Purpose                                                            |
| ---------------- | ------------------------------------------------------------------ |
| Wazuh Manager    | Receives and processes security data from monitored endpoints      |
| Wazuh Indexer    | Stores and indexes security events                                 |
| Wazuh Dashboard  | Provides a web-based interface for monitoring and investigation    |
| Windows Endpoint | Generates Windows security and system telemetry                    |
| Linux Endpoint   | Generates Linux system and security telemetry                      |
| Kali Linux       | Used to simulate controlled security testing and attacker activity |

## Architecture Flow

The general data flow is:

```text
                    ┌──────────────────────┐
                    │    Wazuh Dashboard  │
                    │ Monitoring &        │
                    │ Investigation       │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │    Wazuh Indexer    │
                    │ Event Storage &      │
                    │ Search              │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │    Wazuh Manager     │
                    │ Analysis & Detection │
                    └──────┬───────┬───────┘
                           │       │
                ┌──────────┘       └──────────┐
                ▼                             ▼
       ┌────────────────┐             ┌────────────────┐
       │ Windows        │             │ Linux          │
       │ Endpoint       │             │ Endpoint       │
       │ Wazuh Agent    │             │ Wazuh Agent    │
       └────────────────┘             └────────────────┘

                    ┌────────────────┐
                    │ Kali Linux     │
                    │ Security       │
                    │ Testing        │
                    └────────────────┘
```

> **Note:** The diagram above represents the planned logical architecture. The final architecture diagram will be updated to reflect the actual deployed lab environment.

## Security Monitoring Flow

The monitoring process follows a simplified SOC workflow:

1. Endpoint activity generates system and security events.
2. Wazuh agents collect relevant telemetry from monitored endpoints.
3. Events are forwarded to the Wazuh Manager.
4. The Wazuh Manager analyses the incoming data using configured detection rules and security capabilities.
5. Relevant security events and alerts are indexed for storage and investigation.
6. The Wazuh Dashboard provides visibility into alerts, events, vulnerabilities, and endpoint activity.
7. Detected activity can be investigated and mapped to relevant MITRE ATT&CK techniques.
8. Where appropriate, the investigation can progress into an incident-response workflow.

## Lab Design Principles

The lab follows these principles:

* **Isolation:** Security testing is performed within a controlled virtual environment.
* **Visibility:** Endpoint activity should generate observable telemetry.
* **Detection:** Security events should be converted into meaningful alerts where appropriate.
* **Investigation:** Alerts should provide sufficient information for analysis.
* **Documentation:** Configurations, detections, investigations, and results are documented.
* **Reproducibility:** The environment should be documented sufficiently for the lab to be recreated.

## Planned SOC Workflow

```text
Endpoint Activity
       │
       ▼
Log / Event Collection
       │
       ▼
Wazuh Analysis
       │
       ▼
Alert Generation
       │
       ▼
SOC Investigation
       │
       ├── False Positive
       │
       └── Potential Incident
                  │
                  ▼
           MITRE ATT&CK Mapping
                  │
                  ▼
           Incident Response
```

## Future Architecture Documentation

The architecture section will be expanded as the lab develops to include:

* Final deployed network topology
* Virtual machine specifications
* IP addressing
* Wazuh component relationships
* Endpoint-to-manager communication
* Security testing workflow
* Data and alert flow
* Screenshots of the deployed environment

## Related Sections

* [`../setup/`](../setup/) — Lab installation and configuration
* [`../configurations/`](../configurations/) — Security and system configurations
* [`../detection/`](../detection/) — Detection engineering and alert rules
* [`../vulnerability-management/`](../vulnerability-management/) — Vulnerability assessment
* [`../investigation/`](../investigation/) — Security alert investigations
* [`../mitre-attack/`](../mitre-attack/) — MITRE ATT&CK mapping
* [`../incident-response/`](../incident-response/) — Incident response workflows
* [`../screenshots/`](../screenshots/) — Evidence from the lab environment
