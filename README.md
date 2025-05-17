# (WIP!!!) Debian 12 Setup Guide for Macbook Air 2013 A1465 (EMC 2631)

[Laptop Specs](
https://everymac.com/systems/apple/macbook-air/specs/macbook-air-core-i5-1.3-11-mid-2013-specs.html)

## Initial Setup

Add user to sudoers

```bash
su
sudo adduser [USERNAME] sudo
systemctl reboot
```

copy installation files into a usb drive

Mount usb drive

```bash
sudo mount /dev/[DEVICE PARTITION] [MOUNT DIRECTORY]
# Example: sudo mount /dev/sda1 /media/usb-drive
```

create a downloads folder in home directory and copy all files to the Downloads folder

```bash
mkdir ~/Downloads
cp [MOUNT DIRECTORY] ~/Downloads
```

## Setting up networking (iwd)

install iwd and dependencies

# sudo apt install [filenames]

disable wpa_supplicant

# systemctl --now disable wpa_supplicant

Enable newly installed IWD service (may require su to root)

# systemctl --now enable iwd

uncomment EnableNetworkConfiguration=true in the file /etc/iwd/main.conf

restart iwd service

# systemctl restart iwd

Reboot computer

# Sudo reboot

Connect to a network using iwctl

set up DNS resolution

install systemd-resolved package (use file if installing from the internet doesn't work)

# systemctl enable --now systemd-resolved
# sudo reboot

yipee DNS works!

Install ntp (for syncing time)

# sudo apt install ntp


## Software to Install

Everything should be in nala.history

## Software not Installed through Package Manager

extract croc tarball and move croc executable to /usr/local/bin

## Configs

current timeshift configuration
/etc/timeshift/timeshift.json

### APT & Nala

Sources directory: `/etc/apt/sources.list.d/*`

### ACPI scripts

`/etc/acpi/*`

### IWD (iwctl)

### UFW

**!!! revise this, UFW is not compatible with Docker !!!**

### Zerotier

https://www.zerotier.com/download/#linux

### Docker

```bash
curl -fsSL https://get.docker.com -o get-docker.sh

# Test with dry run first to see what it does
sudo sh get-docker.sh --dry-run

# If everything seems fine, run the script
sudo sh get-docker.sh
```

Manager Docker as a non-root user

```bash
sudo groupadd docker
sudo usermod -aG docker $USER
```

#### Portainer

https://docs.portainer.io/start/install-ce/server/docker/linux