
---

## Important File Locations

### Ubuntu Wazuh Manager

| File | Purpose |
|---|---|
| `/var/ossec/etc/ossec.conf` | Main manager config |
| `/var/ossec/etc/rules/local_rules.xml` | Local custom rules |
| `/var/ossec/logs/alerts/alerts.json` | JSON alerts |
| `/var/ossec/logs/alerts/alerts.log` | Plain text alerts |
| `/var/ossec/bin/agent_control` | Manage agents |

### macOS Wazuh Agent

| File | Purpose |
|---|---|
| `/Library/Ossec/etc/ossec.conf` | Main agent config |
| `/Library/Ossec/logs/ossec.log` | Agent log file |
| `/Library/Ossec/bin/wazuh-control` | Start/stop/restart agent |
| `/Library/Ossec/ruleset/sca` | SCA policies on macOS |

---

## 1. File Integrity Monitoring (FIM)

FIM watches files and directories for changes — creation, modification, deletion, and unauthorized tampering.

**GRC value:** Supports change monitoring, system integrity, and audit controls.

| Framework | How FIM Helps |
|---|---|
| SOC 2 | Change and security monitoring |
| HIPAA | Integrity and audit controls |
| ISO 27001 | Change control |
| NIST | System integrity monitoring |
| GDPR | Protects personal data systems |

**Open the config file:**
```bash
sudo nano /Library/Ossec/etc/ossec.conf
```

**FIM configuration block:**
```xml
<syscheck>
  <disabled>no</disabled>
  <frequency>86400</frequency>
  <scan_on_start>yes</scan_on_start>
  <directories realtime="yes" check_all="yes" report_changes="yes">/Users/lafleur/wazuh-fim-lab</directories>
</syscheck>
```

| Setting | Meaning |
|---|---|
| `disabled: no` | FIM is enabled |
| `frequency: 86400` | Scans every 24 hours |
| `scan_on_start: yes` | Scans when agent starts |
| `realtime: yes` | Detects changes instantly |
| `report_changes: yes` | Reports content changes |

**Create the monitored folder:**
```bash
mkdir -p ~/wazuh-fim-lab
```

**Create a test file:**
```bash
echo "This is my first Wazuh FIM test file" > ~/wazuh-fim-lab/test-file.txt
```

**List files with detail:**
```bash
ls -la ~/wazuh-fim-lab
```

**Check current username (needed for full path):**
```bash
whoami
```

**Restart the agent to apply changes:**
```bash
sudo /Library/Ossec/bin/wazuh-control restart
```

**Check agent status:**
```bash
sudo /Library/Ossec/bin/wazuh-control status
```

**Trigger a file creation alert:**
```bash
echo "New sensitive document" > ~/wazuh-fim-lab/sensitive-note.txt
```

**Trigger a file modification alert:**
```bash
echo "Unauthorized change test" >> ~/wazuh-fim-lab/sensitive-note.txt
```

**Trigger a file deletion alert:**
```bash
rm ~/wazuh-fim-lab/sensitive-note.txt
```

**GRC Evidence Statement:** Wazuh FIM was configured to monitor a test directory on the macOS endpoint. Alerts were generated for creation, modification, and deletion — supporting change and integrity monitoring.

---

## 2. Vulnerability Detection

Wazuh collects software inventory from the agent and correlates it against known vulnerability feeds.

| Framework | How It Helps |
|---|---|
| SOC 2 | Risk mitigation |
| HIPAA | Security management process |
| ISO 27001 | Vulnerability management |
| NIST | Risk assessment |
| GDPR | Security risk reduction |

**Open manager config:**
```bash
sudo nano /var/ossec/etc/ossec.conf
```

**Vulnerability detection block:**
```xml
<vulnerability-detection>
  <enabled>yes</enabled>
  <index-status>yes</index-status>
  <feed-update-interval>60m</feed-update-interval>
</vulnerability-detection>
```

**Restart the manager:**
```bash
sudo systemctl restart wazuh-manager
```

**Check manager status:**
```bash
sudo systemctl status wazuh-manager
```

**Check installed app versions on macOS:**
```bash
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --version
```

```bash
/Applications/Wireshark.app/Contents/MacOS/Wireshark --version
```

```bash
python3 -m pip show setuptools
```

**Upgrade a vulnerable package:**
```bash
python3 -m pip install --upgrade setuptools
```

**GRC Evidence Statement:** Wazuh identified vulnerable software on the macOS endpoint (Chrome, Adobe Acrobat, Wireshark, setuptools). Findings were reviewed, patched, and validated.

---

## 3. Security Configuration Assessment (SCA)

SCA checks systems against secure configuration baselines (mostly CIS benchmarks).

**Open agent config:**
```bash
sudo nano /Library/Ossec/etc/ossec.conf
```

