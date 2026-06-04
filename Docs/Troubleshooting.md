# Troubleshooting - Home Lab Setup

## Overview
Real issues encountered and resolved during home lab setup. Documented for reference and to demonstrate problem solving skills.

---

## Issue 1 — Failing NVMe SSD on HP Pavilion x360

**Symptoms:**
- Ubuntu installer showed "block probing did not discover any disks"
- `dmesg` showed buffer IO errors on /dev/nvme0n1
- Error: `buffer I/O error on dev nvme0n1, logical block 0, lost async page write`

**Diagnosis:**
```bash
dmesg | grep nvme
dmesg | grep error
```
Output confirmed bad sectors on the NVMe drive — physical hardware failure.

**Root Cause:**
SK Hynix NVMe SSD had bad sectors and was physically failing.

**Resolution:**
Switched to Asus X551M laptop with a healthy SATA HDD. HP Pavilion x360 requires NVMe SSD replacement (~$35) to be usable again.

**What I Learned:**
- How to use `dmesg` to diagnose hardware issues
- Difference between NVMe and SATA drives
- How to identify failing storage hardware

---

## Issue 2 — Corrupted USB Drives Causing IO Errors

**Symptoms:**
- Rufus showed error: `Write error [0x0000045D] The request could not be performed because of an I/O device error`
- Balena Etcher showed checksum verification failed
- USB drives showing only 4MB of usable space in Windows

**Root Cause:**
- Both USB drives were damaged from repeated OS flashing
- One USB was corrupted by being unplugged mid-boot
- Cheap USB drives can't handle repeated intensive write operations

**Resolution:**
- Used `diskpart` in Windows CMD to clean and reformat USB drives
- Switched to DD mode in Rufus for more reliable flashing
- Used working USB drive for Debian installation

**Commands Used:**
```
diskpart
list disk
select disk #
attributes disk clear readonly
clean
create partition primary
format fs=fat32 quick
assign
exit
```

**What I Learned:**
- USB drives have limited write cycles
- Always safely eject before unplugging
- DD mode is more reliable than ISO mode for Linux flashing
- Use name brand USB drives (SanDisk, Samsung) for reliability

---

## Issue 3 — UEFI Secure Boot Blocking Linux Installation

**Symptoms:**
- Ubuntu installer could not detect NVMe drive
- Debian installer failed to mount installation media
- Linux boot attempts failing silently

**Diagnosis:**
Checked BIOS settings on HP Pavilion x360 — Secure Boot was enabled.

**Root Cause:**
Secure Boot only allows Microsoft signed bootloaders — blocks Linux from accessing hardware properly including NVMe drives.

**Resolution:**
1. Entered BIOS with F10 on HP laptop
2. Located Secure Boot setting under Security tab
3. Changed from Enabled to Disabled
4. Saved with F10 and rebooted
5. Linux installer could then detect drives properly

**What I Learned:**
- What Secure Boot is and how it works
- BIOS navigation on HP and Asus laptops
- Difference between UEFI and Legacy boot modes
- How to configure boot order in BIOS

---

## Issue 4 — Corrupted Windows Hibernation Data Blocking Partitioning

**Symptoms:**
- Debian installer showed: "The disk contains an unclean file system. Please resume and shutdown Windows fully (no hibernation)"
- Could not proceed with disk partitioning

**Root Cause:**
Windows Fast Startup uses hibernation instead of full shutdown — leaving the filesystem in a locked state that Linux cannot modify.

**Resolution:**
Used `ntfsfix` from the installer shell to clear the Windows hibernation flag:
```bash
sudo ntfsfix /dev/nvme0n1
```

Also disabled Windows Fast Startup:
- Control Panel → Power Options → Choose what power buttons do
- Uncheck "Turn on fast startup"

**What I Learned:**
- How Windows Fast Startup works
- NTFS filesystem locking
- Using `ntfsfix` to repair NTFS partitions
- Importance of proper shutdown procedures

---

## Issue 5 — Intel RST/RAID Conflicts

**Symptoms:**
- Ubuntu installer showed "block probing did not discover any disks"
- Drive visible in BIOS but not in Linux installer

**Root Cause:**
HP Pavilion x360 had Intel Rapid Storage Technology (RST) enabled in BIOS — sets storage controller to RAID mode which Linux cannot read by default.

**Resolution:**
- Located Intel RST setting in BIOS System Configuration
- Disabled Intel RST / changed to AHCI mode
- Ubuntu could then detect the drive

**What I Learned:**
- Difference between RAID and AHCI storage modes
- Intel RST and how it affects Linux compatibility
- How to navigate and configure HP BIOS settings

---

## Issue 6 — Debian Partition ext4 Failure

**Symptoms:**
- Debian installer showed "type ext4 has failed" during partitioning
- "No root file system is defined" error
- Installer crashing during storage configuration

**Root Cause:**
Leftover corrupted partition data from previous Ubuntu installation attempts conflicting with Debian installer.

**Resolution:**
Wiped the drive completely from installer shell:
```bash
cat /dev/zero > /dev/nvme0n1
```
Then used manual partitioning in Debian installer to create fresh GPT partition table and partitions.

**What I Learned:**
- How to wipe a drive from command line
- Manual disk partitioning in Linux
- GPT vs MBR partition tables
- EFI, swap, and root partition layout

---

## Issue 7 — Brian Not in Sudoers File

**Symptoms:**
```
brian is not in the sudoers file. This incident will be reported.
```

**Root Cause:**
Debian does not automatically add users to the sudo group unlike Ubuntu.

**Resolution:**
```bash
su -
apt install sudo -y
usermod -aG sudo brian
exit
logout
```
Log back in to apply group membership.

**What I Learned:**
- Difference between Debian and Ubuntu user setup
- How sudo and the sudoers file works
- Linux user and group management
- Difference between `su` and `sudo`

---

## Issue 8 — Immich Permission Denied Creating Directories

**Symptoms:**
```
Permission denied: /opt/immich
Permission denied: curl download
```

**Root Cause:**
/opt is a system directory owned by root — regular users cannot write to it without sudo.

**Resolution:**
```bash
sudo mkdir -p /opt/immich
sudo chown -R brian:brian /opt/immich
```

**What I Learned:**
- Linux file ownership and permissions
- How `chown` works
- Why /opt requires root access
- Difference between system and user directories

---

## Quick Reference — Useful Diagnostic Commands

```bash
# Check disk health and errors
dmesg | grep error

# List all storage devices
lsblk

# Check disk space
df -h

# Check RAM usage
free -h

# Check running processes
top

# Check Docker containers
docker ps

# Check system logs
journalctl -xe

# Find your IP address
hostname -I

# Check network interfaces
ip addr show
```
