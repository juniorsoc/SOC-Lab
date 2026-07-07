# The OS as the Foundation of Security

Antivirus and firewalls get most of the attention, but they're layered on top of security mechanisms the OS itself provides from boot, before any third-party tool runs.

| Mechanism | What it does | Related threat |
|-----------|----------------|-----------------|
| Authentication | Verifies identity before granting access | Repeated failed attempts = brute force |
| Permissions | Controls what each user/app can do once authenticated | Privilege escalation — going beyond your initial access |
| Isolation | Keeps programs contained in their own boundary | A fault/compromise in one app doesn't spread system-wide |
| System protection | Prevents modification of critical files | Harder for malware to tamper with core components |

These four form the baseline every other security control builds on top of.
