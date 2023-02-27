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

## OS Responsibilities

1. **Process Management**: create, delete, suspend, resume, and schedule processes.
   - Provide mechanisms for process synchronization and communication.
2. **Memory Management**: allocate and free memory. Keep track of memory usage and location.
   - Provide mechanisms for memory sharing and protection.
   - Virtual Memory: Use disk as RAM to emulate more memory.
3. **File-System Management**: create, delete, open, close, read, and write files.
   - syscalls: `open`, `close`, `read`, `write`, `lseek`, and `stat`.
4. **Mass-Storage Management**: manage disk drives and file systems. Disk scheduling, partitioning and protection.
   - syscalls: `mount`, `umount`, `sync`, `reboot`, and `shutdown`.
5. **Cache Management**: manage cache memory. Cache replacement policies.
6. **I/O System Management**: memory management component that includes buffering, caching and spooling.

- **Security**: handle threats from outside of the system. User resources.
- **Protection**: handle threats from within the system. Programs and resources.

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

## Process Abstraction

- **Process** needs CPU, Memory, and I/O devices to complete a task.
  - **CPU**: Instruction Pointer (Program Counter) and Stack Pointer.
  - **Memory**: Set of memory addresses, Code (`cat/proc/<pid>/maps`).
  - **Disk**: Set of file descriptions (`cat/proc/<pid>/fdinfo`).
- **Thread** is a basic unit of CPU utilization. It is a light-weight process.
  - Has its own program counter, stack, register set, and thread ID.
- **Process Control Block**: contains all information about a process.

  - **Process State**: New, Ready, Running, Waiting, and Terminated.
  - **Process ID**: unique number assigned to a process.
  - **Program Counter**: address of next instruction to be executed.
  - **CPU Registers**: general purpose registers.
  - **CPU Scheduling Information**: priority, scheduling queue, and scheduling algorithm.
  - **Memory Management Information**: memory limits, page table, and memory maps.
  - **Accounting Information**: CPU time used, time limits, and accounting number.
  - **I/O Status Information**: I/O devices, open files, and pending I/O operations.
  - **Control Information**: parent process, process group, and session.

- **Creation**: System Initialization, Running Process, and User Request.
  - `fork` allows a parent process to create a child process. Returns 0 for new process and child's PID for parent.
    - Child process contains: address space that is a copy of the parent, register set, and PC.
- **Procedure**: Load code and static data, allocate memory, init stack and heap, init start I/O's, and execute.

### Limited Direct Execution

- Low-Level mechanism that implements user-kernel space separation.
- **Objective** is to virtualize CPU to allow OS to share CPU with multiple jobs and users at the same time.
- **Idea** is to run one process for a short time slice and sequentially on the CPU with no OS intervention.
- **Resources to limit**: Memory access, Disk I/O, x86 instructions.
- **syscall** is made for OS services and data returned to user space process after validating privileges.

## CPU Scheduling

- **Context Switching**: stores the state (context) of a process to be reloaded later.
  - **Context** includes CPU registers, open file descriptors, and state of the process.
  - `yield()` allows a thread/process to voluntarily give up the CPU to another.

- **Cooperative Multitasking**: OS never initiates a context switch. It is up to the process to yield.
- **Non-Cooperative Multitasking**: OS initiates a context switch based on external events
- **Preemptive Multitasking**: OS initiates a context switch on timer interrupt.
  - Timer interrupt is determined by hardware before running processes and switch() is called.

- In process lifecycle, a process alternates between a sequence of CPU and I/O Bursts.
  - **CPU Bursts**: total amount of time required by CPU to execute the process.
  - **I/O Bursts**: total amount of time for process waiting for I/O operation to complete.
- Maximize **Responsiveness** in Interactive Systems and **Not Miss Deadlines** in Real-Time Systems.
- CPU scheduler can be invoked when process starts/ends or switches states: ready, running and waiting.
  - Switch context, switch user mode, and traverse to user program location to restart execution.
- **Scheduler** - Policy:when and how to schedule.
- **Dispatcher** - Mechanism: Execute the scheduled process.

- Maximize CPU Utilization and Throughput. Minimize turnaround, waiting, and response times.
  - **CPU Utilization**: percentage of time the CPU is busy.
  - **Throughput**: number of processes that complete their execution per unit time.
  - **Turnaround Time**: time from submission to completion of a process. $T_{turn} = T_{finish} - T_{arrive}$
  - **Waiting Time**: time a process has been waiting in the ready queue. $T_{wait} = T_{start} - T_{arrive}$
  - **Response Time**: time from request to first (not complete) response. $T_{resp} = T_{first} - T_{arrive}$

- **Assumptions**: Jobs run for same time, arrive at same time, CPU no I/O, and run time is unknown.

### Scheduling Algorithms

- **FIFO**: First In First Out. Ordered by arrival time.
  - Non-preemptive. **Convoy effect** is when a long process blocks a short process.
- **SJF**: Shortest Job First. Ordered by next shortest CPU burst.
  - Non-preemptive by default. Can be preemptive by using **Shortest Remaining Time First**.
- **Round Robin**: Scheduled in order of arrival. Each process is given a time slice and preempted.
  - Preemptive and uses **Fixed Time Quantum** and prioritizes time sharing. wait - ready - run.
  - (+) Fairness and each process gets a chance to run and reschedule after a time quantum.
  - (-) Larger wait and response time. Low throughput. Time consuming for small time quantum.
- **Priority**: Scheduled in order of priority. Smallest integer is highest priority.
  - (-) **Starvation** is when a low priority process never gets to run.
    - **Ageing** increases priority of a process that has been waiting for a long time.
  - **Internal Factors**: timing constrains, memory requirements, ratio of CPU-I/O burst times.
  - **External Factors**: process importance, financial considerations, hierarchy among users.
- **Multilevel Feedback Queue**: Multiple queues with different scheduling algorithms and priority.
  - Optimize turnaround time and minimize response time.
- **Lottery** is a scheduling algorithm that randomly selects a process to run.

### Threads

- **Threads** can share memory space, code, data, and OS resources.
  - `thread_create` creates a new thread and `thread_join` waits for a thread to finish.
  - `thread_exit` terminates a thread and `thread_yield` gives up the CPU to another thread.
- **IPC** - Inter-Process Communication: allows processes to communicate with each other.
  - **Shared Memory**: share a common memory region. `shmget`, `shmat`, `shmdt`, and `shmctl`.
  - **Message Passing**: send messages to each other. `send` and `recv` can be blocking.
  - (-): Copying overhead, expensive context switching and hard to program/debug.
