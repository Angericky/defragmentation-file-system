# OSlab Project 5 - Defragmentation

  Authorize by 赵菁菁  
  Stu_ID: 10152130149
  Date: 2017.12.30

## Overview
  This assignment acquires us to write a file defragmentation code file. We should read the given disk file, then defragment the file system embedded in it. 

## the disk partition
Two data structures are important in this homework -- superblock and inode.

The disk is divided into blocks.
On disk, the first block contain the bootblock. 
The second block contain the superblock, which includes a lot of information about inodes.
The inodes region at inode_offset number block


The overall on-disk organization of the data structures of the file system is as follows:
> bootblock |  superblock  | null |  inode | inode | inode | inode | null | data region | ... |



is simple: a series of blocks, each of size 4 KB. The blocks are addressed from 0 to N − 1, in a partition of size N 4-KB blocks.


## how to implement the defragmentation
After defragmenting, your new disk image should contain:

the same boot block (just copy it),
a new superblock with the same list of free inodes but a new list of free blocks (sorted from lowest to highest to help prevent future fragmentation),
new inodes for the files,
data blocks at their new locations.

## test accuracy
For each inode, I went through blocks of its data region to extract every file.
I wrote extracting file code in 'extract.c'. 
There are three files whose nlink is 0, which means they are unused. So only the left 17 files are extracted.


## what's more
1. I find the swap_offset in superblock is 10243, which means the file system has overall 10243 blocks and the size is 10243 * 512 = 5,244,416 bytes. 
But the original datafile has only 5,243,392 bytes, which is 10241 blocks. 
So the original file loses 2 blocks, and my output file is 1024 bytes larger. 
