# Build Your Own SOC: SOC Analyst Lab

### Practical Cybersecurity | Security Operations | Threat Detection

## About the Project

This repository documents my hands-on journey of building a Security Operations Center (SOC) Analyst Lab.

The main objective is to develop practical cybersecurity skills through security monitoring, log analysis, threat detection, incident investigation, and SIEM operations.

This project focuses on understanding how real-world SOC analysts monitor systems, identify suspicious activities, investigate security events, and respond to potential threats.

## Project Objectives

- Understand SOC operations and security monitoring.
- Configure and work with SIEM tools.
- Collect and analyze Windows and Linux security logs.
- Monitor authentication activities.
- Identify suspicious patterns and potential threats.
- Perform basic security investigations.
- Develop and test detection rules.
- Analyze network traffic.
- Document investigations and technical findings.

## Tools & Technologies

| Tool / Technology | Purpose |
|---|---|
| Splunk Enterprise | SIEM and log analysis |
| Windows Event Viewer | Windows security log investigation |
| Windows Security Logs | Authentication monitoring |
| SPL | Searching and analyzing security events |
| GitHub | Project documentation and version control |

## Lab Environment

- Operating System: Windows
- SIEM Platform: Splunk Enterprise
- Log Source: Windows Security Event Logs
- Hardware: Personal computer

## Practical Work

### Windows Security Monitoring

- Explored Windows Security Event Logs.
- Investigated successful login events (Event ID 4624).
- Investigated failed login events (Event ID 4625).
- Connected Windows Security Logs to Splunk.
- Verified successful log collection and event visibility.

### SIEM Monitoring with Splunk

- Performed searches using Splunk Processing Language (SPL).
- Analyzed successful and failed authentication events.
- Compared login event counts.
- Created a SOC Login Monitoring dashboard.
- Created visualizations for login activity and failed login attempts.

## Repository Structure

```text
build-your-own-soc/
│
├── README.md
├── Lab-Setup/
├── SIEM-Monitoring/
├── Windows-Security/
├── Linux-Security/
├── Network-Analysis/
├── Threat-Detection/
├── Incident-Response/
├── Detection-Rules/
├── Scripts/
├── Investigations/
└── Screenshots/
```

*Folders will be populated as the project develops.*

## Learning Outcomes

Through this project, I aim to gain practical experience in:

- SIEM operations and log analysis.
- Security event investigation.
- Authentication monitoring.
- Threat identification.
- Basic incident response.
- Security documentation and reporting.

## Project Status

**Status:** In Progress

This repository will be continuously updated with practical exercises, configurations, SPL queries, investigation reports, screenshots, and technical documentation.

---

**Note:** This is a personal educational project designed to develop practical SOC Analyst skills.
