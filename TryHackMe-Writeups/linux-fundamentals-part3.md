# TryHackMe — Linux Fundamentals Part 3 (Writeup)
**Status:** ✅ Complete

## Room Overview
This room continues from Part 2 — moving files around (`wget`, `scp`, hosting your own web server with Python), how processes work under the hood, scheduling tasks with cron, adding software repos, and where to find log files.

## Task: Downloading Files - Wget
`wget` downloads a file straight from a URL, same as opening it in a browser. Just give it the link:

```bash
wget https://assets.tryhackme.com/additional/linux-fundamentals/part3/myfile.txt
```

**Key concept:** `wget` grabs the file over HTTP and saves it into your current directory, no browser needed.

## Task: Transferring Files - SCP (SSH)
`scp` (secure copy) moves files between two machines over SSH, so unlike plain `cp` it's encrypted. Works on a SOURCE / DESTINATION model, same as `cp`, just with a machine address tacked on.

Sending a file from my machine to a remote one:
```bash
scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt
```

Pulling a file down from a remote machine without logging in first:
```bash
scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt
```

**Key concept:** whichever direction you're copying, the remote side always needs the format `user@ip:/path`.

## Task: Serving Files From My Host - Python HTTPServer
Ubuntu ships with `python3`, which has a built-in module called `http.server`. It turns whatever folder you run it in into a quick web server, so other machines can grab files from you with `wget` or `curl`.

```bash
python3 -m http.server
```

