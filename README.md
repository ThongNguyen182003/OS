# Simple-FS Overview

Simple-FS is the file system component of the Simple-OS project. It is designed to implement multiple file systems using the FUSE interface—with the long-term goal of integrating this code into the Simple-OS kernel.

## Key Functional Areas

### 1. Userspace (FUSE Interface)
- **FUSE-Based File System Driver:**  
  Provides a user-space implementation of common file system operations such as directory listing, file creation, reading, and writing.
- **Hand-Crafted File System Implementation:**  
  A simple file system designed for educational purposes. It implements basic FUSE interfaces and stores file metadata (e.g., file names, attributes, sizes) and data blocks in a disk image.
- **FAT-32 File System:**  
  Implements most common read/write operations for FAT-32 (with some simplifications like limited Unicode support).  
- **Supporting Tools:**  
  Includes utilities like formatting tools (`make_fs.*`) and an adapter (`fuse_fs.c`) that bridges the VFS (Virtual File System) abstraction to the FUSE layer.

### 2. Kernel/Driver Layer (Future Integration)
- **Block I/O Abstraction (`block_io.*`):**  
  Provides a generic interface for reading and writing sectors, which is crucial for eventual integration into the kernel.
- **Plan for Kernel Integration:**  
  The roadmap includes implementing system calls for file I/O and porting the FUSE file system code into the kernel. This would ultimately allow the OS to perform file operations directly through kernel-level drivers (e.g., ATA operations).

## Dependencies and Build Environment
- **Compiler:** Tested with GCC.
- **FUSE Libraries:**  
  - **Linux:** Uses libfuse (e.g., libfuse3-dev on Ubuntu 20.04 LTS).  
  - **macOS:** Uses macFUSE.

## Summary
Simple-FS bridges user-space file system operations with low-level block I/O functionality. Initially implemented as a FUSE-based system in userspace for ease of development and testing, its design is aimed at a future transition into the Simple-OS kernel, where file operations will be managed directly at the driver level.
