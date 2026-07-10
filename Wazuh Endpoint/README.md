# Wazuh Endpoint Security, Vulnerability Management, and Compliance Lab

## Project Overview

This project is a hands-on cybersecurity lab designed to demonstrate endpoint security monitoring, vulnerability management, risk assessment, and compliance mapping.

The lab uses:

- Ubuntu as the Wazuh Manager
- macOS as the monitored endpoint agent
- Wazuh for security monitoring, endpoint visibility, and vulnerability detection
- GitLab for documentation and interview portfolio presentation

## Project Goal

The goal of this project is to understand how security teams monitor endpoints, identify security risks, document vulnerabilities, and map technical security controls to compliance frameworks such as SOC 2 and HIPAA.

## Lab Environment

| Component | Purpose |
|---|---|
| Ubuntu | Hosts the Wazuh Manager |
| macOS | Endpoint monitored by Wazuh Agent |
| Wazuh | Security monitoring and vulnerability detection |
| GitLab | Documentation and portfolio repository |

## Skills Demonstrated

- Endpoint security monitoring
- Wazuh manager and agent deployment
- Vulnerability management basics
- Security risk assessment
- SOC 2 control mapping
- HIPAA security safeguard mapping
- Technical documentation
- Interview-ready project explanation

## Why This Project Matters

Security and compliance teams need visibility into systems. Without endpoint monitoring, organizations may not know what software is installed, what vulnerabilities exist, or what security events are happening.

This lab demonstrates how a security analyst can use Wazuh to monitor endpoints, review security findings, and document risks in a way that supports compliance readiness.

## Interview Summary

I built a Wazuh-based endpoint security lab using Ubuntu as the manager and macOS as the endpoint agent. I used the lab to monitor endpoint activity, review vulnerabilities, document risks, and map the security controls to SOC 2 and HIPAA concepts.





# Wazuh SIEM/XDR Home Lab: Ubuntu Server + macOS Endpoint Monitoring

## Overview

I completed a Wazuh SIEM/XDR home lab where I deployed Wazuh on an Ubuntu virtual machine and onboarded my macOS system as a monitored endpoint agent.

The purpose of this project was to build a practical blue-team lab that demonstrates centralized security monitoring, endpoint telemetry collection, File Integrity Monitoring, alert validation, and incident-style documentation.

This project simulates a basic Security Operations Center workflow:

```text
Endpoint activity → Wazuh agent → Wazuh manager → Wazuh indexer → Wazuh dashboard → Analyst review
