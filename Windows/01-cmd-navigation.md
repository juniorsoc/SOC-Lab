# Windows Terminal — CMD Navigation

Working from the command line on Windows offers more precise control than navigating through graphical folders and is often the only option available when investigating a remote system without graphical access at all.

The `cd` command, used without arguments, displays the current directory, and used with a folder name changes into that directory, functioning much like `pwd` and `cd` combined on a Linux system. The `dir` command lists the contents of the current folder, serving the same role as `ls`. Adding the appropriate flag reveals hidden files and folders as well, comparable to using an extended listing option on Linux — and this distinction matters because Windows hides certain files from view by default, which is a technique sometimes exploited to conceal malicious files from casual inspection, making it worth always checking for hidden content during an investigation rather than relying on a default listing. The `dir` command can also search recursively through all subfolders for a specific filename when its exact location isn't known, comparable to using `find` on Linux. The `type` command displays the contents of a text file, serving the same role as `cat`.

A typical sequence for locating and reviewing an unfamiliar file on a Windows system involves first confirming the current location, listing the immediate contents of that location including hidden items, searching more broadly across the filesystem if the file isn't found nearby, navigating to wherever it's actually located once found, and finally displaying its contents for review.

## Practical Example — Locating a Hidden File

```
C:\Users\Administrator>dir /a
 Volume in drive C has no label.

 Directory of C:\Users\Administrator

07/07/2026  09:14 AM    <DIR>          .
07/07/2026  09:14 AM    <DIR>          ..
07/07/2026  03:22 AM               487  .malicious_note.txt   ← hidden file, missed by plain dir
07/07/2026  08:40 AM    <DIR>          Documents

C:\Users\Administrator>type .malicious_note.txt
System backup scheduled — do not delete this task.
```

A plain `dir` would have shown only the `Documents` folder. Adding `/a` reveals the hidden text file, and `type` displays its contents directly — in this case, a note left behind that's worth investigating further as a possible social-engineering or persistence artifact.
