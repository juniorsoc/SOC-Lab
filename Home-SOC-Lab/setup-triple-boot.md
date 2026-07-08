# Triple-Boot Setup: Windows 11 + Kali Linux + Ubuntu

## Goal
Set up a single machine running three operating systems — Windows 11, Kali Linux, and Ubuntu — to build a home SOC lab with an attacker machine (Kali), a monitoring/SIEM host (Ubuntu), and a native Windows environment.

## Step 1 — Preparing the USB drive

- Borrowed a USB drive from a friend that had an old Windows 10 boot image on it
- Wiped it using `diskpart` (Win+R → `diskpart` → `clean`) to remove the existing partition table before reusing it
- Freed up disk space on the main drive to make room for the Kali Linux partition
- Temporarily disabled **Secure Boot** (BIOS/UEFI) and **Windows Defender Firewall** to avoid install/boot conflicts during the process

## Step 2 — Installing Kali Linux (dual-boot)

- Downloaded Rufus and the official Kali Linux ISO
- Flashed the ISO to the USB drive using Rufus (GPT / UEFI)
- Rebooted, entered the boot menu with **F11**, selected the USB drive, and booted into the Kali Linux installer
- Went through initial setup: timezone, locale, and tool configuration
- Got comfortable navigating the Linux terminal early on — practiced core commands: `ls`, `ls -al`, `cd`, `cat`, `grep`
- Explored the desktop environment (file manager, wallpaper/appearance settings) to get familiar with the GUI alongside the terminal

## Step 3 — Adding Ubuntu (triple-boot)

- Downloaded the Ubuntu ISO and flashed it to a separate USB drive with Rufus
- Ubuntu's installer was noticeably more straightforward than Kali's — clean, intuitive GUI
- Set up user account, login credentials, and basic system configuration
- Installation completed without partitioning conflicts or errors

## Result

- GRUB boot menu now shows all three operating systems on startup
- Boot selection via **F11** → arrow keys to choose Windows 11 / Kali Linux / Ubuntu

## Lessons learned

- Reusing a USB drive with an existing OS image requires a full wipe (`diskpart clean`) before it can be used for a new installer — otherwise Rufus may not flash correctly
- Disabling Secure Boot is a standard, expected step when dual/triple-booting Linux distributions alongside Windows
- Getting comfortable with basic terminal navigation early (`ls`, `cd`, `cat`, `grep`) made the rest of the Linux-based setup much faster
