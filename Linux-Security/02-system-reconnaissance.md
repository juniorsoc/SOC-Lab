# Linux System Reconnaissance

Before investigating any incident on an unfamiliar system, establish basic context first: who you're logged in as, what system this is, what state it's in.

| Command | Tells you |
|---------|-----------|
| `whoami` | Current username → privilege level |
| `uname -a` | Hostname, kernel version, architecture |
| `df -h` | Disk usage, readable format |
| `cat /etc/os-release` | Exact distro + version |

Files/dirs starting with a dot are hidden by default — a common place to conceal something. Need the extended listing option (`-a`) to see them.

Note: navigating into a hidden directory vs reading a hidden file are different operations — one changes location, the other displays content. Easy to mix up early on.

When searching the whole filesystem, permission errors are common for directories you can't access — suppress them so only real results show.

Typical recon order: identity/privilege → system/kernel info → disk space → distro confirmation → check commonly-abused locations (e.g. `/tmp/`) for anything suspicious.