**SCA configuration block:**
```xml
<sca>
  <enabled>yes</enabled>
  <scan_on_start>yes</scan_on_start>
  <interval>12h</interval>
  <skip_nfs>yes</skip_nfs>
</sca>
```

**List SCA policies on macOS:**
```bash
ls -la /Library/Ossec/ruleset/sca
```

**Restart the agent:**
```bash
sudo /Library/Ossec/bin/wazuh-control restart
```

**GRC Evidence Statement:** SCA reviewed endpoint configuration settings. Failed checks were logged as compliance gaps for remediation tracking.

---

## 4. Authentication Monitoring

Reviews login activity: successful logins, failed logins, sudo usage, privilege escalation.

**Search for sudo alerts:**
```bash
sudo grep -i "sudo" /var/ossec/logs/alerts/alerts.json | tail -n 10
```

**Search for failed activity:**
```bash
sudo grep -i "failed" /var/ossec/logs/alerts/alerts.json | tail -n 10
```

**Search for authentication events:**
```bash
sudo grep -i "authentication" /var/ossec/logs/alerts/alerts.json | tail -n 10
```

**Format sudo alerts with jq:**
```bash
sudo grep -i "sudo" /var/ossec/logs/alerts/alerts.json | jq '{timestamp: .timestamp, agent: .agent.name, rule_id: .rule.id, rule_level: .rule.level, description: .rule.description, full_log: .full_log}'
```

**Example alert fields found in lab:**

| Field | Value |
|---|---|
| rule_id | 5402 |
| rule_level | 3 |
| description | Successful sudo to ROOT executed |
| decoder | sudo |
| location | journald |

**GRC Evidence Statement:** Authentication monitoring provides evidence of login and privilege activity, supporting logical access control review.

---

## 5. Security Alerts

**Alert storage on Ubuntu Manager:**
```text
/var/ossec/logs/alerts/alerts.json
/var/ossec/logs/alerts/alerts.log
```

**Alert threshold configuration:**
```xml
<alerts>
  <log_alert_level>3</log_alert_level>
  <email_alert_level>12</email_alert_level>
</alerts>
```

**View last 20 alerts:**
```bash
sudo tail -n 20 /var/ossec/logs/alerts/alerts.json
```

**Watch alerts live:**
```bash
sudo tail -f /var/ossec/logs/alerts/alerts.json
```

**Search for rootcheck alerts:**
```bash
sudo grep -i "rootcheck" /var/ossec/logs/alerts/alerts.json | tail -n 10
```

**Count alerts mentioning port 55555:**
```bash
sudo grep -i "55555" /var/ossec/logs/alerts/alerts.json | wc -l
```

**Extract readable fields with jq:**
```bash
sudo grep -i "55555" /var/ossec/logs/alerts/alerts.json | jq '{timestamp: .timestamp, agent: .agent.name, rule_id: .rule.id, rule_level: .rule.level, full_log: .full_log}'
```

**Key alert fields:**

| Field | Meaning |
|---|---|
| timestamp | When it happened |
| agent.name | Which endpoint |
| rule.id | Which rule triggered |
| rule.level | Severity |
| full_log | Raw alert message |

**SOC analyst alert formula:**
```text
WHO + WHAT + WHERE + WHEN + SEVERITY + IMPACT + ACTION
```

---

## 6. Malware Detection and Rootcheck

Rootcheck detects anomalies that might indicate malware or rootkits, including hidden ports.

**Example lab alert:**
```text
Port '55555'(tcp) hidden. Kernel-level rootkit or trojaned version of netstat.
```

**List user LaunchAgents (macOS):**
```bash
ls -la ~/Library/LaunchAgents
```

**List system LaunchAgents:**
```bash
ls -la /Library/LaunchAgents
```

**List system LaunchDaemons:**
```bash
ls -la /Library/LaunchDaemons
```

**Search agent logs for the alert:**
```bash
grep -i "55555\|rootcheck\|hidden" /Library/Ossec/logs/ossec.log | tail -n 30
```

**Extract timestamps of matching alerts (manager):**
```bash
sudo grep -i "55555" /var/ossec/logs/alerts/alerts.json | grep -o '"timestamp":"[^"]*"'
```

**Filter to only real rootcheck alerts:**
```bash
sudo grep -i "55555" /var/ossec/logs/alerts/alerts.json | jq 'select(.decoder.name=="rootcheck") | {timestamp: .timestamp, agent: .agent.name, rule_id: .rule.id, rule_level: .rule.level, full_log: .full_log}'
```

**GRC Evidence Statement:** The alert was investigated and classified as a likely false positive, supporting incident response documentation.

---

## 7. Incident Response Evidence Template

**Alert:** Rootcheck Hidden Port Alert
**Source:** Wazuh Rootcheck
**Endpoint:** Lafleur.local
**Message:** Port '55555'(tcp) hidden. Kernel-level rootkit or trojaned version of netstat.
**Rule ID:** 510
**Rule Level:** 7

