# Lessons Learned

## 1. Troubleshooting Silent Downloads

While installing Wazuh, the installer script within the Linux terminal initially failed to download successfully.

The original, documented command used:

```bash
curl -s0 https://packages.wazuh.com/4.14/wazuh-install.sh
```
Learning that the -s flag enables silent mode, the command provided no useful feedback upon troubleshooting why the install wasn't going through.
Troubleshooting steps included:
- Verifying the current directory with pwd
- Checking whether the file existed with ls -lh
- Confirming curl was installed
- Checking the VM's system time
- Enabling NTP synchronization
- Retrying the download with verbose output

The successful troubleshooting command was:
```bash
curl -v https://packages.wazuh.com/4.14/wazuh-install.sh -o wazuh-install.sh
```
## 2. Sysmon Telemetry Depends on Config

During my first investigation, Sysmon successfully was able to record process creation events, but no file creation events.
Reviewing the active Sysmon configuration showed that no custom rules were installed and that FileCreate events were not being collected by default

The installed Sysmon schema confirmed:
- Event ID 1 = Process Create
- Event ID 11 = File Create
- FileCreate is excluded by default unless explicitly enabled.

Creating a custom configuration for Sysmon was done to include this telemetry.

### Key Takeaway:
Sysmon does not automatically come with every useful event type and is important to know as these logs are important.

Telemetry coverage must be validated against the current config, if an expected event is missing, checking whether the corresponding Sysmon event type is enabled before assuming the activity was not logged is important.

This reinforced the importance of understanding:
- what telemetry a tool is capable of collecting
- what telemetry is ACTUALLY enabled in the current config.
## 3. Registry Telemetry Troubleshooting
Registry telemetry troubleshooting required validating each layer independently: first confirming Sysmon generated Event IDs 12–14 locally, then confirming the Wazuh agent collected the Sysmon channel, and finally enabling raw Wazuh archives to view events that did not trigger standard alerts. The key lesson was to verify telemetry at the source before troubleshooting the SIEM
