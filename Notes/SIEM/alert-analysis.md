# SIEM Alert Analysis

## Example: Multiple Failed SSH Logins

| Field | Value |
|-------|-------|
| Alert | Multiple Failed SSH Login Attempts |
| Severity | Medium |
| Detection | SIEM flagged multiple failed auth events |
| Log example | `Failed password for user admin from 192.168.1.50` |

**What to check:** affected user account, source IP, number of failed attempts, time window, whether a successful login followed the failures.

**Investigation steps:**
1. Check auth logs (`/var/log/auth.log`)
2. Identify source IP — known or suspicious?
3. Look for a successful login after the failures — possible sign of compromise

**Possible causes:** user forgot password, automated login attempt, brute force attack.

**Response if confirmed malicious:** block source IP, reset compromised password, escalate, document findings.

**Skills practiced:** alert triage, log analysis, incident investigation, documentation.