**What happened:** Wazuh flagged TCP port 55555 as hidden.

**Why it was suspicious:** Hidden ports can indicate malware or rootkits hiding communication.

**Investigation steps:**

1. Reviewed the alert in `alerts.json`
2. Confirmed the alert source was rootcheck
3. Counted occurrences of the port 55555 alert
4. Extracted timestamps
5. Reviewed Wazuh agent logs on macOS
6. Reviewed LaunchAgents and LaunchDaemons for persistence
7. Determined whether supporting evidence existed

**Commands used:**
```bash
sudo grep -i "55555" /var/ossec/logs/alerts/alerts.json | tail -n 5
```

```bash
sudo grep -i "55555" /var/ossec/logs/alerts/alerts.json | wc -l
```

```bash
grep -i "55555\|rootcheck\|hidden" /Library/Ossec/logs/ossec.log | tail -n 30
```

**Analyst decision:** Likely false positive.

**Reason:** No supporting evidence of malware, persistence, or repeated malicious behavior was found.

**Recommendation:** Continue monitoring; do not disable the rule without approval. Document repeats as known false positives.

---

## 8. Rule Tuning and False Positive Handling

**Key principle:** Never blindly disable a security rule. Investigate first, document, get approval, scope narrowly, and review later.

**Open local rules file (manager):**
```bash
sudo nano /var/ossec/etc/rules/local_rules.xml
```

**Example narrowly-scoped local rule:**
```xml
<group name="local,rootcheck,">
  <rule id="100510" level="0">
    <if_sid>510</if_sid>
    <match>Port '55555'(tcp) hidden</match>
    <description>Known lab false positive for hidden TCP port 55555 on macOS endpoint.</description>
  </rule>
</group>
```

**Restart manager after editing:**
```bash
sudo systemctl restart wazuh-manager
```

---

## 9. Rootcheck Scan Timing

**Rootcheck config block:**
```xml
<rootcheck>
  <disabled>no</disabled>
  <check_files>yes</check_files>
  <check_trojans>yes</check_trojans>
  <check_ports>yes</check_ports>
  <frequency>86400</frequency>
  <skip_nfs>yes</skip_nfs>
</rootcheck>
```

**Temporary testing workflow:**

1. Change `frequency` to `60` (seconds)
2. Restart agent
3. Wait for scan to run
4. Review alerts
5. Change `frequency` back to `86400`
6. Restart agent again

```bash
sudo nano /Library/Ossec/etc/ossec.conf
```

```bash
sudo /Library/Ossec/bin/wazuh-control restart
```

---

## 10. Manager Commands Cheat Sheet

```bash
sudo systemctl status wazuh-manager
```

```bash
sudo systemctl restart wazuh-manager
```

```bash
sudo systemctl status wazuh-dashboard
```

```bash
sudo systemctl status wazuh-indexer
```

```bash
sudo /var/ossec/bin/agent_control -l
```

```bash
sudo /var/ossec/bin/agent_control -lc
```

```bash
sudo /var/ossec/bin/agent_control -i 001
```

---

## 11. macOS Agent Commands Cheat Sheet

```bash
sudo /Library/Ossec/bin/wazuh-control status
```

```bash
sudo /Library/Ossec/bin/wazuh-control restart
```

```bash
tail -f /Library/Ossec/logs/ossec.log
```

```bash
sudo nano /Library/Ossec/etc/ossec.conf
```

```bash
ls -la ~/Library/LaunchAgents
```

```bash
ls -la /Library/LaunchAgents
```

```bash
ls -la /Library/LaunchDaemons
```

---

## 12. Compliance Control Mapping

| Wazuh Feature | GRC Control Area | Compliance Meaning |
|---|---|---|
| FIM | Change monitoring | File changes can be detected |
| Vulnerability Detection | Vulnerability management | Known weaknesses identified |
| SCA | Secure configuration | Systems checked against baseline |
| Authentication Monitoring | Access monitoring | Login activity reviewable |
| Security Alerts | Security monitoring | Events centrally monitored |
| Rootcheck | Anomaly detection | Suspicious behavior reviewed |
| Incident Response Notes | Incident response | Alerts triaged and documented |

---

## 13. Risk Register

| Risk ID | Finding | Impact | Likelihood | Rating |
|---|---|---|---|---|
| R-001 | FIM alert | High | Medium | High |
| R-002 | Vulnerability findings | High | Medium | High |
| R-003 | SCA failed checks | Medium | Medium | Medium |
| R-004 | Authentication alerts | Medium | Medium | Medium |
| R-005 | Rootcheck hidden port | High | Low | Medium |
| R-006 | Alerts not reviewed | High | Medium | High |

---

## 14. Gap Analysis

- **Alert review process** needs formal documentation
- **Vulnerability remediation** needs assigned ownership
- **FIM scope** needs clearly defined critical directories
- **SCA failures** need tracking until closure
- **Incident response notes** need a standardized template


