# Incident Report

## Incident Title

SSH Brute Force Attack


## Severity

Medium


## Detection

Detected by SIEM alert:

Multiple Failed SSH Login Attempts


## Timeline

Example:

12:00 - Multiple failed SSH login attempts detected

12:05 - Source IP identified

12:10 - Authentication logs reviewed


## Indicators of Compromise (IoC)

Source IP:
Unknown

Target User:
root/admin

Attack Type:
Brute Force


## Investigation

Checked:

- authentication logs
- source IP address
- login attempts
- successful logins after failed attempts


## Analysis

Multiple failed SSH login attempts indicate a possible brute force attack.

The attacker attempted to gain unauthorized access to the system.


## Response Actions

Actions taken:

- Block suspicious IP address
- Monitor authentication logs
- Review affected accounts


## Recommendations

- Use strong passwords
- Enable MFA
- Disable root login over SSH
- Monitor authentication events
