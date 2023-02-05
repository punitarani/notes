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

## Examples

### Array Sum

#### `Worker.java`

```java
 // Worker inner class to add up a section of the array.
public class Worker extends Thread {
    int start;
    int end;
    double sum;
    double[] data;

    Worker(int start, int end, double[] d) {
        this.start = start;
        this.end = end;
        this.data=d;
        sum = 0;
    }


    // Computes the sum for our start..end section
    // in the array (client should call getSum() later).
    public void run() {
        for (int i=start; i<end; i++) {
            sum += data[i];
        }
        //sync.release();
    }

    public double getSum() {
        return sum;
    }
}
```

#### `addArrayThread.java`

```java
import java.util.*;
import java.util.concurrent.*;



public class addArrayThread {
    private double[] data;

    public addArrayThread(double[] data) {
        this.data=data;
    }

    public void runParallel() {
        int numWorkers = 10;

        // Make and start all the workers, keeping them in a list.
        List<Worker> workers = new ArrayList<Worker>();
        System.out.println(data.length);

        int lenOneWorker = data.length / numWorkers;
        for (int i=0; i<numWorkers; i++) {
            int start = i * lenOneWorker;
            int end = (i+1) * lenOneWorker;

            // Special case: make the last worker take up all the excess.
            if (i==numWorkers-1) {
                end = data.length;
            }

            Worker worker = new Worker(start, end, data);
            workers.add(worker);
            worker.start();
        }

        try {
            for(int i=0; i<workers.size(); i++) {
                workers.get(i).join();
            }
        } catch(InterruptedException ignored) {}


        // Gather sums from workers ()
        int sum = 0;
        for (Worker w: workers) {
            System.out.println(w.getName());
            System.out.println(w.getSum());
            sum += w.getSum();
        }

        System.out.println("len:" + data.length + " sum:" + sum + " workers:" + numWorkers);
    }
}
```

#### `runArraySum.java`

```java
public class runArraysum {
    public static void main(String[] args) {
        // command line argument: array_length
        int len = 10000000;
        double[] data = new double[len];
        for (int i=0; i<len; i++) {
            data[i] = i*1.2;
        }


        long startTime = System.currentTimeMillis();
        long endTime=0;
        addArrayThread at = new addArrayThread(data);
        at.runParallel();
        endTime = System.currentTimeMillis();

        System.out.println("time elapsed with thread" + (endTime - startTime));


        // The following code does the same operation above without thread
        startTime = System.currentTimeMillis();

        double[] array = new double[len];
        for (int i=0; i<len; i++) {
            array[i] = i*1.2;
        }

        double sum=0;
        for ( int i=0; i<len; i++) {
            sum += array[i];
        }

        endTime = System.currentTimeMillis();

        System.out.println("time elapsed without thread" + (endTime - startTime));
        }
    }
```

### Bank Account Synchronization

#### `DepositThread.java`

```java
public class DepositThread implements Runnable {
    private Account account;
    private double amount;

    public DepositThread(Account account, double amount) {
        this.account = account;
        this.amount = amount;
    }

    public void run() {
        account.deposit(amount);
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {}
    }
}
```

#### `WithdrawThread.java`

```java
public class WithdrawThread implements Runnable {
    private Account account;
    private double amount;

    public WithdrawThread(Account account, double amount) {
        this.account = account;
        this.amount = amount;
    }

    public void run() {
        account.withdraw(amount);
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {}

    }
}
```

#### `Account.java`

```java
public class Account {
    private double balance = 0;

    public Account(double balance) {
        this.balance = balance;
    }

    // if ‘synchronized’ is removed, the outcome is unpredictable
    public synchronized void deposit(double amount) {
        if (amount < 0) {
            throw new IllegalArgumentException("Can’t deposit.");
        }

        this.balance += amount;

        System.out.println("Deposit " + amount + " in thread" + Thread.currentThread().getId() + ", balance is " + balance);
    }

    // if ‘synchronized’ is removed, the outcome is unpredictable
    public synchronized void withdraw(double amount) {
        if (amount < 0 || amount > this.balance) {
            throw new IllegalArgumentException("Can’t withdraw.");
        }

        this.balance -= amount;

        System.out.println("Withdraw " + amount + " in thread " + Thread.currentThread().getId() + ", balance is " + balance);
    }
}
```

#### `InternetBankingSystem.java`

```java
// InternetBankingSystem.java: A simple program showing a typical invocation of banking operations via multiple threads.

import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class InternetBankingSystem {
    public static void main(String[] args) {
        Account accountObject = new Account(100);

        /* Without thread pool
        new Thread(new DepositThread(accountObject,30)).start();
        new Thread(new DepositThread(accountObject,20)).start();
        new Thread(new DepositThread(accountObject,10)).start();
        new Thread(new WithdrawThread(accountObject,30)).start();
        new Thread(new WithdrawThread(accountObject,50)).start();
        new Thread(new WithdrawThread(accountObject,20)).start();
        */

        // With thread pool
        ExecutorService executor = Executors.newFixedThreadPool(5);
        // ExecutorService executor = Executors.newSingleThreadExecutor();

        Runnable worker;
        for (int i = 0; i < 10; i++) {

            if (i % 2 == 0) {
                worker = new DepositThread(accountObject, i * 10);
            } else {
                worker = new WithdrawThread(accountObject, i * 5);
            }

            executor.execute(worker);
        }

        executor.shutdown();
        while (!executor.isTerminated()) {}
        System.out.println("Finished all threads");
    }
}
```
