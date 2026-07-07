# find, grep, and wc — Searching Through Logs

The `find` command locates files across the filesystem based on their name or other attributes, which is useful both for locating a specific known file and for searching more broadly using pattern matching when the exact filename isn't known.

The `grep` command searches within file contents for a given pattern and offers several useful modifiers. It can restrict output to only the portion of each line that actually matched, rather than the whole line. It can report a simple count of matching lines instead of the matches themselves, which is useful for quickly gauging the scale of something without reviewing every individual entry. It can prefix each match with the line number it was found on, which helps when cross-referencing findings against the original file. And it can search recursively through every file within a directory structure, rather than being limited to a single file.

The `wc` command, when used with its line-counting option, reports the total number of lines in a file, which for a log file typically corresponds directly to the number of recorded entries — a quick way to gauge the overall volume of activity captured.

A typical web server access log entry records several pieces of information in a consistent structure: the IP address of the client making the request, a timestamp indicating when the request occurred, the HTTP method and path that was requested, the status code returned by the server, and the size of the response. Reviewing these fields in combination is often more informative than looking at any single field in isolation — for instance, correlating a specific IP address against a concentration of error status codes can reveal patterns of scanning or probing behavior that wouldn't be obvious from the raw log alone.

## Practical Example — Investigating a Suspicious IP in access.log

```bash
$ wc -l access.log
14832 access.log

$ grep "81.143.211.90" access.log | wc -l
1204

$ grep "81.143.211.90" access.log | grep " 404 " | wc -l
1187

$ grep "81.143.211.90" access.log | head -3
81.143.211.90 - - [07/Jul/2026:03:12:01] "GET /admin.php HTTP/1.1" 404 162
81.143.211.90 - - [07/Jul/2026:03:12:01] "GET /wp-login.php HTTP/1.1" 404 162
81.143.211.90 - - [07/Jul/2026:03:12:02] "GET /.env HTTP/1.1" 404 162
```

Out of 1,204 total requests from this one IP, 1,187 returned a 404 — a 98.6% not-found rate. Combined with the requested paths (`admin.php`, `wp-login.php`, `.env`), this is a textbook automated scan probing for common vulnerable endpoints, not legitimate traffic.
