# Wazuh Manager Setup on Ubuntu

## Purpose

This document explains the setup and purpose of the Wazuh Manager in my endpoint security and compliance lab.

The Ubuntu system is used as the central security monitoring server. It receives security data from endpoint agents, analyzes the information, and makes alerts visible in the Wazuh dashboard.

## Lab Role

| System | Role |
|---|---|
| Ubuntu | Wazuh Manager / central monitoring server |
| macOS | Endpoint monitored by Wazuh agent |
| Browser | Access to Wazuh dashboard |

## What the Wazuh Manager Does

The Wazuh Manager is responsible for:

- Receiving security data from Wazuh agents
- Analyzing endpoint activity
- Generating alerts
- Supporting vulnerability visibility
- Providing centralized monitoring
- Helping analysts review security events

## Why Ubuntu Is Used

Ubuntu is used as the Wazuh Manager because it is a common Linux server operating system and is supported for Wazuh server installation.

Using Ubuntu helps simulate a real-world security monitoring environment where Linux servers often host security tools.

## Wazuh Central Components

In this lab, the Wazuh environment includes:

| Component | Simple Explanation |
|---|---|
| Wazuh Server | Receives and analyzes endpoint data |
| Wazuh Indexer | Stores and indexes security data |
| Wazuh Dashboard | Web interface used by the analyst |
| Wazuh Agent | Installed on endpoints such as my Mac |

## Basic Setup Notes

> Note: Exact installation commands may vary depending on Wazuh version and operating system version. I followed the official Wazuh installation documentation for my lab setup.

High-level setup process:

1. Prepare the Ubuntu system
2. Install Wazuh central components
3. Access the Wazuh dashboard
4. Confirm the manager is running
5. Add the macOS endpoint as an agent
6. Verify that the agent reports to the manager

## Analyst Verification Checklist

After setup, I checked:

- The Ubuntu system was running
- Wazuh services were active
- The Wazuh dashboard was reachable
- The Wazuh manager was ready to receive agent data
- The macOS endpoint could be added as an agent

## Useful Commands

These are useful Linux commands for checking system and service status:

```bash
hostname -I
