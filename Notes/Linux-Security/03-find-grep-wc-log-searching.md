# find, grep, wc — Searching Through Logs

| Command | Use |
|---------|-----|
| `find` | Locate files by name/attributes, exact or pattern match |
| `grep` | Search file contents for a pattern |
| `wc -l` | Count lines in a file (= entry count for a log) |

Useful `grep` modifiers:

| Flag | Effect |
|------|--------|
| `-o` | Show only the matched part of the line, not the whole line |
| `-c` | Count matching lines instead of printing them |
| `-n` | Prefix each match with its line number |
| `-r` | Search recursively through a directory |

Typical web access log entry: client IP, timestamp, HTTP method + path, status code, response size. Combining fields (e.g. one IP + a cluster of error codes) reveals patterns — like scanning/probing — that a single field alone wouldn't show.
