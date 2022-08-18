# Extend rootfs partition

## Overview

The rootfs partition is not fully occupied on M.2 SSD, and the size is too short to run k3s clusters.
So we have to extend rootfs partition.

Here is the instruction how to extend rootfs partition

## Extend rootfs

1. Run `gparted`.

   You may get the following warning when you run `gparted`.

   Press `Fix`.

   ![Warning](images/extend-rootfs/gparted01.png)

   Contents of storage after we flashed yocto image to M.2 SSD.
   ![Contents of storage](images/extend-rootfs/gparted02.png)

1. Extend rootfs partition to the end of disk.

   Right click `root` partition, then click `Resize/Move`.
   ![Move data](images/extend-rootfs/gparted03.png)

   Extend the square to the right end.

   ![Extend root](images/extend-rootfs/gparted04.png)
   ![Root extended](images/extend-rootfs/gparted05.png)

   Then, click `Resize/Move`.

   ![Extend square](images/extend-rootfs/gparted06.png)

1. Apply changes.

   Click check mark icon.

   ![Apply changes](images/extend-rootfs/gparted07.png)

   Click `Apply`.

   ![Apply](images/extend-rootfs/gparted08.png)

   Click `Close`.

   ![Close](images/extend-rootfs/gparted09.png)

   You can get rootfs as follows.

   ![rootfs](images/extend-rootfs/gparted10.png)
