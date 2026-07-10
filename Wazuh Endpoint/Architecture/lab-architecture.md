
# Lab Architecture

## Project Name

Wazuh Endpoint Security, Vulnerability Management, and Compliance Lab

## Purpose

The purpose of this lab is to demonstrate how endpoint security monitoring works using Wazuh.

This lab shows how a security analyst can monitor an endpoint, review security events, identify vulnerabilities, document risk, and map technical security work to compliance frameworks such as SOC 2 and HIPAA.

## Lab Components

| Component | System | Purpose |
|---|---|---|
| Wazuh Manager | Ubuntu | Central security monitoring server |
| Wazuh Agent | macOS | Endpoint being monitored |
| Wazuh Dashboard | Browser-based UI | Used to view alerts, agents, vulnerabilities, and security events |
| GitLab | Documentation platform | Used to document the project for portfolio and interview use |

## High-Level Architecture

```text
+-------------------+          +-------------------------+
|                   |          |                         |
|   macOS Endpoint  |  ---->   |   Ubuntu Wazuh Manager  |
|   Wazuh Agent     |          |   Wazuh Server          |
|                   |          |                         |
+-------------------+          +-------------------------+
                                         |
                                         v
                              +---------------------+
                              |   Wazuh Dashboard   |
                              |   Analyst View      |
                              +---------------------+
