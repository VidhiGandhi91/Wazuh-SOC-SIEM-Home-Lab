# Wazuh SOC/SIEM Home Lab

A hands-on cybersecurity home lab focused on **Security Information and Event Management (SIEM), security monitoring, vulnerability management, attack simulation, log analysis, detection engineering, and incident response** using Wazuh.

The lab is built in an isolated VirtualBox environment containing a Wazuh Manager running on Ubuntu and a Bitnami WordPress server acting as the monitored endpoint and attack target.

---

## 🎯 Project Objectives

The main objectives of this project are to:

* Deploy and configure a Wazuh SIEM environment
* Connect and monitor a Linux-based endpoint
* Collect and analyse authentication events
* Simulate password-guessing and brute-force activity
* Perform vulnerability assessment using Wazuh
* Analyse security alerts and threat events
* Understand MITRE ATT&CK classification
* Investigate the limitations of default SIEM detection
* Improve application-layer visibility through additional log integration and custom detection rules
* Document detection, investigation, response, and lessons learned

---

## 🏗️ Lab Architecture

The initial lab uses an isolated **VirtualBox NAT Network**.

| Component          | Role                               | IP Address    |
| ------------------ | ---------------------------------- | ------------- |
| Ubuntu             | Wazuh Manager                      | `10.0.3.4`    |
| Bitnami WordPress  | Monitored Endpoint / Attack Target | `10.0.3.5`    |
| VirtualBox Network | Isolated NAT Network               | `10.0.3.0/24` |

### Architecture


                    Isolated VirtualBox NAT Network
                         10.0.3.0/24
                              │
             ┌────────────────┴────────────────┐
             │                                 │
             ▼                                 ▼
     Ubuntu VM                         Bitnami WordPress VM
   Wazuh Manager                           Wazuh Agent
     10.0.3.4                               10.0.3.5
             │                                 │
             │◄──── Security Events ──────────│
             │                                 │
             ▼                                 ▼
      Wazuh Dashboard                    WordPress
      Threat Hunting                     Web Application
```

---

## 🛠️ Technologies and Tools

* **Wazuh SIEM**
* **Ubuntu Linux**
* **Bitnami WordPress**
* **VirtualBox**
* **WPScan**
* **MITRE ATT&CK**
* Linux authentication logs
* WordPress / web application logs

---

# Phase 1 — Environment Setup

## 1. VirtualBox Network

An isolated NAT Network was created using:

```
10.0.3.0/24
```

This allowed the virtual machines to communicate with each other within the lab environment.

---

## 2. Wazuh Manager

The Ubuntu virtual machine was configured as the Wazuh Manager.

Resources:

* 2 vCPU
* 4 GB RAM
* 50 GB storage
* IP address: `10.0.3.4`

Wazuh was installed using the following commands:

```
curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh
sudo bash wazuh-install.sh -a
```

The Wazuh dashboard was then accessed through:

```
https://10.0.3.4
```

---

## 3. Bitnami WordPress Endpoint

A Bitnami WordPress virtual machine was configured on the same isolated network.

IP address:

```
10.0.3.5
```

The system was used as:

1. A monitored endpoint
2. A WordPress application server
3. A target for controlled security testing

---

# Phase 2 — Wazuh Agent Configuration

The Wazuh agent was installed on the Bitnami endpoint and configured to communicate with the Wazuh Manager.

```
sudo WAZUH_MANAGER='10.0.3.4' WAZUH_AGENT_NAME='S20240099' dpkg -i wazuh-agent.deb
```

The agent was registered using:

```
sudo /var/ossec/bin/agent-auth -m 10.0.3.4 -A S20240099
```

The connection was verified from the Wazuh Manager:

```bash
sudo /var/ossec/bin/agent_control -l
```

The agent successfully appeared as **ACTIVE**.

---

# Phase 3 — Authentication Failure Detection

A controlled password-guessing scenario was performed against the Bitnami system.

Multiple incorrect login attempts were intentionally generated after rebooting the virtual machine.

The resulting authentication events were collected by the Wazuh agent and displayed in Wazuh Threat Hunting.

### Result

Wazuh successfully detected:

* Authentication failures
* Failed login events
* Password-guessing activity

The events were also associated with relevant **MITRE ATT&CK** classification.

### Security Lesson

This demonstrated that Wazuh can provide effective visibility into system-level authentication activity when the relevant operating-system logs are available to the agent.

---

# Phase 4 — WordPress Brute-Force Simulation

A controlled WordPress brute-force simulation was performed using **WPScan**.

Target:

```text
http://10.0.3.5/wp-login.php
```

The test used the identified WordPress username and the `rockyou.txt` password wordlist to simulate automated password-guessing attempts.

The purpose was to determine whether Wazuh's default configuration would detect application-layer brute-force activity.

### Result

The WPScan attack generated multiple automated login attempts.

However, **no dedicated WordPress brute-force detection events were observed in Wazuh under the default configuration**.

This became an important finding in the lab.

---

# 🔍 Detection Gap Identified

The lab demonstrated an important difference between **system-level** and **application-level** monitoring.

### System-level authentication

Wazuh successfully detected authentication failures because operating-system authentication events are available through system logs such as:

```text
/var/log/auth.log
```

### WordPress application authentication

WordPress login attempts occur at the application layer and are handled through the web application stack.

Under the configuration used during the initial experiment, these application events were not being directly monitored by Wazuh.

### Key Finding

```text
WPScan
   │
   ▼
