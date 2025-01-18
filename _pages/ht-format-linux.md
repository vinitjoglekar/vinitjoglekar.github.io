---
layout: default
title: How to format a drive on Linux?
---

# How to format a drive on Linux?

1. Check the device name of the drive using `lsblk` command. Using `df` command, verify that the drive is not mounted. If it is mounted, unmount it.
    - Let's suppose, for example, that the device is `/dev/sda`.
2. Open the device using `fdisk`: `fdisk /dev/sda`. You may need super user privileges for this.
3. All the `fdisk` commands with a short description of each, may be listed using `m` command.
4. Delete any existing partitions using `d` command.
5. Create a new partition using following sequence of commands: `n` (new partition), `p` (primary), `[enter]`, `[enter]` (select default first and last sectors)
6. Assign a type to the partition using commands: `t` (change the partition type), `L` (list all the available partition types), `07` (for NTFS - do not select 86 or 87, those are for volume sets).
7. View the changes you are about to make using command `p`, and write them using command `w`.
8. Now the device should have the partition `/dev/sda1` on it - you can verify this using `lsblk` command.
9. Create NTFS fileystem on `/dev/sda1` using command: `mkfs.ntfs --label MY_LABEL --verbose /dev/sda1`. You may need super user privileges for this.

Note that, if your device size is larger than 2TB, you should use `gdisk` instead of `fdisk`.
 


