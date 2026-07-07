# Online Tools for Reconnaissance and Analysis

A number of publicly available tools support the reconnaissance and investigative work a SOC analyst regularly performs, each serving a distinct purpose within that workflow.

Shodan functions as a search engine for internet-connected devices, indexing open ports and running services across publicly reachable systems, which makes it valuable for identifying whether an organization has inadvertently exposed something to the internet that shouldn't be reachable from outside. VirusTotal accepts files, URLs, and file hashes and checks them simultaneously against a large number of independent antivirus engines, providing a quick way to assess whether a given piece of content is broadly recognized as malicious rather than relying on the judgment of any single detection engine. The National Vulnerability Database serves as the authoritative source for CVE records and their associated CVSS scores, providing the definitive reference point when researching a specific known vulnerability. Exploit-DB maintains a repository of proof-of-concept exploit code, which is useful for understanding whether a working exploit exists for a given vulnerability and helps inform how urgently it should be remediated. GitHub hosts a wide range of security-related scanners, tools, and CVE analyses, often published and updated faster than official channels can keep pace with.

Working with proof-of-concept code found online, particularly on GitHub, calls for a degree of caution: not every published exploit is complete or reliable, some contain intentional flaws, and in rare cases a repository itself may be crafted maliciously. Reviewing code carefully before execution, and avoiding running unfamiliar scripts in a production environment, is a standard precaution when working with this kind of material.

## Practical Example — Checking a Hash Against VirusTotal

```bash
$ sha256sum suspicious_file.exe
8f14e45fceea167a5a36dedd4bea2543d1f5f5f2e8e3d2f9c6a7b8c1d2e3f4a  suspicious_file.exe

$ curl -s -H "x-apikey: $VT_API_KEY" \
  "https://www.virustotal.com/api/v3/files/8f14e45fceea167a5a36dedd4bea2543d1f5f5f2e8e3d2f9c6a7b8c1d2e3f4a" \
  | grep -o '"malicious":[0-9]*'
"malicious":41
```

Generating the file's hash first, rather than uploading the file itself, avoids exposing potentially sensitive file contents while still allowing a lookup against VirusTotal's database. A result showing 41 out of roughly 70 engines flagging the hash as malicious is a strong, corroborated signal that the file is genuinely dangerous rather than a false positive from a single vendor.
