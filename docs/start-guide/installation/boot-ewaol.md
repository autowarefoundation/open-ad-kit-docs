# Boot EWAOL

## Overview

You need to use SSD enclosure case to flash yocto image to M.2 SSD directly.

## Flash yocto image

Remove M.2 SSD from AVA platform and flash yocto image to it directly.

1. Remove M.2 SSD from AVA platform.

1. Install M.2 SSD into a M.2 enclosure case.

1. Plug it into your host machine.

1. Then, show available block devices.

   ```console
   lsblk -p
   NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
   ...
   /dev/sdb       8:0   0 119.2G  0 disk
   ├─sdb1         8:1   0   512M  0 part
   ├─sdb2         8:2   0     1G  0 part /media/foo/7d00c690-db24-462d-8c8d-dce7bdf151d8
   └─sdb3         8:3   0 117.8G  0 part
   ```

1. Flush yocto image to M.2 SSD.

   :speech_balloon: For example

   ```console
   sudo bmaptool copy --bmap build/tmp_baremetal/deploy/images/ava/ewaol-baremetal-image-ava.wic.bmap build/tmp_baremetal/deploy/images/ava/ewaol-baremetal-image-ava.wic.gz  /dev/sdb
   ```

## Extend rootfs partition

You have to extend rootfs partition. Follow the instructions [Extend rootfs partition](extend-rootfs.md)

## Reinstall SSD

1. Remove M.2 SSD from enclosure case and install it into AVA platform, then turn it on.

1. The following screen comes up, then login as `root` without password.

   ```console
   EWAOL (Edge Workload Abstraction and Orchestration Layer) v1.0 ava -
   ava login:

   ```

   :speech_balloon: You are able to access via SSH.
