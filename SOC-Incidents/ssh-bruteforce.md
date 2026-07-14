# SSH Failed Login Test - Wazuh Detection Check

## What I did

Before running a real brute-force attack with Hydra, I wanted to first check if Wazuh actually picks up failed SSH logins at all. No point running a big automated attack if the basic detection isn't even working.

So I did a simple manual test: tried to SSH into my Ubuntu box from my MacBook using the right username but a wrong password, and checked if anything showed up in the Wazuh dashboard.

## Setup

- Target: Ubuntu 26.04 LTS, running Wazuh (indexer + manager + dashboard, all installed on the same machine - "all-in-one" setup)
- Attacker: MacBook (macOS), same home network
- Service: SSH, port 22

## The test

From the MacBook:

```bash
ssh onfroy@192.168.1.14
```

Typed in a wrong password on purpose.

## What Wazuh caught

Went into the dashboard (Threat Hunting section) and found the failed login showed up as three separate alerts, all pretty much at the same timestamp:

**Rule 5760** - `sshd: authentication failed.` (level 5)
This is the SSH daemon itself logging that the password was wrong.

**Rule 5557** - `unix_chkpwd: Password check failed.` (level 5)
This is a lower-level Linux tool that actually checks the password, confirming the same thing.

**Rule 5503** - `PAM: User login failed.` (level 5)
PAM (Linux's authentication system) also logged the failed login attempt.

So one wrong password attempt = 3 correlated log entries, which was actually interesting to see - I didn't realize one failed login triggers that many separate log sources.

Timeline (from the dashboard):
16:09:19 - PAM: User login failed
16:09:19 - unix_chkpwd: Password check failed
16:09:21 - sshd: authentication failed
16:09:27 - unix_chkpwd: Password check failed
16:09:29 - sshd: authentication failed## MITRE ATT&CK

This maps to **T1110.001 - Password Guessing** under Credential Access. It's a single manual attempt rather than an automated attack, but it's the same category of technique - just smaller scale.

## Notes / what I learned

- Detection pipeline works - Wazuh is correctly catching failed SSH logins on this host
- No successful login happened, no compromise, this was just a check
- Now that I know the basic detection works, next step is to actually run Hydra with a small password list and see how the alerts look different at scale (probably a lot more of rule 5760 in a short time window, maybe a brute-force correlation rule kicking in too)
- Good practice I picked up: check that your monitoring actually works *before* running the real attack simulation, otherwise you don't know if "no alerts" means "nothing happened" or "detection is broken"

## Basic mitigations (for a real environment, not needed in this lab)

- SSH key-based auth instead of passwords
- Fail2ban or similar
- Rate limiting / account lockout after repeated failures
- Restrict SSH access by IP/firewall
