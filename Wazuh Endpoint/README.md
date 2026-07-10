# Wazuh SIEM/XDR Home Lab: Ubuntu Server + macOS Endpoint Monitoring

## Overview

I completed a Wazuh SIEM/XDR home lab where I deployed Wazuh on an Ubuntu virtual machine and onboarded my macOS system as a monitored endpoint agent.

The purpose of this project was to build a practical blue-team lab that demonstrates centralized security monitoring, endpoint telemetry collection, File Integrity Monitoring, alert validation, and incident-style documentation.

This project simulates a basic Security Operations Center workflow:

```text
Endpoint activity → Wazuh agent → Wazuh manager → Wazuh indexer → Wazuh dashboard → Analyst review
