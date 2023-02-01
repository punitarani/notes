# Multithreading

- Multithreading is a way of executing multiple threads simultaneously within a process.
- OS performs process scheduling and resource allocation.
  - System calls allow user to create, manage, and synchronize processes.
- It is critical to ensure that the threads do not interfere with each other.

- Multiple processors are necessary for multithreading to be effective.
  - With single processor, time-sharing is used to simulate multithreading.

## Process/Thread vs Program/Method

- A program/method is a piece of code that is executed (static).
- A process/thread is an instance of a program/method that is executed (dynamic).
  - Exists only when the program/method is being executed .
  - Includes current values, state information and resources allocated to it.
  - Each thread has its own stack, but shares the heap with other threads.
- Each process has its own address space and memory space: it is isolated from other processes.
  - Processes can communicate with each other through inter-process communication (IPC) like pipes, sockets, and shared memory.
- Threads can share the same address space and memory space with other threads in the same process.
  - Locks and semaphores are used to ensure that only one thread can access shared resource at a time.
