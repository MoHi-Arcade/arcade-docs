==============================
Raspberry Pi SD Card Recovery
==============================

This page explains how to recover a Raspberry Pi SD card when the user password is forgotten or `sudo` is broken.  
It covers booting into a root shell, mounting the SD card on another system, and restoring `sudo`.

Getting into a Root Shell
=========================

If you forget the Pi password, you can boot into a root shell using the following method:

1. Power off the Raspberry Pi and remove the SD card.
2. Insert the SD card into another computer.
3. Open the `boot` partition and edit the `cmdline.txt` file.
4. At the end of the single line in the file, append:

   .. code-block:: text

      init=/bin/sh

5. Safely eject the SD card and reinsert it into the Raspberry Pi.
6. Boot the Pi. It will drop you into a root shell.
7. Remount the root filesystem as writable:

   .. code-block:: bash

      mount -o remount,rw /

8. Reset your user password (replace `pi` with your username):

   .. code-block:: bash

      passwd pi

9. After rebooting normally, remove the `init=/bin/sh` from `cmdline.txt`.

Mounting the SD Card on Another System
======================================

If you need to repair `sudo` from another machine:

1. Insert the SD card into a Linux machine.
2. Identify the device:

   .. code-block:: bash

      lsblk

   Typically `/dev/sda1` is the boot partition (FAT32) and `/dev/sda2` is the root filesystem (ext4).

3. Mount the root partition:

   .. code-block:: bash

      sudo mkdir -p /mnt/pi-root
      sudo mount /dev/sda2 /mnt/pi-root

Restoring Sudo
==============

To fix a broken `sudo`:

1. Ensure the `/usr` directory has correct ownership:

   .. code-block:: bash

      sudo chown -R root:root /mnt/pi-root/usr
      sudo chmod -R a+rX /mnt/pi-root/usr

2. Specifically fix the `sudo` binary:

   .. code-block:: bash

      sudo chown root:root /mnt/pi-root/usr/bin/sudo
      sudo chmod 4755 /mnt/pi-root/usr/bin/sudo

3. Verify the permissions:

   .. code-block:: bash

      ls -l /mnt/pi-root/usr/bin/sudo

   Correct output should resemble:

   .. code-block:: text

      -rwsr-xr-x 1 root root 165888 Jan 1 12:34 /mnt/pi-root/usr/bin/sudo

4. Sync and unmount the SD card:

   .. code-block:: bash

      sync
      sudo umount /mnt/pi-root
      sudo eject /dev/sda

Notes
=====

- Never run `chown` or `chmod` on the boot partition (`/dev/sda1`) because FAT32 does not support Linux ownership/permissions.  
- The setuid bit (`s`) on `/usr/bin/sudo` is critical; without it, `sudo` will not function.  
- This procedure can also be used to fix other permission issues on `/usr` or `sudo` after filesystem corruption.