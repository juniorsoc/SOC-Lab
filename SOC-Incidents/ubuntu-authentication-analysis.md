# Ubuntu Authentication Log Analysis

## Objective

Analyze authentication events and privileged activity from Ubuntu authentication logs to determine whether suspicious behavior occurred.

## Environment

Operating System:
Ubuntu Linux

Log Source:

/var/log/auth.log

Tools Used:

- grep
- awk
- sort
- uniq


# Investigation Steps

## 1. Authentication Failure Analysis

Command used:

    grep -i "failed" /var/log/auth.log

Finding:

Observed failed password verification attempts for local user:

    unix_chkpwd: password check failed for user (onfroy)

Analysis:

The events indicate unsuccessful password verification.

No indicators of brute force activity were identified.

Observed:

- No source IP address
- No SSH authentication attempts
- No repeated login attempts in a short time period


## 2. Successful Session Analysis

Command used:

    grep -i "session opened" /var/log/auth.log

Finding:

Detected sessions related to:

- Local user login
- Sudo privilege elevation
- System services
- Cron tasks

Analysis:

The activity was consistent with normal local system administration.

No unauthorized remote sessions were identified.


## 3. Privileged Command Analysis

Command used:

    grep "COMMAND=" /var/log/auth.log

Finding:

Observed commands:

    apt update
    apt install github-desktop
    apt install nmap
    apt install tcpdump
    apt install git

Analysis:

Commands were executed through sudo by the local user.

Activity matched:

- System configuration
- Software installation
- Security lab preparation


# Indicators of Compromise

No Indicators of Compromise (IOC) identified.

Not observed:

- SSH brute force
- Unauthorized remote access
- Suspicious privilege escalation
- Suspicious binaries


# Conclusion

Based on the available authentication logs, no indicators of compromise were identified.

The observed activity appears consistent with legitimate local administrative actions performed by the system owner.
