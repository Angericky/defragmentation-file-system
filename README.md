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
The inodes region begins at (inode_offset + 2) block, and the number of inode is  (data_offset - inode_offset) * blocksize / sizeof(inode).
The data region starts at (data_offset + 2) block, contains different file data of inodes.

The overall on-disk organization of the data structures of the file system is as follows:
> bootblock |  superblock  | null |  inode | inode | inode | inode | null | data region | ... |

## how to implement the defragmentation
My defragmenting process in this part:

1. Read and copy the same boot block.

2. Read the original superblock and inodes. 

3. data blocks at their new locations.<br>

I maintain two global variables -- cur_pos & data_blk_sz.<br>
The former refers to the smallest number of free blocks in data region at present, and the latter refers to the number of data blocks  left to be read in the current file.<br>

  * go through the file's datablocks sequently by DFS algorithm(sorted from lowest to highest to help prevent future fragmentation) 
  * reallocate datablock numbers, update block_num values in the inode
  * write inode and data block to outfile 

4. update the superblock and inodes
Update the value of 'free_iblock' in superblock and write it.(Use fseek() to location the superblock position in output file.)
inode

## test correctness 
  For each inode, I went through blocks of its data region to extract every file.<br>
  I wrote extracting file code in 'extract.c'. <br>
  There are three files whose nlink is 0, which means they are unused. So only the left 17 files are extracted.
  
### The types and sizes of files are:
    1  94.2kB  Document      2  182.3kB image       3 42.5kB Program
    4  512B    Binary        5  11.3kB  Text        6 17.4kB Program
    7  2.6kB   Binary        8  15.4kB  Unknown     9 22.0kB Text
    10  20.5kB  Program      11 512B    Binary      12 230.4kB Program
    13  1.5kB   Program      14 4.1kB   Text        15 2.0kB Binary
    16  250.9kB Document     17 184.3kB Text
  Using the same code, the disk after my defragmentation can also be extracted the same 17 files.
  
## what's more
2. I find the swap_offset in superblock is 10243, which means the file system has overall 10243 blocks and the size is 10243 * 512 = 5,244,416 bytes.  
    But the original datafile has only 5,243,392 bytes, which is 10241 blocks.  
    So the original file loses 2 blocks, and my output file is 1024 bytes larger. 
