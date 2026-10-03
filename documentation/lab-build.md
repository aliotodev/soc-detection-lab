# Lab Build & Infrastructure Map

## Environment

- Host OS: Windows 11 Home
- Virtualization: VMware Workstation Pro
- SIEM: Wazuh
- SIEM Server: Ubuntu Server
- Endpoint: Windows 11
- Endpoint Telemetry: Sysmon
- Threat Framework: MITRE ATT&CK

### Build Summary
1. Installed VMware Workstation Pro
2. Created Ubuntu Server VM
3. Configured networking and SSH
4. Installed Wazuh
5. Enrolled Windows endpoint
6. Installed Sysmon
7. Configured Sysmon telemetry
8. Enabled raw Wazuh archives
9. Validated endpoint telemetry
10. Performed controlled detection scenarios

## Architecture

```text
Windows 11 Host
│
├── Sysmon
├── Windows Event Logs
├── Wazuh Agent
│
└── VMware Workstation Pro
    └── Ubuntu Server
        └── Wazuh
            ├── Manager
            ├── Indexer
            └── Dashboard
