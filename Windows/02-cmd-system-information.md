# Windows CMD — System Information

| Command | Checks | Linux equivalent |
|---|---|---|
| `whoami` | Current user/privileges | `whoami` |
| `hostname` | Machine name | `hostname` |
| `systeminfo` | OS version, architecture, RAM, patch date | `uname -a` |
| `ipconfig` | IP, gateway, network config | `ip a` |

**SOC relevance:** `whoami` reveals privilege escalation to SYSTEM; `systeminfo` reveals outdated/vulnerable versions; `ipconfig` can reveal suspicious VPN adapters set up by an attacker.
