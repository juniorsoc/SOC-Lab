# SIEM Basics

## What is SIEM?

SIEM (Security Information and Event Management) is a security system used to collect, analyze and monitor logs from different sources.

SOC analysts use SIEM to detect suspicious activity and investigate security incidents.


## How SIEM works

1. Collect logs

SIEM receives data from:
- servers
- endpoints
- firewalls
- applications
- network devices


2. Normalize data

Different log formats are converted into a common format.


3. Analyze events

SIEM searches for suspicious patterns.


4. Generate alerts

When a rule is triggered, SIEM creates an alert for analysts.


## Important SIEM Terms

Event:
A single recorded activity.

Example:
User login attempt.


Alert:
A notification about suspicious activity.


Correlation rule:
A rule that combines multiple events to detect threats.


False Positive:
An alert that looks suspicious but is not a real attack.


## Examples of SIEM Tools

- Splunk
- Microsoft Sentinel
- IBM QRadar
- Elastic SIEM
- Wazuh


## SOC Analyst Workflow

1. Receive alert
2. Check logs
3. Investigate activity
4. Decide severity
5. Document findings
6. Escalate if needed
