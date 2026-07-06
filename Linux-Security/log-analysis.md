# Linux Log Analysis

## Goal

Learn how to analyze Linux security events like a SOC analyst.

## Important log locations

Authentication logs:

/var/log/auth.log

System logs:

journalctl


## Useful commands

Show failed SSH logins:

grep "Failed password" /var/log/auth.log


Show successful logins:

grep "Accepted password" /var/log/auth.log


Show recent user activity:

last


## What a SOC analyst looks for

- Failed login attempts
- Unknown IP addresses
- Multiple login attempts
- Suspicious user activity# Linux Log Analysis

## Goal

Learn how to analyze Linux security events like a SOC analyst.

## Important log locations

Authentication logs:

/var/log/auth.log

System logs:

journalctl


## Useful commands

Show failed SSH logins:

grep "Failed password" /var/log/auth.log


Show successful logins:

grep "Accepted password" /var/log/auth.log


Show recent user activity:# Linux Log Analysis

## Goal

Learn how to analyze Linux security events like a SOC analyst.

## Important log locations

Authentication logs:

/var/log/auth.log

System logs:

journalctl


## Useful commands

Show failed SSH logins:

grep "Failed password" /var/log/auth.log


Show successful logins:

grep "Accepted password" /var/log/auth.log


Show recent user activity:

last


## What a SOC analyst looks for

- Failed login attempts
- Unknown IP addresses
- Multiple login attempts
- Suspicious user activity
