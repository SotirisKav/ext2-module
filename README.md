# Ext2 Filesystem Implementation

This repository contains a Linux kernel module that implements the Second Extended Filesystem (ext2). The project demonstrates how to interface with the Linux Virtual File System (VFS) subsystem to handle low-level storage operations.

The driver is capable of parsing ext2 on-disk structures, managing inodes, and performing directory traversal. It maps standard system calls (like mount, open, and ls) to specific low-level operations defined in the kernel's `super_operations`, `inode_operations`, and `file_operations` structures.

## Project Description

The implementation breaks down the filesystem logic into modular components, mirroring the architecture of the Linux kernel's native ext2 driver:

* **Superblock Management (`super.c`):** Handles the mounting process. It reads the filesystem superblock from the disk to verify the "magic number" and initializes the in-memory `super_block` structure.
* **Inode Operations (`inode.c`):** Implements the logic for reading and writing inode metadata. This includes mapping logical block numbers to physical disk blocks using direct and indirect pointers.
* **Directory Handling (`dir.c`, `namei.c`):** Manages directory entries. `namei.c` specifically handles path resolution (looking up a filename to find its corresponding inode number).
* **Allocation Bitmaps (`balloc.c`, `ialloc.c`):** These files manage the block bitmap and inode bitmap, which track free and used space on the disk. They are responsible for finding free blocks when new files are created or expanded.

## Prerequisites

* Linux Kernel Headers (required to compile kernel modules)
* GCC compiler
* Make
* Root privileges (required to insert the module and mount filesystems)

## Building the Module

To compile the source code into a kernel object (`.ko`) file, run the following command in the root directory:

```bash
make
