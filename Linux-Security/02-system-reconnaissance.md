# Linux System Reconnaissance

Typical recon order on an unfamiliar system:

```
whoami                  → who am I
uname -a                → system/kernel info
df -h                   → disk usage
cat /etc/os-release     → distro
ls -al /tmp/            → check for suspicious files
```

**Hidden files** (starting with `.`) don't show with plain `ls` — use `ls -al`. Never `cd` into a file; only into directories.

**Suppress permission errors while searching:**
```bash
find / -name file.txt 2>/dev/null
```