Output:
```
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

Default port is 8000. From a separate terminal (the one running the server just sits there until you `Ctrl+C` it), pull the file down with `wget`, remembering to include the port:

```bash
wget http://10.113.149.98:8000/myfile
```

Note to self: this method has no indexing/browsing — you need to know the exact filename. Room mentions **Updog** as a nicer alternative for this, might look into that later.

## Flag Captured
Downloaded the flag file the same way:
```bash
wget http://10.113.149.98:8000/.flag.txt
```

```
THM{WGET_WEBSERVER}
```

## Task: Viewing Processes
Every running program is a process, managed by the kernel, and each one gets a PID. PIDs increase in the order the processes start — the 60th process to launch gets PID 60.

```bash
ps          # processes in my current session
ps aux      # every process on the system, including other users and system processes
top         # live, refreshing view of processes
```

Small logic check I had to work through myself: if the previous process had PID 300, the next one to start will be **301** (just +1, in order of launch).

## Task: Managing Processes - Signals
`kill <PID>` sends a signal to a process to stop it. Different signals behave differently:

| Signal | What it does |
|---|---|
| SIGTERM | Kill the process, but let it clean up first |
| SIGKILL | Kill it immediately, no cleanup |
| SIGSTOP | Pause/suspend the process |

```bash
kill 1337
```

**Key concept:** `kill` without specifying a signal sends `SIGTERM` by default — that's the "clean" way to kill something.

## Task: How Processes Start - Namespaces & PID 0
The OS splits resources (CPU, RAM) between processes using **namespaces** — these isolate processes from each other, so only processes in the same namespace can see one another.

PID 0 is the very first process that starts when the system boots — on Ubuntu that's `systemd`. Every other program starts as a **child process** of `systemd`, meaning `systemd` manages it, but it still runs as its own separate process.

## Task: Starting Services on Boot - systemctl
`systemctl` talks to the `systemd` process/daemon directly. Format:

```
systemctl [option] [service]
```

| Option | Meaning |
|---|---|
| start | Start the service now |
| stop | Stop the service now |
| enable | Service starts automatically on every boot |
| disable | Service won't start automatically on boot |
| status | Shows the current state of the service |

```bash
systemctl start apache2      # start apache2 right away
systemctl enable apache2     # make apache2 start automatically on boot
```

What command would stop a service called "myservice":
```bash
systemctl stop myservice
```

What command would start that same service on boot:
```bash
systemctl enable myservice
```

## Task: Foreground & Background Processes
Normally a command runs in the **foreground** and takes over your terminal until it finishes — `echo` is a good example, the output comes straight back to you.

Add `&` to push it to the **background** instead — you get the PID back immediately instead of the output:
```bash
echo "Hi THM" &
```

`Ctrl + Z` suspends a process that's already running in the foreground, freeing up the terminal without killing it.

Bringing a backgrounded/suspended process back into focus:
```bash
fg
```

## Investigation trail (own reasoning, not directly prompted by the task)
Wasn't given a command straight away for finding the right process, so I worked through it myself:

```
tryhackme@linux3:~$ ps aux
USER       PID  %CPU %MEM COMMAND
root         1   0.0  0.1 /sbin/init
root       412   0.0  0.2 /usr/sbin/sshd
tryhackme  588   0.0  0.1 ./suspicious_task
tryhackme  601   0.0  0.0 ps aux
tryhackme@linux3:~$ cat /proc/588/cmdline
./suspicious_task
```

Everything else in the list was a normal system service (`sshd`, `init`, etc.) — `suspicious_task` running under my own user was the one that stood out, so I checked it further and pulled the flag from there.

## Flag Captured
```
THM{PROCESSES}
```

## Task: Text Editors - Nano & VIM
Everything up to now was written into files using `echo` and `>` / `>>`, which gets annoying fast for anything longer than one line. `nano` is a simple terminal text editor.

```bash
nano myfile
```

Shortcuts all use `Ctrl` (shown as `^` in nano itself):
- `^X` — exit
- `^O` — write out (save)
- `^W` — where is (search)
- `^K` / `^U` — cut / paste text

**VIM** is mentioned as the more advanced option — customisable shortcuts, syntax highlighting, and it works on pretty much every terminal (nano isn't always installed by default). Leaving VIM for later, TryHackMe has a whole separate room dedicated to it (cheatsheet: [vim.rtorr.com](https://vim.rtorr.com)).

## Task: Scheduling Jobs - Crontab
`cron` is a process that starts at boot and is responsible for running scheduled jobs, based on a **crontab** file.

A crontab line needs 6 fields:

| Field | Meaning |
|---|---|
| MIN | Minute to run at |
| HOUR | Hour to run at |
| DOM | Day of month |
| MON | Month |
| DOW | Day of week |
| CMD | The actual command to run |

Example — backing up a folder every 12 hours:
```bash
0 */12 * * * cp -R /home/cmnatic/Documents /var/backups/
```

Any field you don't care about just gets a `*` (wildcard) instead.

```bash
crontab -e
```

Checked the crontab on the deployed instance (`10.113.149.98`) — it's set to run `@reboot`, meaning it fires once every time the system boots, instead of on a normal time-based schedule.

## Task: Packages & Repositories - APT
An APT repository is a server holding ready-to-install, pre-compiled software (`.deb` files) that `apt` pulls from — different from a Git/GitHub repo, which is for storing and version-controlling source code. Rough analogy: an APT repo is like an app store, a Git repo is more like a workspace for the code itself. (Closest thing I know on macOS would be Homebrew — same idea, different platform.)

Adding a repo manually (example used in the room: Sublime Text):

1. Download and trust the dev's GPG key (confirms the software's integrity/origin):
```bash
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
```

2. Create a separate file for the repo under `/etc/apt/sources.list.d/` (good practice: one file per third-party repo), and put the repo's address inside it.

3. Refresh apt so it knows about the new repo:
```bash
apt update
```

4. Install the software:
```bash
apt install sublime-text
```

Removing a repo / package:
```bash
add-apt-repository --remove ppa:PPA_Name/ppa
apt remove sublime-text
```

Note: TryHackMe instances don't have internet access, so this task was read-only/theoretical — not meant to actually be run on the deployed machine.

## Task: Log Files
Logs live in `/var/log`, and Ubuntu automatically manages/rotates them so they don't grow forever.

Examples covered:
- **Apache2** — web server logs (`access.log` = who requested what, `error.log` = what went wrong)
- **fail2ban** — logs brute-force attempts it detects
- **UFW** — firewall logs

Web server logs record every single request, which is useful for diagnosing performance issues or investigating an intruder's activity.

```bash
cat /var/log/apache2/access.log
```

Went through the apache2 access log on the deployed machine to find which IP hit the site and what file they requested — good reminder that access logs are one of the first places to check when figuring out what a visitor (or attacker) actually did on a server.

## Commands Learned So Far
`wget`, `scp`, `python3 -m http.server`, `ps`, `ps aux`, `top`, `kill`, `systemctl`, `nano`, `crontab -e`, `apt update`, `apt install`, `apt remove`, `add-apt-repository`

## Key Takeaways
- `scp` always needs `user@ip:/path` on the remote side, no matter which direction you're copying.
- `python3 -m http.server` is a fast way to share one file, but there's no browsing — you need the exact filename.
- PIDs just increment: new process = last PID + 1, in launch order.
- `SIGTERM` = clean kill (default for `kill`), `SIGKILL` = force kill, `SIGSTOP` = pause.
- Every process traces back to PID 0 (`systemd` on Ubuntu), which is the parent of everything else.
- `&` and `Ctrl+Z` both push a process to the background, `fg` brings it back to the foreground.
- Crontab fields are `MIN HOUR DOM MON DOW CMD`, and `@reboot` is a special schedule meaning "run once at startup."
- An APT repo (software store) and a Git repo (source code / version control) are not the same thing, even though both get called "repos."
- `/var/log` is the first place to check for what a service — or an attacker — has actually been doing.

Part of a Linux Fundamentals series on TryHackMe, documenting core CLI skills before moving into more advanced security-focused rooms.
