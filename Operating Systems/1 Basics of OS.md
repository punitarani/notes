# Basics of Operating Systems

## Operating System

An operating system (OS) is a software that manages computer hardware and software resources and provides common services for computer programs.
It is the primary interface between a human and a computer.

### Responsibilities

- **Process Management**: Schedule programs for execution and coordinate their execution.
- **Job Management**: Manage the execution of jobs and the allocation of resources to jobs.
- **Device Management**: Managing connected devices, peripherals and their drivers.
- **File Management**: Manage files and directories.
- **Memory Management**: Manage memory allocation and de-allocation and memory protection for processes.

## Processing

Processing is the execution of a program by a computer.

### Batch Processing

Jobs are queued, executed and results rendered.
Batch processing is essentially a series of scheduled programs that require no external influence.

### Interactive Processing

Programs with Input and Output.
Many programs are interactive in nature.
Interactive programs require some for of user interaction to accomplish goals that the user sets forth.

### Multiprocessing/Multithreading

Multiple processes working with shared data.
It allows multiple programs to run simultaneously to increase the overall efficiency of the system.
This can lead to problems from concurrency errors to race conditions and deadlocks.

## Foundational Components

### Shell

Shell is the outermost layer of an OS and is the interface between the user and the computer.
It is a command line interpreter that accepts commands from the user and passes them to the OS to be executed and returns the results to the user.
It uses a specific programming language (Ex: Bash for Linux and Batch for DOS) to interpret the commands.

### Kernel

The kernel is the core and the non-replaceable portion of the OS.
It consists of multiple managers that manage the resources of the computer.

#### Memory Manager

The memory manager is responsible for managing the memory (RAM) allocation and de-allocation and memory protection for processes.

- Static Memory: Static and Global variables. Allocated at compile time.
- Stack Memory: Local and non-static variables. Allocated at run time.
- Heap Memory: Dynamic allocation. Allocated at run time.

$\text{(slowest) Disk} \rightarrow \text{RAM} \rightarrow \text{Cache} \rightarrow \text{Register (fastest)}$

The memory manager shuffles data between the RAM and Register most of the time and to Disk for permanent storage.

##### Virtual Memory

Virtual memory is a memory management technique that allows a computer to use a portion of its hard disk as if it were RAM.
The memory manager also handles virtual memory by shifting pages of data between RAM and Virtual Memory.

#### File Manager

The file manager, or file system, is responsible for managing, storing, and retrieving files and directories on the disk.

It consists of three layers:

1. Logical File System
   - Provides an API for file management to applications.
2. Virtual File System
   - Interface to allow concurrent instances of the physical file system.
3. Physical File System
   - Actual storage of files and directories.
   - Handles buffering, memory management, and disk management.
   - Interacts with the device drivers to read and write data to the disk.

A directory, or folder, is a collection of files and other directories to add logical structure to managing them.
Each directory has a path to describe its full organizational structure

The file manager works with different types of files:

- Ordinary Files
  - Files created by the user and applications
  - Consist of useful data. Ex: text, byte data, executables, etc.
  - User can add, modify, and delete them.
- Directory Files
  - They contain lists of file names and other information related to those files.
- Device/Special Files
  - They represent devices and other special resources.
    - Character Special Files: data is handled as a stream of characters (Ex: printers, terminals, etc.)
    - Block Special Files: data is handled as a stream of blocks (Ex: disks, etc.)

##### Space Management

Files are allocated space on the disk in blocks which is organized by it.

There are 3 allocation methods:

1. Contiguous Allocation
   - Files are allocated space in contiguous blocks.
   - Addresses are assigned in linear order.
   - Easy to implement.
   - Fragments are created resulting in wasted space and slow access times.
2. Linked Allocation
   - Files are comprised of list of links to disk blocks.
   - Can be implemented as a linked list.
   - Inefficient especially for direct file access.
3. Indexed
   - Creates a indexed block of pointers to files.
   - Each file has an index block that contains pointers to the blocks that contain the file data.
   - Most robust and efficient system that is used by most OSs.

##### File Access

1. Sequential
   - The _default_ method of file access where the file chunks are accessed in order.
2. Direct/Random
   - Data chunks (records) are assigned their own addresses.
   - Each record is accessed directly via these addresses.
   - Records can be in any sequence.
3. Indexed
   - File chunks are indexed
   - The indices are accessed sequentially
   - Pointers allow for direct access to records

#### Device Manager

The device manager is the replaceable portion of the OS.
It is responsible for managing the connected devices and their drivers.

#### Process Manager

The process manager is responsible for scheduling programs for execution and coordinating their execution.
It handles the creation, termination, and synchronization of multiple and concurrent processes.

## Booting Up

The Bootstrap is a program in ROM that is transferred to RAM and executed by the CPU.
It is responsible for loading the OS into memory and starting the OS.

## Program vs Process

### Program

A Program is a set of instructions that is stored on the disk.
It is meant to be executed at a later time.

### Process

A Process is an instance of a program that is loaded into the RAM and being executed.
It has a process state including:

- Program Counter: what instruction to execute next.
- Register Values: The values of the registers.
- Memory contents: the data from memory required to run the program.

## Virtual Machine

A virtual machine is a software that emulates a computer system and allows multiple operating systems to run on the same hardware.
It allows for an executable to be run on a controlled OS environment within the host OS increasing the portability of the executable.

## Multitasking

The OS has a scheduler that is responsible for allocating CPU time for processes to run next.
The dispatcher is responsible for switching between states and controlling the time slices for each process.

### Multitasking Issues

- Concurrency problems
  - Two processes/threads accessing the same resource at the same time introduce inconsistences in data and error.
- Race Conditions
  - Two or more processes/threads compete for the same data or resources.
  - Faster processes/threads can finish before slower processes/threads.
  - Slow processes/threads can create bottlenecks.
- Deadlock
  - Multiple processes have competing actions that prevent each other from completing.

#### Solutions to Multitasking Issues

- Spin Locks allows the shared resource is locked until a process/thread is done with their task.
- Code better algorithms to anticipate deadlock and recover from it.
