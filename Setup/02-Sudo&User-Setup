# Sudo and User Setup on Debian

## Overview
Unlike Ubuntu, Debian does not automatically give your user sudo access during installation. This guide covers how to add a user to the sudo group and configure sudo properly.

---

## Why This Matters
- Regular users cannot install software or change system settings
- Sudo gives temporary root access for single commands
- Safer than using root account directly
- Essential for server administration

---

## Step 1 — Switch to Root
After logging in as your regular user:
```bash
su -
```
Enter your **root password** when prompted.

---

## Step 2 — Install Sudo
Debian minimal install may not include sudo by default:
```bash
apt install sudo -y
```

---

## Step 3 — Add User to Sudo Group
Replace `brian` with your actual username:
```bash
usermod -aG sudo brian
```

---

## Step 4 — Verify it Worked
```bash
groups brian
```
You should see **sudo** listed in the output.

---

## Step 5 — Exit Root
```bash
exit
```

---

## Step 6 — Log Out and Back In
```bash
logout
```
Log back in with your username and password — this refreshes your group membership.

---

## Step 7 — Test Sudo
```bash
sudo apt update
```
It will ask for your password — if it works sudo is configured correctly!

---

## Common Error — Not in Sudoers File
If you see:
```
brian is not in the sudoers file. This incident will be reported.
```
Go back to Step 1 and repeat the process.

---

## Useful Sudo Commands
```bash
# Run single command as root
sudo command

# Switch to root shell
sudo -i

# Check sudo access
sudo -l

# Edit a system file
sudo nano /etc/filename
```

---

## Keep Server Running with Lid Closed
Since this is a headless server configure the laptop lid behavior:

```bash
sudo nano /etc/systemd/logind.conf
```

Find and change these lines (remove the # to uncomment):
```
HandleLidSwitch=ignore
HandleLidSwitchExternalPower=ignore
HandleLidSwitchDocked=ignore
```

Apply the change:
```bash
sudo systemctl restart systemd-logind
```

Now closing the laptop lid will not suspend the server.
