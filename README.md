# OSlab Project 5 - Defragmentation

  Authorize by 赵菁菁  
  Stu_ID: 10152130149
  Date: 2017.12.30

## Overview
  This assignment acquires us to write a file defragmentation code file. We should read the given disk file, then defragment the file system embedded in it. 

## the disk partition
Two data structures are important in this homework -- superblock and inode.

The disk is divided into a series of blocks.
On disk, the first block contain the bootblock. 
The second block contain the superblock, which includes a lot of information about inodes.
The inodes region at inode_offset number block

The overall on-disk organization of the data structures of the file system is as follows:
> bootblock |  superblock  | null |  inode | inode | inode | inode | null | data region | ... |

## how to implement the defragmentation
My defragmenting process in this part:

1. Read and copy the same boot block.

2. Read the original superblock.
a new superblock with the same list of free inodes 

3. data blocks at their new locations.
    * find the file's datablocks and read them one by one
    * reallocate datablock numbers and write data to outfile 
    value of free blocks (sorted from lowest to highest to help prevent future fragmentation) 
    
4. update the superblock and inodes
build the new in

## test correctness 
  For each inode, I went through blocks of its data region to extract every file.<br>
  I wrote extracting file code in 'extract.c'. <br>
  There are three files whose nlink is 0, which means they are unused. So only the left 17 files are extracted.<br>


## what's more
    1. I find the swap_offset in superblock is 10243, which means the file system has overall 10243 blocks and the size is 10243 * 512 = 5,244,416 bytes. 
    But the original datafile has only 5,243,392 bytes, which is 10241 blocks. 
    So the original file loses 2 blocks, and my output file is 1024 bytes larger. 
