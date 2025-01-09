# How To Configure Storage On Linux
- URL: https://embeddedprojects101.com/the-beginners-guide-to-linux-storage-configuration/
- Added At: 2025-01-09 09:58:34
- [Link To Text](2025-01-09-how-to-configure-storage-on-linux_raw.md)

## TL;DR
本文介绍了Linux系统中存储管理的基本概念和命令，包括块设备命名、分区、文件系统、挂载以及逻辑卷管理器（LVM）的使用。通过关键命令如`lsblk`、`fdisk`、`mkfs`、`mount`等，用户可以管理存储设备、创建分区和文件系统，并实现动态调整逻辑卷大小。LVM提供了灵活的存储管理功能，适合初学者学习。

## Summary
1. **文章简介**：本文介绍了在Linux系统中配置存储的基本概念和命令，适合初学者学习如何管理块存储设备、分区、文件系统以及逻辑卷管理器（LVM）。

2. **主要内容**：
   - **块存储设备命名**：Linux将存储设备视为文件，存储在`/dev`目录下，设备文件的命名取决于设备的总线类型和插入顺序。
   - **分区**：分区是将块设备划分为逻辑块设备的过程，常用的分区方案有MBR和GPT。
   - **文件系统**：文件系统是建立在分区之上的逻辑抽象层，常见的文件系统类型有ext4和xfs。
   - **挂载文件系统**：挂载是将文件系统链接到系统文件层次结构中的操作，挂载点是一个目录。
   - **逻辑卷管理器（LVM）**：LVM是一种Linux存储技术，提供了逻辑卷、精简配置、快照和软件RAID等高级功能。

3. **详细内容**：
   - **块存储设备命名**：
     - SCSI或SATA设备命名为`sda`、`sdb`等，NVMe设备命名为`nvme0n1`、`nvme0n2`等。
     - 使用`ls /dev`命令可以列出所有块设备。
   - **分区**：
     - 使用`lsblk`命令列出所有磁盘和分区。
     - 使用`fdisk`或`gdisk`命令创建分区。
     - 分区表存储在磁盘的前几个扇区中，包含分区的起始和结束扇区信息。
   - **文件系统**：
     - 使用`mkfs`命令创建文件系统，如`mkfs -t xfs /dev/sdb1`。
     - 文件系统创建后需要挂载到目录上才能使用。
   - **挂载文件系统**：
     - 使用`mount`命令挂载文件系统，如`mount /dev/sdb1 /data`。
     - 使用`df -h`命令查看已挂载的文件系统。
     - 挂载信息可以写入`/etc/fstab`文件以实现持久化挂载。
   - **LVM**：
     - LVM由物理卷（PV）、卷组（VG）和逻辑卷（LV）三层组成。
     - 使用`pvcreate`命令创建物理卷，`vgcreate`命令创建卷组，`lvcreate`命令创建逻辑卷。
     - 逻辑卷可以动态调整大小，卷组可以动态添加物理卷。

4. **关键命令**：
   - `lsblk`：列出块设备。
   - `gdisk`、`fdisk`：创建分区。
   - `mkfs`：创建文件系统。
   - `mount`：挂载文件系统。
   - `df`：查看已挂载的文件系统。
   - `pvcreate`、`vgcreate`、`lvcreate`：LVM相关命令。

5. **总结**：
   - Linux将块存储设备视为文件，存储在`/dev`目录下。
   - 使用分区、文件系统和挂载操作来管理存储空间。
   - LVM提供了灵活的存储管理功能，支持动态调整逻辑卷大小。
   - 关键命令包括`lsblk`、`gdisk`、`fdisk`、`mkfs`、`mount`、`df`、`pvcreate`、`vgcreate`、`lvcreate`。

6. **推荐资源**：推荐阅读Sander Van Vugt的《Red Hat RHCSA 9 Cert Guide: EX200》以深入学习Linux存储管理。
