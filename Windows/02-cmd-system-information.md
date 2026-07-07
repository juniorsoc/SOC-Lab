# Windows CMD — Gathering System Information

Before troubleshooting/investigating an unfamiliar Windows machine, establish basic context first.

| Command | Tells you |
|---------|-----------|
| `whoami` | Current user + privilege level (SYSTEM/Admin = full control) |
| `hostname` | Machine name on the network — naming patterns can hint at its role (e.g. domain controller) |
| `systeminfo` | OS version, architecture, installed memory, last patch date — outdated patch date = possible known vulnerabilities |
| `ipconfig` | IP, subnet, gateway — can reveal unexpected adapters (e.g. a VPN tunnel that shouldn't be there) |

Typical order: identity/privilege → identify the machine → OS version/patch status → network configuration.
