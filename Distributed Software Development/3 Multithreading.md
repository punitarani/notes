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

## Thread implementation in Java

1. Extend the `Thread` class
2. Implement the `Runnable` interface
3. Implement the `Callable` interface
4. Use `java.util.concurrent` package's `ThreadPool` and `Executor`

### Extending the `Thread` class

- The `Thread` class is a subclass of `Object` and implements `Runnable` interface.

```java
public class ThreadA extends Thread {
    private String name;

    public ThreadA(String name) {
        this.name = name;
    }

    public void run() {
        System.out.println("Hello from " + name);
    }
}
```

### Implementing the `Runnable` interface

- The `Runnable` interface has a single method `run()` that is called when the thread is started.

```java
import java.lang.Runnable;

public class ThreadB implements Runnable {
    private String name;

    public ThreadB(String name) {
        this.name = name;
    }

    public void run() {
        System.out.println("Hello from " + name);
    }
}
```

### Implementing the `Callable` interface

- The `Callable` interface is similar to `Runnable` but it can return a value.

```java
import java.util.concurrent.Callable;

public class ThreadC implements Callable<String> {
    private String name;

    public ThreadC(String name) {
        this.name = name;
    }

    @Override
    public String call() throws Exception {
        Thread.sleep(1000);
        return "Hello from " + name;
    }
}
```

- Unlike the others, `Callable` returns a value and can throw an exception.

### Using `ThreadPool` and `Executor`

- The `ThreadPool` and `Executor` classes are used to create and manage threads.

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class SimpleThreadPool {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(5);

        for (int i = 0; i < 10; i++) {
            String name = "Thread " + i;

            Runnable worker = new ThreadB(name);
            executor.execute(worker);
        }

        executor.shutdown();
        while (!executor.isTerminated()) {
            // Wait for all threads to finish
        }

        System.out.println("Done");
    }
}
```

### Running Java Threads

```java
public class RunThreads {
    public static void main(String[] args) {
        ThreadA a = new ThreadA("Thread A");
        ThreadB b = new ThreadB("Thread B");
        Thread b1 = new Thread(b);

        // Start the threads
        a.start();
        b1.start();

        // Wait for the threads to finish
        try {
            a.join();
            b1.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Done");
    }
}
```

- `start()` starts the thread.
- `join()` waits for the thread to finish.

## Thread implementation in C#

There are 3 ways to create a thread in C#:

Method 1: Using the `Thread` class

```C#
Thread thread1 = new Thread("Thread 1");
thread1.Start();
thread1.Join();
```

Method 2: Using the `ThreadStart` delegate

```C#
Thread thread2 = new Thread(new ThreadStart("Thread 2"));
```

Method 3: Using Lambda expressions

```C#
Thread thread3 = new Thread(() => SomeMethod());
thread3.Start();
```

### Synchronization

- Producer and consumer are two threads that share a common resource.

  - Producer produces data and puts it in the resource.
  - Buffer is a resource that is shared by the producer and consumer.
  - Consumer consumes data from the resource.

- Synchronization is used to ensure that only one thread can access the resource at a time.
- **Synchronized Methods**: `synchronized` keyword is used to make a method synchronized.
  - Only one thread can execute a synchronized method at a time.
  - Other threads that try to execute the method are blocked until the method is finished.

`synchronized` code example:

```C#
public class Counter {
    private int count = 0;
    private bool locked = false;

    public synchronized void increment() {
        while (locked) {
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        count++;
        locked = true;
        notify();
    }

    public synchronized void decrement() {
        while (locked) {
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        count--;
        locked = true;
        notify();
    }

    public synchronized int getCount() {
        while (!locked) {
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        locked = false;
        notify();
        return count; }
}
```

### Monitor

- **Monitor**: A monitor is an object that is used to control access to a shared resource.
  - It uses `Enter` and `Exit` methods to control access to the resource.
  - A monitor is associated with a class or an object.
  - A monitor is entered when a thread executes a synchronized method or block.
  - A monitor is exited when a thread finishes executing a synchronized method or block.
  - Only one thread can enter a monitor at a time.
  - Other threads that try to enter the monitor are blocked until the monitor is exited.

Monitor code example:

```C#
public void produce() {
    for (int i = 0; i < 10; i++) {
        Monitor.Enter(SomeClass.buffer);
        try {
            SomeClass.buffer.set(i);
            Console.WriteLine("Produced: " + i);
        } finally {
            Monitor.Exit(SomeClass.buffer);
        }
    }
}
```

```C#
public void consume() {
    for (int i = 0; i < 10; i++) {
        Monitor.Enter(SomeClass.buffer);
        try {
            int value = SomeClass.buffer.get();
            Console.WriteLine("Consumed: " + value);
        } finally {
            Monitor.Exit(SomeClass.buffer);
        }
    }
}
```
