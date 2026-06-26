# wazuh-siem-macos-lab
A  completed a Wazuh SIEM/XDR home lab where I deployed Wazuh on an Ubuntu VM and onboarded my macOS machine as an endpoint agent.


# Wazuh SIEM/XDR Home Lab

## Objective
Built a Wazuh SIEM/XDR home lab using an Ubuntu VM as the Wazuh server and a macOS endpoint as the monitored agent. The goal was to deploy security monitoring, validate endpoint telemetry, and demonstrate File Integrity Monitoring detections.

## Architecture
- Ubuntu 24.04 LTS VM: Wazuh manager, indexer, dashboard, Filebeat
- macOS endpoint: Wazuh agent
- Network: Local private lab network
- Dashboard: HTTPS access to Wazuh web interface

## Key Accomplishments
- Installed Wazuh all-in-one stack
- Resolved disk space and LVM storage issues
- Deployed Wazuh agent on macOS
- Verified agent status as Active
- Configured File Integrity Monitoring
- Detected file added, modified, and deleted events
- Confirmed alerts in the Wazuh dashboard

## Detection Test
Created, modified, and deleted a file in a monitored macOS directory:

/Users/lafleur/wazuh-fim-test/demo.txt

Wazuh generated alerts for:
- File added
- Integrity checksum changed
- File deleted

## Skills Demonstrated
- SIEM deployment
- Endpoint monitoring
- Linux administration
- macOS security monitoring
- File Integrity Monitoring
- Alert analysis
- Troubleshooting
