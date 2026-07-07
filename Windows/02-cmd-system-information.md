# Windows CMD — Gathering System Information

Before troubleshooting an issue or beginning an investigation on an unfamiliar Windows machine, it's standard practice to first establish the basic context of the system — who's logged in, what the machine is, what version of Windows it's running, and how it's connected to the network.

The `whoami` command reports the currently logged-in user account, which establishes the privilege level available on the system — an account with SYSTEM or Administrator privileges represents full control over the machine, and identifying this early shapes how the rest of the investigation proceeds. The `hostname` command reports the machine's name as it's known on the network, which can help identify its role within a larger environment — certain naming patterns, for instance, commonly indicate a domain controller or other infrastructure role. The `systeminfo` command reports detailed information about the operating system, including its version, architecture, and installed memory, along with the date it was last patched — an outdated patch date is a meaningful signal that the system may be vulnerable to known, publicly documented exploits. The `ipconfig` command reports the current network configuration, including the assigned IP address, subnet mask, and default gateway, and can also reveal the presence of unexpected network adapters, such as a VPN tunnel that shouldn't otherwise be present on that machine.

A typical order for gathering this information on an unfamiliar system starts with identity and privilege level, moves to identifying the machine itself, then reviews the operating system's version and patch status, and finally examines how the system is connected to the surrounding network.

## Practical Example — Initial Recon on an Unfamiliar Windows Host

```
C:\Users\jsmith>whoami
desktop-04\jsmith

C:\Users\jsmith>hostname
DESKTOP-04

C:\Users\jsmith>systeminfo | findstr /C:"OS Name" /C:"OS Version" /C:"System Type"
OS Name:                   Microsoft Windows 10 Enterprise
OS Version:                10.0.19045 N/A Build 19045
System Type:               x64-based PC

C:\Users\jsmith>ipconfig
Ethernet adapter Ethernet0:
   IPv4 Address. . . . . . . . . . . : 10.0.5.22
   Default Gateway . . . . . . . . . : 10.0.5.1

PPP adapter VPN Connection:            ← unexpected on a standard workstation
   IPv4 Address. . . . . . . . . . . : 172.16.99.4
```

The user account here has standard (non-admin) privileges. The `systeminfo` output, filtered with `findstr` to just the relevant lines, confirms the exact OS build for cross-referencing against known vulnerabilities. The `ipconfig` output reveals an unexpected VPN adapter — worth investigating, since a workstation that shouldn't normally have a VPN tunnel active is a pattern sometimes associated with unauthorized remote access tools.
