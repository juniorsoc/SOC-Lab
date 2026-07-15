# TryHackMe — Linux Fundamentals Part 2 (Writeup)

**Status:** 🚧 In Progress — will be completed as more tasks are finished

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

## Commands Learned So Far

```
ssh, man, touch, mkdir, cp, mv, rm, file
```

## Next Steps

More tasks from this room to be added — likely covering further filesystem operations and possibly permissions/redirection, depending on how the room progresses.

---
*Part of a Linux Fundamentals series on TryHackMe, documenting core CLI skills before moving into more advanced security-focused rooms.*
