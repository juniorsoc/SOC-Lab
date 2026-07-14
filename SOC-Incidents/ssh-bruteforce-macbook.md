# SSH Brute Force Detection - macOS Attack Simulation

## Incident Overview

A simulated SSH brute force attack was performed from a MacBook device against an Ubuntu Linux system monitored by Wazuh SIEM.

The purpose of this experiment was to test SSH authentication monitoring, log collection, detection rules, and incident investigation workflow in a SOC environment.

---

## Environment

### Target System

- Operating System: Ubuntu Linux
- SIEM Platform: Wazuh
- Log Source: SSH authentication logs (/var/log/auth.log)
- Detection Engine: Wazuh Rules Engine

### Source System

- Device: MacBook (macOS)
- Source IP Address: 192.168.1.28

---

## Attack Simulation

The attack simulation was performed from a MacBook by generating multiple failed SSH login attempts against the Ubuntu host.

Command used:

```bash
ssh fakeuser@TARGET_IP he test used a non-existent username and incorrect authentication attempts to simulate password guessing activity.

Example log event:

Failed password for invalid user fakeuser from 192.168.1.28 port 59406 ssh2
Detection

The Wazuh SIEM successfully detected the suspicious SSH authentication activity.

Detected alerts:

Rule ID: 5710

Description:

sshd: Attempt to login using a non-existent user.

Severity:

Level 5

Meaning:

A login attempt was made using an account that does not exist on the system.

Rule ID: 2502

Description:

User missed the password more than one time.

Severity:

Level 10

Meaning:

Multiple failed authentication attempts were detected, indicating possible password guessing activity.

Rule ID: 5712

Description:

sshd: brute force trying to get access to the system. Non existent user.

Severity:

Level 10

Meaning:

Wazuh correlated multiple failed SSH attempts and classified the behavior as a possible brute force attack.

Investigation

The following indicators were analyzed during the investigation.

Source IP Address
192.168.1.28

The source IP belongs to the testing MacBook device that generated the SSH authentication attempts.

Target Username
fakeuser

The attacker attempted to authenticate using a non-existent account.

Using invalid usernames is a common technique during automated SSH attacks because attackers often test common account names.

Target Service
SSH
Port: 22

SSH is a common attack target because it provides remote access to Linux systems.

Timeline

Example attack timeline:

20:25:34 - Failed SSH login attempt detected
20:25:40 - Multiple authentication failures detected
20:25:54 - Wazuh detected possible brute force activity
20:26:24 - SSH connection closed after failed authentication
MITRE ATT&CK Mapping

Technique:

T1110 - Brute Force

Tactic:

Credential Access

Attackers use brute force techniques to gain unauthorized access by repeatedly attempting different passwords or usernames.

Analyst Assessment

The activity matched the behavior of an SSH brute force attack simulation.

The attack was detected successfully by Wazuh before any unauthorized access occurred.

No successful authentication was observed.

Incident classification:

Severity: Medium
Status: Investigated
Result: No compromise detected
Recommended Mitigations

Recommended defensive actions:

Disable SSH password authentication when possible.
Use SSH key-based authentication.
Restrict SSH access using firewall rules.
Monitor repeated authentication failures.
Implement fail2ban or similar protection.
Disable unnecessary user accounts.
Lessons Learned

This experiment demonstrated the complete SOC workflow:

Generate a simulated attack.
Collect authentication logs.
Detect suspicious activity using SIEM rules.
Investigate indicators of compromise.
Map activity to MITRE ATT&CK.
Document findings.

The Wazuh SIEM successfully detected SSH brute force behavior originating from an external device and provided sufficient information for investigation and response.
