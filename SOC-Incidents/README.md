# SOC Incidents

Incident reports and detection tests from my home SOC lab (Ubuntu + Wazuh target, MacBook attacker).

## Reports

- **ssh-bruteforce.md** - SSH failed login detection test using Wazuh. Manual failed-login check to confirm the detection pipeline (sshd/PAM/unix_chkpwd) works before running an automated brute-force simulation.
- **ubuntu-authentication-analysis.md** - Analysis of authentication events on the Ubuntu target.

## Environment

- Target: Ubuntu 26.04 LTS, Wazuh SIEM (indexer + manager + dashboard, all-in-one)
- Attacker: MacBook (macOS), same local network
- Each report includes: setup, test steps, detected Wazuh alerts (rule IDs), MITRE ATT&CK mapping, and lessons learned

## Status

Lab is a work in progress - adding new detection tests and attack simulations as I go.
