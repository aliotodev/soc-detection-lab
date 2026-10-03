# INC-002 - Registry Run Key Persistence

## Summary
A controlled persistence technique was stimulated on the Windows endpoint by creating a registry Run key entry using `reg.exe`

The purpose of this activity was to validate Sysmon process telemetry, Wazuh ingestion, and analyst investigation of persistence-related behavior.

## Detection Source

- Endpoint: `WIN11-HOST`
- Telemetry: Sysmon
- SIEM: Wazuh
- Primary Event Type: Process Creation
- Sysmon Event ID: `13`

## Observed Activity
A registry value was created under the Windows Run-key persistence mechanism

The activity was associated with:
`HKCU\Software\Microsoft\Windows\CurrentVersion\Run`

A test value named:
`SOC-Lab-Test5`

was configured to execute:

`notepad.exe`

This registry location can cause configured programs to execute when the user logs in.

## Supporting Process Telemetry
Sysmon also recorded a process creation event showing `reg.exe` being launched by PowerShell.

- Sysmon Event ID: `1`
- Image: `C:\Windows\System32\reg.exe`
- Parent Image: `C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe`
- Process ID: `9032`
- User: `M\MA`
- Integrity Level: `High`
- Timestamp: `2026-10-03 21:40:27.368 UTC`

### Command Line

```text
"C:\WINDOWS\system32\reg.exe" add HKCU\Software\Microsoft\Windows\CurrentVersion\Run /v SOC-Lab-Test5 /t REG_SZ /d notepad.exe /f

```
## Correlation

This investigation correlated registry and process telemetry:
PowerShell
    ↓
reg.exe
    ↓
Sysmon Event ID 1
Process creation and command line captured
    ↓
Registry Run key modified
    ↓
Sysmon Event ID 13
Registry value set

## MITRE ATT&CK Mapping
**T1547.001 — Boot or Logon Autostart Execution: Registry Run Keys / Startup Folder**

### Analysis Assessment
The activity was intentionally generated as part of the SOC detection lab and was benign.
However, registry Run keys are a legitimate persistence mechanism that can also be abused by bad actors. Unexpected creation or modification of these values would warrant investigation in a production environment.
## Remediation
The lab persistence entry was removed after testing:
`reg delete "HKCU\Software\Microsoft\Windows\CurrentVersion\Run" /v SOC-Lab-Test5 /f`

## Outcome & Lessons Learned
### Outcome
The exercise demonstrated:
- Registry modification visibility with Sysmon Event ID 13
- Process creation visibility with Sysmon Event ID 1
- Parent/child process analysis
- Command-line investigation
- Raw-event analysis in Wazuh
- MITRE ATT&CK mapping
- Persistence investigation
### Lessons Learned
- Sysmon Event ID 13 records registry value modifications.
- Sysmon Event ID 1 provides supporting process and command-line context.
- Correlating multiple event types provides a more complete picture than relying on a single event.
- Raw Wazuh archives can expose useful telemetry that may not appear in the standard alert view.
- Detection coverage depends heavily on proper Sysmon configuration.
