# Linux System Reconnaissance

Before investigating any incident on an unfamiliar system, an analyst first establishes the basic context of what they're actually working with — who they're logged in as, what system this is, and what state it's currently in.

The `whoami` command reports the currently active username, which establishes the privilege level available for the rest of the investigation. The `uname -a` command reports detailed information about the system and kernel, including the hostname, kernel version, and system architecture, giving a fuller picture of exactly what's running. The `df -h` command reports disk usage in a readable format, showing how much space is used and available across the system's storage. The `cat /etc/os-release` command reveals precisely which Linux distribution and version is installed, which matters since different distributions organize their filesystems and default configurations somewhat differently.

Files and directories whose names begin with a dot are hidden by default and won't appear in a standard directory listing — a fact worth remembering, since hidden files are also a common place for something to be deliberately concealed. Revealing them requires an extended listing option rather than the default command. It's also worth noting that navigating into a hidden directory and reading a hidden file are different operations entirely — one changes the current working directory, the other displays the contents of a specific file, and confusing the two is a common early mistake.

When searching across the filesystem for a specific file, it's common to encounter permission errors for directories the current user isn't allowed to access. These errors can be suppressed so that only genuine results are displayed, which keeps the output focused and readable rather than cluttered with noise from inaccessible locations.

A typical reconnaissance sequence on an unfamiliar system proceeds roughly in this order: establish identity and privilege level, gather system and kernel details, check available disk space, confirm the specific distribution in use, and finally review commonly abused locations such as temporary directories for anything suspicious.

## Practical Example — Full Recon Sequence

```bash
$ whoami && uname -a && df -h && cat /etc/os-release
ubuntu
Linux tryhackme 6.2.0-39-generic #40-Ubuntu x86_64 GNU/Linux
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda1       20G   14G  5.2G  73% /
PRETTY_NAME="Ubuntu 22.04.3 LTS"

$ ls -al /tmp/
drwxrwxrwt  4 root   root   4096 Jul  7 09:12 .
drwxr-xr-x 5 ubuntu ubuntu 4096 Jul  7 08:40 .research
-rwxr-xr-x 1 root   root  45232 Jul  7 03:14 .hidden_backdoor
```

Running the four recon commands chained together gives a fast snapshot of the system. The `/tmp/` listing then reveals two hidden items a plain `ls` would have missed entirely — a `.research` folder and a suspiciously named executable, `.hidden_backdoor`, both invisible without the `-a` flag.
