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
