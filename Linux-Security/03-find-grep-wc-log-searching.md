# find, grep, wc — Searching Logs

```bash
find -name "*.txt"                          # find files by name/pattern
grep "IP_ADDRESS" access.log                # search for a term
grep -c "term" access.log                   # count matches
grep -n "term" access.log                   # show line numbers
grep -R "term" /etc/                        # recursive search
wc -l access.log                            # count lines/entries
```

**access.log format:** `IP - - [timestamp] "METHOD /path HTTP/1.1" status size`

**SOC use:** a high count of `404` from one IP = directory brute-forcing/scanning:
```bash
grep "IP_ADDRESS" access.log | grep " 404 " | wc -l
```
