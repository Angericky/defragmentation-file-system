# OSlab Project 5 - Defragmentation

  赵菁菁  Stu_ID:  10152130149<br>
  2017.12.30

## Overview
  This assignment acquires us to write a file defragmentation code file. We should read the given disk file, and defragment the file system embedded in it. 

## the disk partition
The overall on-disk organization of the data structures of the file system is as follows:
    
> bootblock
		| boot | superblock | inode1~5 | inode6~10 | inode11~15 | inode16~20 | null | dblock | iblock | null | dblock | ... |
