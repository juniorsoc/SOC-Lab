# Operating System Fundamentals, Kernel Space, Virtualization, and Linux Basics

## What an Operating System Does

An operating system serves as the manager sitting between the user, running applications, and the underlying hardware, and its responsibilities span several core areas. Process management allows multiple applications to run concurrently by rapidly switching the processor's attention between them, creating the appearance of simultaneous execution. Memory management allocates working memory to each running application and offloads data to slower storage when physical memory runs short. File management keeps track of where every file resides on disk and enforces who is permitted to access each one. User management isolates the files and settings of different accounts on the same machine from one another. Device management recognizes and integrates external hardware, such as peripherals, as they're connected.

Each of these responsibilities has direct security relevance. Process management is what allows an unfamiliar or unauthorized process to be identified. File permissions are what prevent unauthorized modification of protected files. User account management is what makes the appearance of an unauthorized account on a system such a strong signal of compromise.

## Kernel Space vs User Space

A system is divided into different privilege levels specifically to contain the damage that a single faulty or malicious component could otherwise cause. The kernel occupies the most privileged level, holding direct and unrestricted authority over the hardware itself, while ordinary applications run in a separate, more restricted user space, with no direct hardware access of their own.

When an application in user space needs to interact with hardware — reading a file, sending network traffic — it cannot do so directly. Instead, it issues a system call, a formal request that the kernel evaluates and, if permitted, carries out on the application's behalf. This layer of indirection means that a failure or exploit within a single application is generally contained to that application, whereas a failure within the kernel itself can compromise the entire system.

The operating system as a whole encompasses far more than just the kernel — it includes the graphical interface, system utilities, and drivers working alongside it — but the kernel specifically is the component holding actual authority over the hardware. A vulnerability that allows an attacker to execute code at the kernel level represents one of the most severe classes of compromise possible, since it grants complete control over the machine, bypassing the isolation that normally protects the system from user-space applications.

## Virtualization

Physical servers historically ran a single application each, resulting in significant underutilization of available hardware capacity. A hypervisor addresses this by dividing one physical machine into multiple independent virtual machines, each capable of running its own operating system and workload as though it were a separate physical server.

Hypervisors fall into two categories. A Type 1 hypervisor runs directly on the underlying hardware without a separate host operating system beneath it, and is the typical choice for production environments and data centers due to its performance and stability. A Type 2 hypervisor runs on top of an existing host operating system, which introduces additional overhead but makes it well suited to learning and testing scenarios.

Virtual machines and containers represent two different approaches to isolation. A virtual machine runs a complete, independent operating system of its own, which provides strong isolation but comes with a slower startup time and greater resource overhead. A container instead shares the underlying host's operating system kernel while isolating the application and its dependencies, resulting in a much faster startup and lighter resource footprint, at the cost of somewhat weaker isolation compared to a full virtual machine.

## Linux Fundamentals for a SOC Analyst

Linux underpins a substantial portion of the infrastructure a SOC analyst will encounter, including the large majority of web servers, much critical infrastructure, and the kernel underlying the Android operating system itself.

Several distributions recur frequently in professional contexts. Ubuntu is widely used for both servers and desktop environments and is notably lightweight, capable of running on very modest hardware. Debian serves as a stable foundation underlying many other distributions and a large share of server deployments. Kali Linux comes preconfigured with a broad set of security and penetration-testing tools, making it a natural environment for hands-on security work. CentOS and RHEL are common in larger enterprise environments requiring long-term support and stability.

One notable contrast with Windows is resource efficiency: a minimal Linux server installation can run comfortably on a small fraction of the memory that Windows Server requires, which is a significant factor in Linux's dominance in server environments.

The terminal is the primary interface through which meaningful work gets done on a Linux system, typically presenting a prompt indicating the current user, hostname, and working directory. A core set of commands recurs constantly: `whoami` reveals the currently logged-in user; `ls` lists the contents of a directory; `cd` changes the current working directory; `cat` displays the contents of a file; `pwd` reports the full path of the current location; `grep` searches for specific text within a file or a stream of output; `find` locates files across the filesystem by name or other criteria; `ps aux` lists all currently running processes; `file` identifies a file's actual type based on its underlying content rather than trusting its extension; and `xxd` renders a file's raw contents as a hexadecimal dump for closer inspection.

Certain filesystem locations carry particular significance during investigative work. The `/var/log/` directory holds the bulk of system logs and serves as the primary source of evidence during an investigation. The `/tmp/` directory is frequently writable by any user and is a common landing spot for files dropped by malicious activity. The `/etc/passwd` file lists system user accounts. The `/etc/crontab` file defines scheduled tasks and is a common location where persistence mechanisms are hidden. The `/proc/` directory exposes live information about currently running processes.
