# INC-001 - PowerShell File Creation

## Summary
A PowerShell process was observed creating a file in the user's temporary directory. This activity was generated intentionally as part of the SOC detection lab to validate Sysmon telemetry and Wazuh event ingestion.

## Detection Source

- Endpoint: WIN11-HOST
- Telemetry: Sysmon
- SIEM: Wazuh
- Event IDs:
  - 1 - Process Create
  - 11 - File Create

 ## Observed Activity
PowerShell executed a command to create:

'C:\Users\MA\AppData\Local\Temp\soc-lab-test3.txt'

The activity was captured by Sysmon and ingested into Wazuh.

## Process Details
- Image: 'powershell.exe'
- Parent Image: 'powershell.exe'
- Integrity Level: High
- User: M\MA
- Command:

`New-Item -Path C:\Users\MA\AppData\Local\Temp\soc-lab-test3.txt -ItemType File -Force'

## MITRE ATT&CK Mapping

- T1059.001 -- Command and Scripting Interpreter: PowerShell

## Remediation

No remediation was required.

## Lessons Learned
- Sysmon does not collect every event type by default.
- File creation telemetry had to be explicitly enabled
- Process and file events can be correlated to reconstruct activity.