WordPress Login
   │
   ▼
Application/Web Logs
   │
   X
   │
   └── Default Wazuh configuration did not generate
       a dedicated WordPress brute-force alert
```

This demonstrates that **SIEM visibility depends heavily on correct log-source integration and detection rules**.

---

# 🛡️ Vulnerability Management

Wazuh vulnerability detection identified several significant vulnerabilities on the Bitnami environment.

The three vulnerabilities analysed in the original lab were:

### CVE-2023-50387

DNSSEC-related vulnerability associated with excessive computational processing.

Potential impact includes:

* Resource exhaustion
* Performance degradation
* Denial-of-Service conditions

General mitigation includes applying appropriate software updates and monitoring abnormal DNS activity.

### CVE-2023-50868

DNSSEC NSEC3-related computational attack.

Potential impact includes:

* High CPU usage
* System performance degradation
* Potential Denial-of-Service conditions

General mitigation includes updating affected DNS software and applying appropriate DNS security controls.

### CVE-2024-28085

Linux kernel TTY information-leak vulnerability.

Potential impact includes:

* Sensitive information exposure
* Information disclosure
* Potential security impact to affected systems

General mitigation includes applying current security patches and maintaining an updated Linux kernel.

---

# 🧪 Planned Detection Engineering

The initial experiment identified a detection gap for WordPress brute-force activity.

The next phase of this project will therefore focus on improving detection coverage.

Planned work includes:

* [ ] Integrate relevant WordPress / Apache logs with Wazuh
* [ ] Create custom Wazuh detection rules
* [ ] Detect repeated WordPress login failures
* [ ] Generate a dedicated WordPress brute-force alert
* [ ] Test SSH brute-force detection
* [ ] Test Nmap scanning detection
* [ ] Configure File Integrity Monitoring
* [ ] Investigate generated alerts
* [ ] Map detections to MITRE ATT&CK
* [ ] Build an incident timeline
* [ ] Perform a complete incident-response exercise
* [ ] Document detection improvements
* [ ] Create a final SOC monitoring dashboard

---

# 🚨 Planned Incident Response Workflow

Future attack simulations will follow a simplified SOC incident-response process:

```text
Attack Simulation
       │
       ▼
Detection
       │
       ▼
Alert Investigation
       │
       ▼
Evidence Collection
       │
       ▼
Containment
       │
       ▼
Eradication
       │
       ▼
Recovery
       │
       ▼
Lessons Learned
```

The objective is to demonstrate not only how to generate alerts, but also how a security analyst would investigate and respond to them.

---

# 📊 Project Evidence

Screenshots and supporting evidence will be organised throughout the project.

Planned evidence includes:

* VirtualBox network configuration
* Ubuntu configuration
* Bitnami network configuration
* Wazuh installation
* Wazuh dashboard
* Active Wazuh agent
* Authentication failure detection
* MITRE ATT&CK classification
* WPScan attack execution
* WordPress detection gap
* Custom detection rules
* Security alerts
* Vulnerability findings
* Incident investigation
* Final monitoring dashboard

---

# 📚 Key Learning Outcomes

This project demonstrates practical experience with:

* SIEM deployment
* Endpoint monitoring
* Security event collection
* Authentication monitoring
* Vulnerability management
* Attack simulation
* Log analysis
* Threat detection
* Detection gaps
* Custom detection engineering
* MITRE ATT&CK mapping
* Incident investigation
* Incident response
* Security documentation

---

# ⚠️ Lab Disclaimer

All security testing in this repository is performed within an isolated, controlled virtual laboratory environment for educational and defensive cybersecurity purposes.

No testing is intended against systems or applications without authorisation.

---

# 🚧 Project Status

**Current status: In Progress**

The initial Wazuh deployment, endpoint integration, authentication monitoring, vulnerability assessment, and WordPress brute-force testing have been completed.

The next stage is to improve application-layer visibility and build custom security detections based on the detection gap identified during testing.
