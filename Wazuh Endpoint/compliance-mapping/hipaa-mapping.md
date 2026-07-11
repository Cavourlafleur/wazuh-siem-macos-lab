# HIPAA Security Rule Mapping

## Objective

The objective of this document is to explain how my Wazuh lab supports HIPAA Security Rule concepts.

This lab does not use real patient data. Instead, it demonstrates how endpoint monitoring, vulnerability management, logging, and risk documentation could support HIPAA security safeguard activities in a healthcare environment.

## What Is HIPAA Security Rule?

HIPAA Security Rule focuses on protecting electronic protected health information, also called ePHI.

The rule includes three major safeguard categories:

- Administrative Safeguards
- Physical Safeguards
- Technical Safeguards

## Lab Environment

| Component | Purpose |
|---|---|
| macOS Endpoint | Simulated workstation |
| Wazuh Agent | Endpoint monitoring |
| Ubuntu Wazuh Manager | Central security monitoring server |
| Wazuh Dashboard | Alert and vulnerability review |
| GitLab | Documentation and evidence repository |

---

## HIPAA Mapping 1 - Audit Controls

### HIPAA Concept

Audit controls help organizations record and examine activity in systems that contain or use ePHI.

### Wazuh Lab Control

Wazuh collects endpoint security events from the macOS agent and sends them to the Wazuh Manager.

### Evidence From Lab

- File Integrity Monitoring alerts
- Endpoint security events
- Vulnerability findings
- Wazuh dashboard screenshots

### Why This Matters

If an endpoint is used in a healthcare environment, audit logs help analysts review activity and investigate suspicious behavior.

---

## HIPAA Mapping 2 - Integrity

### HIPAA Concept

Integrity means protecting electronic information from improper alteration or destruction.

### Wazuh Lab Control

Wazuh File Integrity Monitoring detects when monitored files are created, modified, or deleted.

### Evidence From Lab

In the endpoint monitoring lab, I created, modified, and deleted files inside a monitored folder. Wazuh detected those changes.

### Why This Matters

If important files are changed without approval, it could indicate tampering, malware activity, or unauthorized access.

---

## HIPAA Mapping 3 - Security Management Process

### HIPAA Concept

Security management includes identifying risks and implementing security measures to reduce those risks.

### Wazuh Lab Control

Wazuh Vulnerability Detection identified high severity vulnerabilities on the macOS endpoint.

### Evidence From Lab

Wazuh identified high severity findings affecting:

- Chrome
- Adobe Acrobat
- Wireshark
- setuptools

### Why This Matters

Healthcare organizations need to identify weaknesses before attackers exploit them.

---

## HIPAA Mapping 4 - Risk Analysis

### HIPAA Concept

Risk analysis means reviewing possible threats and vulnerabilities that could affect sensitive systems.

### Wazuh Lab Control

I reviewed Wazuh vulnerability findings and documented risk using a sample risk register.

### Evidence From Lab

The risk register included:

- Asset
- Vulnerability
- Severity
- Threat
- Business impact
- Remediation recommendation
- Status

### Why This Matters

Risk analysis helps security teams decide what needs to be fixed first.

---

## HIPAA Mapping 5 - Workstation Security

### HIPAA Concept

Workstation security focuses on protecting workstations that may access electronic protected health information.

### Wazuh Lab Control

The macOS endpoint was monitored by the Wazuh agent.

### Evidence From Lab

The Wazuh Dashboard showed the macOS endpoint as a monitored agent.

### Why This Matters

Endpoint monitoring helps security teams maintain visibility into workstation activity.

---

## HIPAA Mapping 6 - Vulnerability Remediation

### HIPAA Concept

HIPAA does not say “use Wazuh,” but it expects organizations to protect systems and manage security risks.

### Wazuh Lab Control

Wazuh helped identify vulnerable software installed on the endpoint.

### Evidence From Lab

High severity vulnerabilities were grouped by affected software:

| Software | Finding Count |
|---|---|
| Chrome | 16 |
| Adobe Acrobat full app | 15 |
| Adobe Acrobat mini app | 15 |
| setuptools | 6 |
| Wireshark | 4 |

### Recommended Remediation

| Software | Action |
|---|---|
| Chrome | Update Chrome to latest version |
| Adobe Acrobat | Update Adobe Acrobat |
| Wireshark | Upgrade Wireshark |
| setuptools | Upgrade Python setuptools package |

---

