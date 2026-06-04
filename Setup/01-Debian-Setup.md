# Debian Installation Guide

## Overview
Step by step guide for installing Debian 13 Bookworm on a laptop as a headless home lab server.

---

## What You Need
- USB drive (2GB minimum)
- Laptop to install Debian on
- Another computer to download and flash the ISO
- Internet connection (WiFi or ethernet)

---

## Step 1 — Download Debian ISO
1. Go to **debian.org/download**
2. Download **Debian 13 Bookworm netinstall ISO**
3. Select **amd64** for standard Intel/AMD laptops
4. File size is around **750MB**

---

## Step 2 — Flash USB with Rufus
1. Download **Rufus** from rufus.ie
2. Open Rufus as **Administrator**
3. Select your USB drive under Device
4. Click **SELECT** and choose the Debian ISO
5. Partition scheme: **MBR**
6. Click **START**
7. Select **DD mode** when prompted
8. Wait for flashing to complete

---

## Step 3 — Configure BIOS
Before booting from USB configure these BIOS settings:

1. Turn on laptop and spam **F2** (Asus) or **F10** (HP) to enter BIOS
2. Disable **Fast Boot**
3. Disable **Secure Boot**
4. Enable **CSM** if available
5. Save with **F10**

---

## Step 4 — Boot from USB
1. Plug in USB drive
2. Turn on laptop and spam **F12** (Asus) or **F9** (HP)
3. Select your USB drive from boot menu
4. Press **Enter**

---

## Step 5 — Start Installation
1. Select **Install** (not Graphical Install)
2. Select your **language**
3. Select your **location**
4. Select your **keyboard layout**

---

## Step 6 — Network Setup
- Select your **WiFi network** if prompted
- Enter your **WiFi password**
- If WiFi fails select **Continue without network** — you can connect after install

---

## Step 7 — Configure Hostname and Domain
- **Hostname** — give your server a name (example: `homelab`)
- **Domain name** — leave blank for home use

---

## Step 8 — Set Up Users
- Set a **root password** — keep this safe
- Create a **regular user account** with username and password
- This is the account you will log in with daily

---

## Step 9 — Partition Disk
1. Select **Guided - use entire disk**
2. Select your **internal hard drive** (not the USB)
   - SATA drive shows as `/dev/sda`
   - NVMe drive shows as `/dev/nvme0n1`
3. Select **All files in one partition**
4. Select **Finish partitioning and write changes to disk**
5. Select **Yes** to confirm

---

## Step 10 — Software Selection
When asked what to install **only select:**
- ✅ **SSH server**
- ✅ **Standard system utilities**

**Uncheck everything else:**
- ❌ Debian desktop environment
- ❌ GNOME
- ❌ XFCE
- ❌ Web server
- ❌ Print server

This keeps the server lean and headless — no GUI needed.

---

## Step 11 — Install GRUB Bootloader
1. Select **Yes** to install GRUB to the EFI partition
2. Select **Yes** to update NVRAM variables
3. This ensures Debian boots automatically on startup

---

## Step 12 — Complete Installation
1. Wait for installation to finish
2. When you see **Installation Complete** click **Continue**
3. **Unplug the USB drive**
4. Laptop will reboot into Debian

---

## Step 13 — First Login
You will see a black screen with a login prompt:
```
homelab login:
```
1. Type your **username** and press Enter
2. Type your **password** and press Enter
3. You are now logged into your Debian server!

---

## Step 14 — Update System
First thing to do after logging in:
```bash
su -
apt update && apt upgrade -y
exit
```

---

## Next Steps
- [Sudo and User Setup](02-sudo-setup.md) — configure sudo access
- [Docker Installation](03-docker-install.md) — install Docker

---

## Common Issues

**Black screen after reboot:**
- Replug USB and boot from it again
- Reinstall GRUB bootloader

**WiFi not working during install:**
- Select continue without network
- Connect to WiFi after install using `sudo nmtui`

**Disk not detected:**
- Disable Secure Boot in BIOS
- Disable Intel RST in BIOS
- See [Troubleshooting Guide](../docs/troubleshooting/README.md)

**Permission denied errors:**
- See [Sudo and User Setup](02-sudo-setup.md)
