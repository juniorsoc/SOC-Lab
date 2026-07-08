# Linux Log Analysis

## Goal

Analyze Linux security events like a SOC analyst.

## Important log locations

| Log | Location |
|-----|----------|
| Authentication | `/var/log/auth.log` |
| System | `journalctl` |

## Useful commands

| Command | Shows |
|---------|-------|
| `grep "Failed password" /var/log/auth.log` | Failed SSH logins |
| `grep "Accepted password" /var/log/auth.log` | Successful logins |
| `last` | Recent user activity |

## What a SOC analyst looks for

- Failed login attempts
- Unknown IP addresses
- Multiple login attempts in a short window
- Suspicious user activity
