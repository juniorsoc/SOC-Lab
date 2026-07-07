# Bash Operators — Redirection and Command Chaining

| Operator | Effect | Use case |
|----------|--------|----------|
| `>` | Overwrite file with output | Starting a fresh file |
| `>>` | Append output to file | Collecting results from multiple commands into one file |
| `&&` | Run next command only if previous succeeded | Safe multi-step sequences |
| `&` | Run command in background | Long-running tasks (e.g. continuous packet capture) that shouldn't block the terminal |

These let you chain a full analysis workflow in one line — search, save to file, run a follow-up command on that output — instead of doing each step manually.
