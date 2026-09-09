# SOC/SIEM Home Lab Architecture

## Overview

This section documents the architecture of the Wazuh-based SOC/SIEM home lab developed in a controlled VirtualBox environment.

The lab is designed to simulate a small Security Operations Center (SOC) environment where security events are collected from a monitored endpoint, analysed by Wazuh, and investigated through the Wazuh Dashboard.

The environment also provides a controlled platform for vulnerability assessment and security testing against a WordPress application.

## Architecture Objectives

The architecture is designed to demonstrate practical SOC and SIEM capabilities, including:

* Centralised security event monitoring
* Endpoint monitoring using Wazuh Agent
* Security event collection and analysis
* Authentication and system activity monitoring
* Vulnerability monitoring
* Controlled security testing
* Alert investigation
* MITRE ATT&CK technique mapping
* Incident response workflows
* Security evidence collection and documentation

## Lab Environment

The current lab consists of two primary virtual machines connected through an isolated VirtualBox NAT Network.

| Component              | Role                                                        | IP Address    |
| ---------------------- | ----------------------------------------------------------- | ------------- |
| Ubuntu VM              | Wazuh Manager and Wazuh Dashboard                           | `10.0.3.4`    |
| Bitnami WordPress VM   | Wazuh Agent, monitored endpoint and security testing target | `10.0.3.5`    |
| VirtualBox NAT Network | Isolated network connecting the virtual machines            | `10.0.3.0/24` |
| WPScan                 | Controlled vulnerability and security testing tool          | N/A           |

## Network Architecture

The virtual machines communicate through an isolated VirtualBox NAT Network.

```text
                    VirtualBox
               Isolated NAT Network
                    10.0.3.0/24
                         │
              ┌──────────┴──────────┐
              │                     │
              ▼                     ▼
     ┌─────────────────┐    ┌─────────────────────┐
     │    Ubuntu VM    │    │ Bitnami WordPress   │
     │                 │    │        VM           │
     │ Wazuh Manager   │◄──►│ Wazuh Agent         │
     │ Wazuh Dashboard │    │ WordPress Server    │
     │                 │    │ Security Test Target│
     │   10.0.3.4      │    │     10.0.3.5        │
     └─────────────────┘    └─────────────────────┘
                                      ▲
                                      │
                                 WPScan Testing
```

### Network Design

The isolated network provides separation between the lab environment and the host system while allowing the virtual machines to communicate with each other.

The current addressing scheme is:

```text
Network:        10.0.3.0/24
Ubuntu VM:      10.0.3.4
WordPress VM:   10.0.3.5
```

The network configuration may be expanded as additional endpoints and security testing components are introduced.

## Wazuh Architecture

The Ubuntu virtual machine hosts the primary Wazuh components used by the lab.

### Wazuh Manager

The Wazuh Manager is responsible for receiving and analysing security data from the monitored endpoint.

Its responsibilities within this lab include:

* Receiving events from the Wazuh Agent
* Analysing collected security data
* Applying detection rules
* Generating security alerts
* Supporting vulnerability monitoring
* Providing data for security investigations

### Wazuh Dashboard

The Wazuh Dashboard provides the visual interface used to monitor and investigate the environment.

The dashboard is used to review:

* Security alerts
* Endpoint activity
* Authentication events
* Vulnerability information
* Security monitoring data
* Investigation results

### Wazuh Agent

The Wazuh Agent is installed on the Bitnami WordPress virtual machine.

The agent collects relevant endpoint information and forwards security events to the Wazuh Manager.

The monitored endpoint provides a realistic target for generating security telemetry and performing controlled security testing.

## Monitored Endpoint

The Bitnami WordPress virtual machine serves two purposes within the lab:

1. **Monitored endpoint**
2. **Controlled security testing target**

The environment allows endpoint activity and security testing to be observed through Wazuh.

Examples of activities that can generate observable security events include:

* Authentication failures
* Authentication activity
* System events
* File and system activity
* Web application activity
* Vulnerability scanning
* Controlled WordPress security testing

## Security Testing

WPScan is used for controlled security testing of the WordPress environment.

The purpose of this testing is not to attack external systems but to generate realistic security activity within the isolated home lab.

The resulting activity can be analysed to determine:

* What activity is visible to Wazuh
* Which events generate alerts
* Which events are not detected automatically
* What additional monitoring or detection rules may be required

This provides an opportunity to practise detection engineering rather than relying only on default SIEM alerts.

## Security Monitoring Data Flow

The current monitoring workflow can be represented as:

```text
┌──────────────────────────┐
│ Bitnami WordPress VM     │
│                          │
│ Endpoint / Web Activity  │
└────────────┬─────────────┘
             │
             │ Wazuh Agent
             ▼
┌──────────────────────────┐
│ Wazuh Manager            │
│                          │
│ Event Analysis           │
│ Detection Rules          │
│ Alert Generation         │
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│ Wazuh Dashboard          │
│                          │
│ Monitoring               │
│ Alert Review             │
│ Investigation            │
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│ SOC Investigation        │
│                          │
│ Detection Analysis       │
│ MITRE ATT&CK Mapping     │
│ Incident Response        │
└──────────────────────────┘
```

