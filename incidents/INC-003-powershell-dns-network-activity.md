# INC-003 - PowerShell DNS and Network Activity

## Summary
A controlled PowerShell web request was generated to validate DNS and network telemetry is Sysmon and Wazuh.

This activity showed PowerShell resolving 'example.com' and then making an outbound HTTPS connection to one of the resolved IP addresses.

## Detection Source
- Endpoint: `WIN11-HOST`
- Telemetry: Sysmon
- SIEM: Wazuh
- Event ID 22 — DNS Query
- Event ID 3 — Network Connection

## DNS Activity
PowerShell queried:

`example.com`

Resolved addresses included:

- `104.20.23.154`
- `172.66.147.243`

Process:

`C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe`

Process ID:

`21488`

Process GUID:

`{9939ffd5-7c1e-6ac1-4007-00000000a202}`

## Network Activity

The same PowerShell process initiated an outbound connection to:

`104.20.23.154:443`

Details:

- Protocol: TCP
- Initiated: true
- Destination Port: 443
- Service: HTTPS
- Source IP: `192.168.1.159`
- Source Port: `53070`

## Correlation

The DNS and network events shared the same:

- Process ID: `21488`
- Process GUID: `{9939ffd5-7c1e-6ac1-4007-00000000a202}`

This confirmed that the PowerShell process that resolved `example.com` was also responsible for the outbound HTTPS connection.

## Process Flow

```text
powershell.exe
    ↓
DNS query: example.com
    ↓
104.20.23.154
    ↓
Outbound TCP connection
    ↓
104.20.23.154:443
```

# MITRE ATT&CK
**T1059.001 — Command and Scripting Interpreter: PowerShell**
The DNS and network events were used as supporting telemetry for PowerShell activity.

## Analyst Assessment
The activity was intentionally generated as part of the SOC detection lab and was benign.
In a production environment, PowerShell making unexpected outbound connections could warrant investigation, especially if the destination, command line, parent process, or surrounding activity appeared suspicious.
### Outcome
The exercise demonstrated:
- DNS query visibility with Sysmon Event ID 22
- outbound connection visibility with Sysmon Event ID 3
- process-level correlation using Process ID and Process GUID
- Wazuh raw-event investigation
- network activity reconstruction
### Key Takeaway
Correlating DNS and network telemetry using the same Process GUID provides stronger evidence than reviewing either event in isolation.
