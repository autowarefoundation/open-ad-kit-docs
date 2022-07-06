# Boot EWAOL via SSD Boot

## Overview

You need to use SSD enclosure case to flash yocto image to M.2 SSD directly.

## Get yocto image

1. Build yocto image with EWAOL by following the instructions [Getting started with EWAOL](getting-started.md), or Download the image from the website to your host machine;
   - [AVA Developer Platform Downloads – I-Pi SMARC](https://www.ipi.wiki/pages/download-ava-developer-platform) (:white_check_mark: `Yocto with SOAFEE` is preferred.)

## Flash yocto image

Remove M.2 SSD from AVA platform and flash yocto image to it directly.

1. Remove M.2 SSD from AVA platform.

1. Install M.2 SSD into a M.2 enclosure case.

1. Plug it into your host machine.

1. Then, show available block devices.

   ```console
   lsblk
   NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
   ...
   sdn           8:208  0 119.2G  0 disk
   ├─sdn1        8:209  0   512M  0 part
   ├─sdn2        8:210  0     1G  0 part /media/foo/7d00c690-db24-462d-8c8d-dce7bdf151d8
   └─sdn3        8:211  0 117.8G  0 part
   ```

1. Flush yocto image to M.2 SSD.

   :speech_balloon: For exmple

   ```console
   sudo dd if=ewaol-image-docker-comhpc-20211022083723.rootfs.wic of=/dev/sdn bs=1M status=progress && sync
   ```

## Extend rootfs partition

You have to extend rootfs partition. Follow the instructions [Extend rootfs partition](extend-rootfs.md)

## Reinstall SSD

1. Remove M.2 SSD from enclosure case and install it into AVA platform, then turn it on.

1. The following screen comes up, then login as `root` without password.

   ```console
   EWAOL (Edge Workload Abstraction and Orchestration Layer) 0.1 comhpc tty1
   comhpc login:



   ```

   :speech_balloon: You are able to access via SSH.
