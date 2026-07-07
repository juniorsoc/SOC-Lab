# Bash Operators — Redirection and Command Chaining

Bash provides several operators that control how commands interact with files and with one another, and understanding the distinctions between them matters because using the wrong one can silently discard data that was meant to be preserved.

The output redirection operator that overwrites a file replaces its entire previous contents with new output every time it's used, which is appropriate when starting a fresh file from scratch but destructive if applied repeatedly to something meant to accumulate over time. The append operator, by contrast, preserves whatever a file already contains and adds new output onto the end of it, which is the correct choice whenever results from multiple separate commands need to be collected together into a single running file.

Command chaining operators control how sequences of commands relate to one another. The conditional chaining operator runs a second command only if the first one completed successfully, which is useful for building safe multi-step sequences where it wouldn't make sense to proceed if an earlier step failed. The background operator launches a command without waiting for it to finish, immediately returning control of the terminal so that other work can continue in parallel — this is particularly relevant for long-running tasks such as continuous traffic capture, which would otherwise tie up the terminal for as long as they run.

Together, these operators allow multi-step analysis workflows to be constructed directly from the command line — searching for something, saving the results to a file, and immediately following up with another command that depends on that output, all in a single chained sequence rather than as separate manual steps.
