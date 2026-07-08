# Home SOC Lab

Building a home lab environment to practice real detection and monitoring — not just theory or online simulators.

## Goal
Simulate a small SOC environment end-to-end: generate malicious traffic, detect it, investigate it, document it — the same workflow used in a real SOC.

## Hardware

| Component | Details |
|---|---|
| Motherboard | ASRock B450M-HDV (AM4) |
| Storage | Samsung SSD 980 500GB |
| OS Setup | Triple-boot: Windows 11 Pro / Kali Linux / Ubuntu |

## Lab Architecture

- **Windows 11** — victim/test machine (Windows Event Logs → Splunk)
- **Kali Linux** — attacker machine (Nmap, Hydra, Metasploit — generating traffic to detect)
- **Ubuntu** — stable host for SIEM (Splunk) and IDS (Suricata)

## Build Status

| Stage | Status |
|---|---|
| Kali install (dual-boot) | ✅ Done |
| Ubuntu install (triple-boot) | 🔄 In progress |
| Splunk on Ubuntu | ⏳ Next |
| Suricata on Ubuntu | ⏳ Next |
| First detected incident (end-to-end test) | ⏳ Next |

## Files in this folder

| File | Description |
|---|---|
| [`setup-triple-boot.md`](./setup-triple-boot.md) | Step-by-step triple-boot install process (Windows 11 + Kali + Ubuntu) |
| [`splunk-install.md`](./splunk-install.md) | Splunk installation and configuration on Ubuntu |
| [`suricata-install.md`](./suricata-install.md) | Suricata installation, rules, and Splunk integration |
| [`tools.md`](./tools.md) | Tools used in this lab and why |

## Why this matters

Most of what recruiters see in junior applications is coursework or CTF writeups. This lab shows infrastructure I built myself, from partitioning disks to correlating IDS alerts with SIEM logs — the same skill of setting up and troubleshooting a monitoring stack that a junior SOC role requires on day one.
