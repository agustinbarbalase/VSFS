# Very simple filesystem

- Introduction
- Structure
- Library

## Introduction

The idea for this project is inspired in a laboratory of subject [Operating System at FIUBA](https://fisop.github.io/website/),
the lab required a filesystem with basic operations and persistency. The current implementation is a Very simple
filesystem with the same requirement.

## Structure

The filesystem have five parts:

1. Superblock
2. Bitmap of inodes
3. Bitmap of data blocks
4. Inodes
5. Data blocks

The first is the metadata about the filesystem, the next two are the data structures needed to know which inodes or
data blocks are free or not. The inodes are the representation of a file in the filesystem, and the data blocks are
the information of the file itself.

Imagine you have a disk with 4096 4KB blocks and the size of an inode is 256 bytes. How many Inodes and data blocks
does our file system have?

```txt

> 4096 blocks / 256 bytes per inode = 16 inodes per block

> 4KB = 4096 bytes

> 4096 bytes per block / 16 inodes per block = 256 block of inodes

> 4096 - 256 - 3 = 3837 Data blocks

The representation of filesystem is the next:

+------+------+------+-------------------+------------------+
|      |      |      |                   |                  |
|  SB  |  BI  |  BD  | 256 Inodes blocks | 3837 Data blocks |
|      |      |      |                   |                  |
+------+------+------+-------------------+------------------+

```

## Library

For developed the project use [FUSE](https://github.com/libfuse/libfuse), it's a filesystem in userland.
