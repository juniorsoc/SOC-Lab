TryHackMe — Linux Fundamentals Part 3 (Writeup)
Status: ✅ Complete

Room Overview
This room continues from Part 2 and covers moving files around (wget, scp, hosting your own web server with Python), how processes work in Linux, scheduling tasks with cron, adding software repos, and finally where to find log files.

Task: Downloading Files with Wget
wget lets you download a file straight from a URL, same as if you opened it in a browser. Basic syntax:

wget https://assets.tryhackme.com/additional/linux-fundamentals/part3/myfile.txt

Nothing fancy, you just give it the link and it grabs the file into your current folder.

Task: Transferring Files with SCP
scp (secure copy) moves files between two machines over SSH, so it's encrypted, unlike plain cp which only works locally.

It works as SOURCE and DESTINATION, same logic as cp but with a machine address in front.

Copy a file from my machine to a remote machine:

scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt

Copy a file from a remote machine down to mine (without logging in first):

scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt

Key thing I had to remember: the remote side always needs user@ip:/path, doesn't matter if it's the source or the destination.

Task: Serving Files from My Own Machine
Turns out Ubuntu already comes with Python3, and Python has a built-in module called http.server that turns your current folder into a mini web server. Good for quickly sending a file to another machine on the network without setting up anything else.

Start it in the folder you want to share from:

python3 -m http.server

By default it runs on port 8000. Output looks like this:

Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...

Then from another terminal (has to be a new one, the first one is stuck running the server) you can pull the file with wget, just remember to add the port:

wget http://10.113.149.98:8000/myfile

Downloaded the flag file this way:

wget http://10.113.149.98:8000/.flag.txt

Flag Captured

THM{WGET_WEBSERVER}

Note to self: this method has no way to browse/list files, you need to know the exact filename. Room mentions a tool called Updog as a nicer alternative, might check that out later.

Task: Viewing Processes
Every running program is a process, and each one gets a PID (process ID). PIDs just go up in order — first process to start gets a lower number, next one gets the next number, and so on.

ps — shows processes running under my own session
ps aux — shows everything, including other users' processes and system processes (root, etc.)
top — same idea as ps aux but live/updating, refreshes automatically

Quick logic check I had to think through: if the last process had PID 300, the next one that starts will be 301 (just +1).

Task: Killing / Managing Processes
kill <PID> sends a signal to stop a process. Different signals behave differently:

Signal	What it does
SIGTERM	Kill the process but let it clean up first
SIGKILL	Kill it immediately, no cleanup
SIGSTOP	Pause/suspend the process

So if I want to be "nice" about it and kill something cleanly, that's SIGTERM.

Task: How Processes Actually Start
This part took a bit to wrap my head around. The OS uses namespaces to split up the machine's resources (CPU, RAM, etc.) between processes, kind of like giving everything its own slice so it doesn't just eat all the resources.

PID 0 is the very first process that starts when the system boots — on Ubuntu that's systemd. Every other program you start after that becomes a child process of systemd, meaning systemd is in charge of it even though it runs as its own separate process.

Task: Starting Services on Boot with systemctl
systemctl is the command used to talk to systemd. Format is:

systemctl [option] [service]

The 5 options covered:

start
stop
enable
disable
status

So to turn on a service:

systemctl start apache2

To make sure it also comes on automatically every time the machine boots:

systemctl enable apache2

Answers I worked out:

Stop a service called "myservice":

systemctl stop myservice

Start "myservice" automatically on boot:

systemctl enable myservice

Task: Foreground vs Background Processes
Normally when you run a command it runs in the foreground, meaning it takes over your terminal until it's done (like echo, you see the output straight away).

You can push something to the background two ways:

Add & at the end of the command — instead of getting the output back, you just get the process ID and your terminal is free again.
Ctrl + Z while something is already running — this suspends/pauses it instead of killing it, and gives the terminal back.

To bring a backgrounded process back into focus:

fg

Locating the running process on the deployed machine gave me this flag:

THM{PROCESSES}

Task: Text Editors — Nano
Up until now I was only writing to files using echo and > / >>, which is fine for one line but annoying for anything longer. nano is a simple terminal text editor.

nano filename

Opens (or creates) the file so you can just type normally, arrow keys to move around. All the shortcuts use Ctrl (shown as ^ in nano itself), e.g. Ctrl+X to exit, Ctrl+O to save.

Room also mentions VIM as a more advanced option — more powerful, works basically everywhere even when nano isn't installed, but has a steeper learning curve. Leaving that for later, there's apparently a whole separate TryHackMe room just for VIM.

Task: Scheduling Jobs with Cron
cron is a process that starts at boot and runs jobs on a schedule. You manage those jobs through a crontab.

A crontab line needs 6 fields:

Field	Meaning
MIN	Minute to run at
HOUR	Hour to run at
DOM	Day of month
MON	Month
DOW	Day of week
CMD	The actual command to run

Example — backing up a folder every 12 hours:

0 */12 * * * cp -R /home/cmnatic/Documents /var/backups/

Any field you don't care about, just put a * (wildcard) instead.

To edit your own crontab:

crontab -e

Checked the crontab on the deployed machine — it was set to run @reboot, meaning it just fires once every time the system boots up, instead of on a normal time schedule.

Task: Packages & Repositories
When someone writes a program for Linux, it usually gets published to an apt repository so people can install it with apt instead of manually downloading files.

You can add extra (community/3rd-party) repos on top of the default ones with add-apt-repository, or by adding a source file manually. Before installing anything from a new repo, apt checks a GPG key to confirm the software is actually coming from who it says it's from — if the key doesn't match, it just won't install.

Steps to manually add a repo (using Sublime Text as the example in the room):

Add and trust the dev's GPG key:

wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -

Create a file for the new repo under /etc/apt/sources.list.d/ (good practice: one file per repo).

Refresh apt so it knows about the new repo:

apt update

Install the software:

apt install sublime-text

To remove a repo + software again:

add-apt-repository --remove ppa:PPA_Name/ppa
apt remove sublime-text

(This part of the room was read-only, TryHackMe VMs don't have internet access so you're not actually meant to run the add step on the deployed machine.)

Task: Log Files
/var/log is where most services keep their logs. Ubuntu automatically manages/rotates these so they don't just grow forever.

Room pointed out 3 examples:

Apache2 — web server logs (access log = who requested what, error log = what went wrong)
fail2ban — logs brute-force attempts it detected
ufw — firewall logs

Went looking through the apache2 access log on the deployed machine to find which IP hit the site and what file they requested — good reminder that access logs are one of the first places to check when trying to figure out what a visitor (or attacker) actually did on a server.

Commands Learned So Far (new in Part 3)
wget, scp, python3 -m http.server, ps, ps aux, top, kill, systemctl, nano, crontab -e

Key Takeaways
scp always needs user@ip:/path on the remote side, whichever direction you're copying.
python3 -m http.server is a super quick way to share a file, but you need to know the exact filename since there's no browsing/index.
PIDs just increment — new process = last PID + 1.
SIGTERM = clean kill, SIGKILL = force kill, SIGSTOP = pause.
Everything traces back to PID 0 (systemd on Ubuntu) as the parent of all other processes.
& and Ctrl+Z both background a process, fg brings it back.
Crontab fields go MIN HOUR DOM MON DOW CMD, and @reboot is a special schedule that just means "run once at startup."
/var/log is the first place to check for what a service (or an attacker) has been doing.

Part of a Linux Fundamentals series on TryHackMe, documenting core CLI skills before moving into more advanced security-focused rooms.
