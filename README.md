# SOC Detection Lab
This is a project for cybersecurity focused on security monitoring, threat detection, incident investigation, and MITRE ATT&CK mapping using Windows, Linux, Sysmon, and Wazuh.

# Project Overview
The goal of this project is to build a foundation for creating and utilizing a small SOC environment.
The lab will be used to generate security events, collect endpoint telemetry, create detections, investigate alerts, and document incidents using workflows similar to how SOC analysts do so.

## Investigations

### [INC-001 — PowerShell File Creation](incidents/INC-001-powershell-file-creation.md)
Investigated PowerShell process activity and correlated Sysmon process creation with file creation telemetry.

### [INC-002 — Registry Run Key Persistence](incidents/INC-002-registry-run-key-persistence.md)
Simulated Windows Run-key persistence and investigated registry and process telemetry associated with the activity.

### [INC-003 — PowerShell DNS and Network Activity](incidents/INC-003-powershell-dns-network-activity.md)
Correlated Sysmon DNS and network connection events using Process ID and Process GUID to reconstruct outbound PowerShell activity.

## Vulnerability Management

Wazuh vulnerability detection identified outdated software on the Windows endpoint.

One remediation case involved GIMP, where multiple CVEs were associated with an outdated installed version.

The application was upgraded from version `3.0.6-1` to version `3.2`.

After Wazuh refreshed its vulnerability data, the previous GIMP findings were no longer present, validating successful remediation.

## Documentation
- [Lab Build](documentation/lab-build.md)
- [Lessons Learned](documentation/lessons-learned.md)
- [Vulnerability Remediation](documentation/vulnerability-remediation.md)


# Objectives
- Deploy a Linux-based Wazuh SIEM environment
- Monitor a Windows 11 endpoint
- Collect Windows Event Logs and Sysmon telemetry
- Generate controlled suspicious activity
- Investigate alerts and determine root cause
- Map observed activity to the MITRE ATT&CK framework
- Create detection documentation
- Write professional incident reports
- Develop basic security automation scripts
- Document lessons learned throughout the project

# Skills Demonstrated
This project is intended to develop practical experience with:
- SIEM Administration
- Windows endpoint monitoring
- Windows Event Log analysis
- Sysmon
- Log analysis
- Threat detection
- Incident response
- Threat hunting
- Linux administration
- Windows security
- MITRE ATT&CK
- Detection engineering
- Security documentation
- Bash, Python, and PowerShell

## Project Roadmap

- [x] Install VMware Workstation Pro
- [x] Create Ubuntu Server virtual machine
- [x] Configure Linux networking and system updates
- [x] Install Wazuh
- [x] Install Wazuh Agent on Windows
- [x] Install and configure Sysmon
- [x] Verify Sysmon telemetry collection in Wazuh
- [x] Validate process creation telemetry
- [x] Validate file creation telemetry
- [x] Validate registry telemetry
- [x] Validate DNS and network telemetry
- [x] Investigate PowerShell activity
- [x] Investigate registry persistence
- [x] Investigate PowerShell DNS/network activity
- [x] Map activity to MITRE ATT&CK
- [x] Perform vulnerability remediation
- [x] Validate vulnerability closure
- [x] Document lessons learned
- [ ] Create custom Wazuh detection rules
- [ ] Develop PowerShell/Python security automation

## Project Status

**Version 1: Core SOC Lab Complete**

The core SOC environment is operational and has been used to perform endpoint monitoring, telemetry analysis, vulnerability remediation, and controlled security investigations.

The lab currently provides visibility into:

- Windows process creation
- File creation
- Registry activity
- DNS queries
- Network connections
- Vulnerability findings
- Raw security telemetry

Three controlled investigation scenarios have been completed and documented using Sysmon and Wazuh.

Future development will focus on custom detection rules, automation, and additional attack simulations.
