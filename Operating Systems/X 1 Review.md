# Operating Systems Review 1

## Topics

- Operating System Architecture and Responsibilities
- Components of OS and their responsibilities
- How is an Operating System loaded?
- Resource Allocation
- Interrupts, Graphs associated with Interrupts, Interrupt Handler Routines, Interrupt request line
- Multiprocessor Architecture
- SMP
- Multiprogramming and multitasking
- User Mode/Kernel Mode
- System Calls
- Resource Management
- Protection and Security
- Processes and Programs
- Threads/Multithreading
- Caching
- Preemptive vs. Non-preemptive
- CPU Scheduling Algorithms

## General

- **Computer Architecture**: Hardware - Operating System - Application Programs - User Instructions
- **Resource Allocation**: CPU Time, Memory Allocation, Storage, and I/O Devices.
- **Operating System**: Centralized Software Architecture responsible for computer's functionalities:
  - Scheduling Tasks
  - Executing Application
  - Controlling Peripherals
  - Managing Memory and CPU Processing
  - Storage Management and Data Handling
  - Network Management
- **OS Objectives**: Resource Efficiency (Virtualization), Ease of Use, and Reliability (Security).
- **Computer System Organization**: Bus, Interrupts, Storage Structure, I/O Structure.

- **Cache** stores frequently accessed data in faster memory.
  - Skew Rule: 80% requests hit on 20% frequented data.
- **Cache Coherency**: maintain consistency of cached data with multiprocessor environments.

## Interrupts

- **Interrupt** is an attention request for CPU time to signal an event from hardware during execution.
  - **Interrupt Request Line**: Hardware signal to CPU to request attention.
  - **Interrupt Handler Routine**: Software routine to handle interrupt.
  - **Non-maskable Interrupt**: Interrupt that cannot be disabled. Ex: unrecoverable hardware error.
  - **Maskable Interrupt**: Interrupt that can be disabled by software. Ex: keyboard input.
  - **Interrupt Chaining**: Multiple interrupt handlers are linked together and executed in sequence.
  - **Interrupt Priority Levels**: 0-18 NMIs. 15, 19-31 are intel reserved. 32-255 are maskable.
- **Interrupt Objectives**: deferrable handling, efficiently dispatch handlers, and multi-level priority.

## Multiprocessing

- **Shared System Interconnect**: Allows multiple processors to communicate with each other.
  - **NUMA (Non-Uniform Memory Access)**: Multiple processors access different regions of memory at different speeds.
    - (+) Scale more effectively as CPU accesses memory faster and there is no contention over the SSI.
    - (-) Increased latency as CPU accesses over SSI is slower reducing performance.
- **Symmetric Multiprocessing (SMP)**: Each processor performs all tasks, including OS functions and user programs.
- **Symmetric Clustering**: 2+ hosts running the same applications and monitoring each other.
- **Parallelization**: divide program into smaller tasks and run them in parallel on different processors.
- **Multiprogramming**: organize multiple programs to run a single CPU to increase CPU utilization.
- **Process** is a program in execution.
- **Multitasking**: Emulate running multiple processes concurrently by switching between them.

## Modes

- Guarantee proper execution of programs by distinguishing between User and OS code.
  - **User Mode**: computer is executing on behalf of a user application.
  - **Kernel Mode**: user application requests a service from the OS via syscalls.
  - **Supervisor Mode**: a mode above user mode that allows privileged instructions to be executed.
  - **System Mode**: run operating system tasks that do not need access to privileged resources.
  - **Privileged Mode**: allows certain system-level operations to be performed by kernel or system admin.
- **Protection Rings**: 0-3. 0 is most privileged and 3 is least privileged.
  - (-3 : -1) Management Engine(ME), System Management Mode(SMM), Hypervisor.
  - (0 : 3) Kernel, Device Drivers, Device Drivers, User Applications.

## System Calls

- **System Call** is a request for a service from the OS.
  - Interface between an executing program and teh operating system
  - **System Call Interface**: a set of functions that an application program can use to request a service from the OS.
  - **System Call Handler**: a function that is invoked by the OS to handle a system call.
  - **System Call Number**: a unique number assigned to each system call.
  - **System Call Table**: a table of system call numbers and their corresponding system call handlers.
  - **System Call Parameters**: data that is passed to the system call handler.
  - **System Call Return Value**: data that is returned to the application program.
