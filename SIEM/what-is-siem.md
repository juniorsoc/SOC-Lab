# SIEM Basics

**SIEM** (Security Information and Event Management) — collects, analyzes, and monitors logs from multiple sources so a SOC analyst can detect and investigate suspicious activity.

## How it works

| Step | What happens |
|------|--------------|
| Collect | Logs come in from servers, endpoints, firewalls, apps, network devices |
| Normalize | Different log formats get converted to a common format |
| Analyze | SIEM searches for suspicious patterns |
| Alert | A triggered rule generates an alert for analysts |

## Key terms

| Term | Meaning |
|------|---------|
| Event | A single recorded activity (e.g. a login attempt) |
| Alert | Notification about suspicious activity |
| Correlation rule | Combines multiple events to detect a threat |
| False positive | Looks suspicious but isn't a real attack |

## Common tools

Splunk, Microsoft Sentinel, IBM QRadar, Elastic SIEM, Wazuh.

## SOC analyst workflow

Receive alert → check logs → investigate → decide severity → document → escalate if needed.
