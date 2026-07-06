# SIEM Alert Analysis

## Example Alert: Multiple Failed SSH Logins

### Alert Name

Multiple Failed SSH Login Attempts


### Severity

Medium


### Detection Source

SIEM detected multiple failed authentication events.


### Log Example

Failed password for user admin from 192.168.1.50


### Analysis

SOC analyst checks:

- affected user account
- source IP address
- number of failed attempts
- time period
- successful login after failures


### Investigation Steps

1. Check authentication logs

Example:

/var/log/auth.log


2. Identify source IP

Check if IP is known or suspicious.


3. Look for successful login

A successful login after many failed attempts can indicate account compromise.


### Possible Causes

- User forgot password
- Automated login attempt
- Brute force attack


### Response

If malicious activity is confirmed:

- block source IP
- reset compromised password
- escalate incident
- document findings


## SOC Skills Practiced

- Alert triage
- Log analysis
- Incident investigation
- Documentation

