# OS Fundamentals, Kernel Space, Virtualization, Linux Basics

**OS core jobs:** process management, memory management, file management, user management, device management. SOC relevance: spotting unknown processes, file permissions, unauthorized accounts.

**Kernel space vs user space:** the kernel has full hardware access; user-space apps request access via system calls. A kernel exploit = full machine control, the most severe attack class.

**Virtualization:** a hypervisor splits one physical server into multiple VMs. Type 1 (bare metal — ESXi, Hyper-V) for production; Type 2 (hosted — VirtualBox) for testing/learning. VMs have full independent OSes (slower start); containers share the host OS (fast start).

**Linux essentials for SOC:** ~96% of web servers, most infrastructure and IoT devices, and Android all run on Linux.

**Core commands:** `whoami`, `ls`, `cd`, `cat`, `pwd`, `grep`, `find`, `ps aux`, `file` (checks real file type via magic bytes), `xxd` (hex view).

**Key SOC locations:** `/var/log/` (logs), `/tmp/` (common malware landing spot), `/etc/passwd` (users), `/etc/crontab` (scheduled tasks, possible persistence), `/proc/` (running processes).
