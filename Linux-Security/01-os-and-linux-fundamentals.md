# OS Fundamentals, Kernel Space, Virtualization, Linux Basics

## What an OS does

| Responsibility | What it means | Security relevance |
|-----------------|----------------|----------------------|
| Process management | Switches CPU between running apps | Lets you spot an unfamiliar/unauthorized process |
| Memory management | Allocates RAM, offloads to disk when full | — |
| File management | Tracks file locations, enforces access | File permissions block unauthorized changes |
| User management | Isolates accounts from each other | Unauthorized account = strong compromise signal |
| Device management | Recognizes connected hardware | — |

## Kernel space vs user space

System is split into privilege levels to contain damage from a faulty/malicious component.

- **Kernel** — most privileged, direct hardware access.
- **User space** — apps run here, no direct hardware access.

App needs hardware (read a file, send traffic) → issues a **system call** → kernel evaluates and executes it on the app's behalf.

Result: an exploit in one app is usually contained to that app. An exploit in the kernel can compromise the whole system — kernel-level code execution is one of the most severe compromise types possible.

## Virtualization

A **hypervisor** splits one physical machine into multiple independent VMs.

| Type | Runs on | Used for |
|------|---------|----------|
| Type 1 | Bare metal, no host OS | Production, data centers |
| Type 2 | On top of a host OS | Learning, testing |

| | VM | Container |
|---|-----|-----------|
| Isolation | Full OS per VM — strong | Shares host kernel — weaker |
| Startup | Slower | Fast |
| Resources | Heavier | Lighter |

## Linux for a SOC analyst

Common distros:

| Distro | Notes |
|--------|-------|
| Ubuntu | Servers + desktop, lightweight |
| Debian | Stable base for many other distros, common on servers |
| Kali Linux | Preloaded with security/pentest tools |
| CentOS / RHEL | Enterprise, long-term support |

Linux vs Windows: a minimal Linux server runs on a fraction of the RAM Windows Server needs — a big reason Linux dominates server environments.

Core commands: `whoami`, `ls`, `cd`, `cat`, `pwd`, `grep`, `find`, `ps aux`, `file` (real file type, ignores extension), `xxd` (hex dump).

Key filesystem locations for investigations:

| Path | Why it matters |
|------|------------------|
| `/var/log/` | Bulk of system logs — main evidence source |
| `/tmp/` | Writable by any user — common malware landing spot |
| `/etc/passwd` | List of system user accounts |
| `/etc/crontab` | Scheduled tasks — common persistence location |
| `/proc/` | Live info on running processes |
