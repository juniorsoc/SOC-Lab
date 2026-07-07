# Windows CMD Navigation

| Command | Does | Linux equivalent |
|---|---|---|
| `cd` | Show current dir | `pwd` |
| `dir` | List contents | `ls` |
| `dir /a` | List including hidden | `ls -al` |
| `dir /s file` | Search subfolders | `find / -name file` |
| `type file` | Show file contents | `cat file` |

**Note:** hidden ≠ secret — always use `dir /a` during analysis, since attackers commonly hide files this way.
