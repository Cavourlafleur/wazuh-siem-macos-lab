# SOC 2 Control Mapping

## Objective

The objective of this document is to demonstrate how security controls implemented in the Wazuh lab support SOC 2 security requirements.

---

## Control 1 - Endpoint Monitoring

Security Control:

Endpoint monitoring and alerting.

Implementation:

Wazuh Agent installed on macOS endpoint.

Evidence:

File Integrity Monitoring alerts generated during testing.

Business Value:

Provides visibility into endpoint activity and unauthorized changes.

---

## Control 2 - Security Logging

Security Control:

Centralized logging.

Implementation:

Endpoint events forwarded to Wazuh Manager.

Evidence:

Security events visible in Wazuh Dashboard.

Business Value:

Supports investigations and incident response activities.

---

## Control 3 - Vulnerability Management

Security Control:

Identification of vulnerabilities.

Implementation:

Wazuh Vulnerability Detection.

Evidence:

Chrome vulnerabilities identified.

Adobe Acrobat vulnerabilities identified.

Wireshark vulnerabilities identified.

Business Value:

Helps reduce risk by identifying vulnerable software.

---

## Control 4 - Risk Assessment

Security Control:

Risk identification and remediation planning.

Implementation:

Risk register created from Wazuh findings.

Evidence:

Documented remediation recommendations.

Business Value:

Helps management understand and prioritize risk.

---

## Control 5 - Change Detection

Security Control:

Monitoring for unauthorized changes.

Implementation:

Wazuh File Integrity Monitoring.

Evidence:

File creation, modification, and deletion alerts.

Business Value:

Helps detect suspicious activity.

---

## What I Learned

SOC 2 is not just about tools.

SOC 2 is about demonstrating security controls, documenting evidence, and proving that security processes are operating effectively.
