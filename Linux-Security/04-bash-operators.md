# Bash Operators

| Operator | Behavior | Use case |
|---|---|---|
| `>` | Overwrites file | Fresh report |
| `>>` | Appends to file | Aggregating results |
| `&&` | Runs next command only on success | Safe multi-step sequences |
| `&` | Runs in background | Long scans/sniffers (e.g. `tcpdump ... &`) |

Example: `grep "IP" access.log > suspicious.txt && wc -l suspicious.txt`
