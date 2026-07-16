# TryHackMe — Linux Fundamentals Part 2 (Writeup)

**Status:** ✅ Complete

## Room Overview

This room builds on basic Linux navigation by covering remote access via SSH and core filesystem manipulation commands (creating, copying, moving, and removing files and directories).

## Task: Connecting via SSH

TryHackMe deploys two machines for this room: a target Linux VM and the TryHackMe AttackBox (a browser-based Ubuntu machine used to connect to the target).

To connect to the target machine over SSH from the AttackBox terminal:

```bash
ssh tryhackme@10.113.140.3
```

- `tryhackme` — username on the target VM
- `10.113.140.3` — target machine's IP (provided per-deployment on the room page; changes each time)
- Password prompt gives no visual feedback (no characters or placeholder symbols appear while typing) — this is normal SSH behavior, not a bug.

**Key concept:** SSH (Secure Shell) encrypts all traffic between the local and remote machine, so commands and credentials aren't sent in plaintext over the network — unlike older remote-access protocols like Telnet.

✅ Logged into the Linux Fundamentals Part 2 target machine via SSH.

## Task: Using the `man` Command

Learned how to look up documentation for any Linux command using its manual page:

```bash
man ls
```

This opens a paginated help document (man page) describing the command's purpose, syntax, and all available flags. Useful navigation inside `man`:

| Key | Action |
|---|---|
| `↓` (down arrow) | Scroll down the page |
| `q` | Quit / exit the man page |

Also covered `--help` as a quicker (less detailed) alternative for a summary of a command's options directly in the terminal, e.g. `ls --help`.

## Task: Filesystem Manipulation Commands

Covered the core set of commands for creating, copying, moving, and deleting files/folders:

| Command | Full Name | Purpose |
|---|---|---|
| `touch` | touch | Create an empty file |
| `mkdir` | make directory | Create a folder |
| `cp` | copy | Copy a file or folder |
| `mv` | move | Move (or rename) a file or folder |
| `rm` | remove | Delete a file or folder |
| `file` | file | Identify a file's type/content |

### Examples

```bash
touch newnote          # create an empty file called "newnote"
mkdir myfolder          # create a directory called "myfolder"
cp note note2            # copy "note" to a new file "note2"
mv myfile myfolder       # move "myfile" into "myfolder" (or rename if target isn't a directory)
rm note                  # delete a file
rm -R mydirectory        # delete a directory recursively (-R required for non-empty/dirs)
file unknown1            # inspect actual file type regardless of extension
```

**Key concept:** file extensions (`.txt`, `.sh`, etc.) are just naming conventions — they don't guarantee what a file actually contains. The `file` command inspects the file's actual content to determine its real type, which matters when you can't trust a filename at face value (e.g. during a CTF or on a compromised host).

### Flag Captured

Using `file` on `unknown1` in the target's home directory identified it as an ASCII text file. Reading its contents:

```
THM{FILESYSTEM}
```

## Task: File Permissions & Switching Users (`su`)

### Reading permissions with `ls -l`

```bash
ls -lh
```

```
-rw-r--r-- 1 cmnatic cmnatic 0 Feb 19 10:37 file1
```

The first column breaks down into four parts:

- 1st character — entry type (`-` = file, `d` = directory)
- Characters 2–4 — **owner** permissions
- Characters 5–7 — **group** permissions
- Characters 8–10 — **other** (everyone else) permissions

Each permission is one of:
- `r` = read
- `w` = write
- `x` = execute

**Detail that mattered for solving this task on my own:** `ls -l` also prints the file's **owner and group** as separate columns right after the permission string. That's the piece I had to recall from a different room — instead of opening the file to guess ownership, `ls -l <file>` answers "who owns this file" directly, without needing to read its contents.

### Symbolic → numeric permissions (for `chmod`)

| Permission | Value |
|---|---|
| r (read) | 4 |
| w (write) | 2 |
| x (execute) | 1 |

Sum the values per group (owner / group / other):

| Symbolic | Numeric | Meaning |
|---|---|---|
| `rwxrwxrwx` | 777 | Full access for everyone |
| `rwxr-xr-x` | 755 | Owner: full, others: read + execute |
| `rw-r--r--` | 644 | Owner: read/write, others: read only |
| `rwx------` | 700 | Owner-only access |

```bash
chmod 750 system_overview.txt
```
→ owner: full access, group: read + execute, other: no access

### Switching users with `su`

```bash
su user2          # switch user, keeps current user's working directory
su -l user2       # switch user with a full login shell — inherits user2's
                   # environment variables and drops you into their home dir
```

- `-l` / `--login` makes the session behave like an actual fresh login for that user (confirmed via `pwd` landing in `/home/user2` instead of the previous user's directory).
- `exit` returns to the previous session/user.

### Investigation trail (own reasoning, not directly prompted by the task)

```bash
tryhackme@linux2:~$ su -l user2
Password:
user2@linux2:~$ ls
user2@linux2:~$ su -l user1
su: user user1 does not exist
user2@linux2:~$ exit
logout
tryhackme@linux2:~$ ls
important  myfile  myfolder  unknown1
tryhackme@linux2:~$ cd important
-bash: cd: important: Not a directory
tryhackme@linux2:~$ ls -l important
-rw-r--r-- 1 user2 user2 14 May  5  2021 important
```

The task asked who owns the file `important` — rather than being told which command to use, I worked backward from `cd important` failing (it's a file, not a directory), then recalled `ls -l` from an earlier room as the way to inspect ownership without opening the file. `ls -l important` confirmed `user2` as both owner and group.

### Flag Captured

```bash
su -l user2   # password: user2
cat important
```
```
THM{SU_USER2}
```

## Task: Key System Directories

| Directory | Short for | Contents / Purpose |
|---|---|---|
| `/etc` | et cetera | System config files — e.g. `passwd`, `shadow`, `sudoers` |
| `/var` | variable | Data written frequently by services — e.g. logs in `/var/log` |
| `/root` | — | Home directory of the **root** user (not `/home/root`) |
| `/tmp` | temporary | Temporary/volatile data, wiped on reboot; world-writable by default |

- `/etc/passwd` — list of system users
- `/etc/shadow` — hashed user passwords (SHA-512)
- `/etc/sudoers` — users/groups permitted to run commands as root via `sudo`
- `/var/log` — where logs from running services and applications are stored
- `/root` — a common trap is assuming root's home is `/home/root`; it's actually its own top-level directory
- `/tmp` — behaves conceptually like RAM (cleared on restart); useful in pentesting as a default-writable location for enumeration scripts, etc.

## Commands Learned So Far

```
ssh, man, ls -a/-l, touch, mkdir, cp, mv, rm, file, su, su -l, chmod
```

## Key Takeaways

- Filesystem permissions (owner/group/other, `rwx`) and their numeric (`chmod`) equivalents are core building blocks for privilege-related enumeration later on.
- `ls -l` is a quick way to check file ownership without opening the file — useful habit for enumeration on real engagements.
- `/etc/passwd`, `/etc/shadow`, and `/etc/sudoers` are classic first-look files during Linux privilege escalation.
- `/tmp` being world-writable by default is a detail worth remembering for later offensive-security rooms (staging scripts, payloads, etc.).

---
*Part of a Linux Fundamentals series on TryHackMe, documenting core CLI skills before moving into more advanced security-focused rooms.*
