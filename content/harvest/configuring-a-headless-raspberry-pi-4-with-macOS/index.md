---
title: "Configuring a Headless Raspberry Pi 4 with macOS"
date: 2023-01-09
draft: false
description: "A step-by-step guide for setting up a headless Raspberry Pi 4 from macOS."
tags:
  - linux
  - mac
---

Preparing the MicroSD Card I personally use a piece of software called [balenaEtcher](https://www.balena.io/etcher/) however you can also use Raspberry Pi’s own [Imager](https://www.raspberrypi.com/software/) software which includes the option to browse compatible operating systems and the ability to download them within the application.

My operating system of choice is [Raspberry Pi OS Lite](https://www.raspberrypi.com/software/operating-systems/) as it is native to the Raspberry Pi and based on Debian which offers a great deal of support from communities online.

_I prefer to download using a torrent due to speed since the file is being downloading piece by piece from various servers rather than a single one._

### Flashing the Operating System
1. Once Etcher is open you can click on “Flash from file” to choose the .img file that was downloaded.
2. Click “Select Target” and choose the external media device that you wish to flash the operating system onto.
3. Click “Flash!”.

### Enabling SSH via [Terminal.app](http://terminal.app/)
1. Since Etcher automatically ejects the external media once it’s finished flashing the operating system, go ahead and plug in your external media device again.
2. Open a new Terminal window and type - `cd/Volumes/boot` 
3. To enable SSH we are going to create a blank ssh file by typing - `touch ssh` 
4. Type `cd` to get back to the home directory. You can now eject the external media device and remove it from your computer.

### Powering Up
1. Insert the microSD card into the Raspberry Pi.
2. Connect one end of an ethernet cable to the Raspberry Pi and the other end to your router.
3. Plug in the power cable to the Raspberry Pi.

## Connecting via SSH
1. Open up a new Terminal window and type - `ping raspberrypi.local`
2. You should see the output “PING raspberrypi.local (192.x.x.x)”. The numbers inside the parenthesis that either start with “192” or “10” will be the IP address of the Raspberry Pi (to stop the continuous ping type `ctl + C`).
3. To start the SSH session type - `ssh pi@<ip-address>`
4. If you see a warning “authenticity of host can’t be established…are you sure you want to continue connecting” - type `yes` (this is because the SSH client has never encountered the server’s key fingerprint before).
5. The default password is `raspberry` (no text will appear but continue typing - this is a security measure).

### Changing the Default Password
I highly recommend that you change the default password to increase the security of your Raspberry Pi.
1. Type - `passwd`
2. Enter the default password.
3. Then type in your new password.

### Updating
It’s always a good idea to update your packages periodically.
1. To update all currently installed packages and then upgrade them, type - `sudo apt-get update && sudo apt-get upgrade -y`
2. This last step isn’t required but it’s a good habit to always reboot after updating to ensure the changes went into effect (the current SSH session will terminate automatically). Type - `sudo reboot`