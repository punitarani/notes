# CPU Scheduling

- OS decides which process or thread to execute next.
- Responsible for allocating the CPU resources to different processes.
- Ensures efficient use of the CPU and fair chance for all process to execute.
- Different algorithms are used such as round-robin, first-come-first-served, or priority-based scheduling

## Process

- An instance of a running program.
- Has its own memory space, system resources and a set of instructions.
- Has a unique process identifier (PID) that allows the operating system to keep track of it.
- A process can be in one of several states: running, waiting, or terminated
- In multitasking operating systems, multiple processes can execute concurrently.

### Process Anatomy

- **Context**: current state of a process or thread, including its memory, system resources, and registers.
  - Includes information such as the current PC, the registers values, and memory contents.
  - **Context Switching**: The process of saving and restoring the state of a process or thread.

- **Program Counter (PC)**: The address of the next instruction to be executed by the CPU.
- **Stack Pointer (SP)**: The address of the top of the stack (used for function calls).
- **Registers**: A set of registers that are used to store data and addresses.
- **Memory**: The memory space allocated to the process to store data and instructions.
  - **Address Space**: Each process has its own unique address space, which is protected from other processes.
- **File Descriptors**: integer value assigned to an open file or (I/O) resource. Unique for each process.

### Process Creation

- Principle events that cause process creation
  - System initialization
  - Execution of a process creation system call by a running process
  - User request to create a process

- Creation Steps
  - Load the code and static data into memory
  - Initiate the Stack and Heap (small at first)
  - Initiate the start I/Os
  - Start the program at the entry point (e.g., start at main())
