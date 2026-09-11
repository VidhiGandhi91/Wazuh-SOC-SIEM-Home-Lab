# Wazuh SOC/SIEM Home Lab

A practical SOC/SIEM home lab built using **Wazuh**, **Ubuntu**, and a **Bitnami WordPress VM**.  
This project demonstrates real-world security monitoring, attack simulation, detection engineering, and MITRE ATT&CK mapping inside an isolated virtual environment.

---

## 🔧 Lab Architecture
- VirtualBox NAT Network (10.0.3.0/24)  
- **Wazuh Manager** (Ubuntu)  
- **Wazuh Agent** (Bitnami WordPress VM)  
- Isolated SOC environment for safe attack simulation

📁 Folder: [`/architecture`](architecture)

---

## 📦 Setup & Deployment
- Wazuh Manager installation  
- Agent deployment on WordPress VM  
- Secure manager–agent communication  
- Dashboard access and initial configuration

📁 Folder: [`/setup`](setup)

---

## 🛡️ Security Monitoring (Completed Stages)
- System authentication monitoring  
- Password guessing detection  
- WPScan brute-force simulation  
- Vulnerability assessment (CVE findings)  
- MITRE ATT&CK mapping for detected events

📁 Future folders (to be added):
- [`/authentication-monitoring`](authentication-monitoring)
- [`/password-guessing`](password-guessing)
- [`/wpscan`](wpscan)
- [`/vulnerability-assessment`](vulnerability-assessment)
- [`/mitre-mapping`](mitre-mapping)

---

## 🚀 Upcoming Enhancements (SOC-Level Stages)
This lab will be extended with full SOC workflows:

1. Application/Web log integration (Apache + WordPress)  
2. Custom Wazuh detection rules  
3. Multiple attack simulations  
4. Alert investigation workflows  
5. MITRE ATT&CK deep analysis  
6. Incident response simulation  
7. Detection tuning & improvement  
8. SOC dashboards & reporting

📁 Future folders (to be added):
- [`/stage8-application-logs`](stage8-application-logs)
- [`/stage9-custom-rules`](stage9-custom-rules)
- [`/stage10-attack-library`](stage10-attack-library)
- [`/stage11-alert-investigation`](stage11-alert-investigation)
- [`/stage12-mitre-investigation`](stage12-mitre-investigation)
- [`/stage13-incident-response`](stage13-incident-response)
- [`/stage14-detection-improvement`](stage14-detection-improvement)
- [`/stage15-soc-dashboard`](stage15-soc-dashboard)

---

## 🎯 Project Goal
To build a complete SOC home lab demonstrating:

- SIEM deployment  
- Log ingestion  
- Threat detection  
- Attack simulation  
- Detection engineering  
- MITRE mapping  
- Incident response  
- SOC reporting

This repository serves as a practical cybersecurity portfolio showcasing real SIEM and SOC skills.

---

## 📌 Status
**Stages 1–7 completed**  
**Stages 8–15 in progress**