## SOC Monitoring Workflow

The lab follows a simplified SOC workflow:

```text
Endpoint Activity
       │
       ▼
Wazuh Agent Collection
       │
       ▼
Wazuh Manager Analysis
       │
       ▼
Alert Generation
       │
       ▼
Wazuh Dashboard
       │
       ▼
Alert Investigation
       │
       ├───────────────┐
       │               │
       ▼               ▼
 False Positive    Potential Incident
                       │
                       ▼
                MITRE ATT&CK Mapping
                       │
                       ▼
                Incident Response
                       │
                       ▼
                Evidence & Reporting
```

## Detection and Investigation

The architecture supports detection engineering by allowing security activity to be generated against the monitored endpoint and then evaluated through Wazuh.

The investigation process includes:

1. Reviewing generated alerts.
2. Identifying the affected endpoint.
3. Examining event details and timestamps.
4. Determining the nature of the activity.
5. Assessing whether the alert represents a true positive or false positive.
6. Identifying the relevant attack technique where applicable.
7. Mapping activity to MITRE ATT&CK.
8. Documenting investigation findings.
9. Developing or improving detection logic where required.
10. Defining an appropriate incident response action.

## Vulnerability Monitoring

The lab also supports vulnerability management activities.

The WordPress environment can be assessed using controlled vulnerability scanning and security testing techniques.

The vulnerability management workflow is:

```text
Vulnerability Assessment
          │
          ▼
Identify Vulnerabilities
          │
          ▼
Validate Findings
          │
          ▼
Assess Risk
          │
          ▼
Prioritise Remediation
          │
          ▼
Apply Security Improvements
          │
          ▼
Re-test
```

## MITRE ATT&CK Integration

Where appropriate, observed security activity is mapped to the MITRE ATT&CK framework.

The mapping process helps identify:

* Initial Access techniques
* Credential Access techniques
* Discovery techniques
* Execution techniques
* Persistence techniques
* Other applicable adversary behaviours

MITRE ATT&CK mapping will be documented separately within:

```text
mitre-attack/
```

## Incident Response Integration

The architecture supports a basic incident response workflow.

When suspicious activity is identified, the investigation can progress through:

```text
Detection
   │
   ▼
Alert Triage
   │
   ▼
Investigation
   │
   ▼
Determine Scope
   │
   ▼
MITRE ATT&CK Mapping
   │
   ▼
Containment
   │
   ▼
Remediation
   │
   ▼
Validation
   │
   ▼
Lessons Learned
```

Detailed incident response procedures and case documentation will be maintained in:

```text
incident-response/
```

## Security and Isolation Principles

The lab follows several security and documentation principles.

### Isolation

Security testing is performed within a controlled virtual environment rather than against unauthorised external systems.

### Visibility

The lab is designed so that security activity produces observable telemetry wherever possible.

### Detection

Security events are analysed to determine whether they generate meaningful alerts.

### Investigation

Alerts are investigated using available event information and supporting evidence.

### Reproducibility

Configuration and testing procedures are documented so that the lab can be recreated and extended.

### Evidence

Relevant screenshots, configuration information, alerts, and investigation results are retained as project evidence.

## Current Architecture Limitations

The current environment is intentionally small and focuses on learning core SOC/SIEM concepts.

Current limitations include:

* Limited number of monitored endpoints
* Single primary Wazuh Manager environment
* No enterprise-scale network infrastructure
* No dedicated external attacker machine documented as part of the current architecture
* Limited endpoint diversity
* Home-lab network rather than production infrastructure

These limitations provide opportunities for future expansion.

## Planned Architecture Improvements

Future iterations of the lab may include:

* Additional Windows endpoint monitoring
* Additional Linux endpoint monitoring
* Dedicated attacker/security testing VM
* Additional web application targets
* Network traffic monitoring
* Custom Wazuh detection rules
* File Integrity Monitoring use cases
* Brute-force detection
* Web attack detection
* Malware simulation
* MITRE ATT&CK technique-based investigations
* Automated incident response
* Expanded incident case documentation

## Architecture Documentation Roadmap

The architecture section will continue to document:

* Final network topology
* Virtual machine configuration
* IP addressing
* Wazuh component relationships
* Agent-to-manager communication
* Security event flow
* Detection workflow
* Vulnerability testing workflow
* Investigation workflow
* Incident response workflow
* Supporting screenshots and evidence

## Related Sections

* [`../setup/`](../setup/) — Lab installation and setup
* [`../configurations/`](../configurations/) — System and Wazuh configurations
* [`../detection/`](../detection/) — Detection engineering and alert rules
* [`../vulnerability-management/`](../vulnerability-management/) — Vulnerability assessment and management
* [`../investigation/`](../investigation/) — Security alert investigations
* [`../mitre-attack/`](../mitre-attack/) — MITRE ATT&CK mapping
* [`../incident-response/`](../incident-response/) — Incident response workflows
* [`../screenshots/`](../screenshots/) — Lab screenshots and evidence
