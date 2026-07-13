# Company Profile and Compliance Scope

## Company Name
HopeHealth AI

## Industry
Healthtech

## Business Description
HopeHealth AI is a small healthtech startup that provides a web-based patient intake platform. The platform may process sensitive personal and health-related information.

## Compliance Goal
The company wants to improve security maturity and prepare for customer security reviews and compliance readiness activities.

## In-Scope Systems
The following systems are included in this lab:

| System | Description |
|---|---|
| Wazuh Manager | Central security monitoring platform |
| Linux Endpoint | Monitored endpoint with Wazuh agent installed |
| User Authentication Logs | Login and failed login events |
| File Integrity Monitoring | Monitoring of selected files and directories |
| Vulnerability Detection | Endpoint vulnerability visibility |
| Security Configuration Assessment | Endpoint configuration review |

## Out-of-Scope Systems
The following are not included in this lab:

| System | Reason |
|---|---|
| Production EHR system | Not used in this home lab |
| Real patient data | No real sensitive data is used |
| Live customer environment | This is a simulated readiness lab |

## Important Note
This project does not claim that HopeHealth AI is certified or compliant. It demonstrates how Wazuh can support compliance readiness by producing technical security evidence.
