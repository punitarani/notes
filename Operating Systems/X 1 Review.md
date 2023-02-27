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
