# Windows Terminal — CMD Navigation

CLI gives more precise control than GUI folders, and is often the only option when investigating a remote system without graphical access.

| Command | Linux equivalent | Does |
|---------|-------------------|------|
| `cd` | `pwd` / `cd` | Shows current dir / changes dir |
| `dir` | `ls` | Lists folder contents |
| `dir /a` | `ls -a` | Also shows hidden files/folders |
| `dir /s filename` | `find` | Searches recursively for a file |
| `type` | `cat` | Displays file contents |

Windows hides some files by default — a technique sometimes used to conceal malicious files. Always check hidden content during an investigation, don't rely on a default listing.

Typical sequence: confirm current location → list contents (incl. hidden) → search broader if not found nearby → navigate to it → display contents.
