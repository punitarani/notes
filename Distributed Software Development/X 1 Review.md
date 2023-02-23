# CSE 445 Midterm 1 Cheatsheet

## Topics

Covers concepts from Weeks 1 to 6.

- What is distributed computing
- Basic principles of service oriented computing
- How service oriented computing differs from multithreaded applications in a multicore architecture
- What is web service?
  - Why web services are regarded as interoperable
- Read a WSDL document and understand the structure of the web service
  - Name, data types, method names ... etc
- Service Oriented Software Development and Applications
- RESTful web services
- General Issues of Multitasking and Multithreading
- Different ways to implement threads in Java
  - Method level, object instance level, class level locks
  - Thread synchronization
  - Thread lifecycle
- Multithreading in C#
  - How threads are created in C#
  - Thread synchronization
  - Delegates, Events, and Event Driven Programming

### Format

- 70% Multiple Choice
- 30% Short Answer
  - Fundamental concept explanation and applicability
  - Determine output and issues of code snippets
  - Complete the partial code snippets

## Architectures

- **2 Tier**: Client and Server
- **3 Tier**: Presentation, Application Processing and Data Management
- **4 Tier**: Service Repository Layer

### Computer Architecture (Flynn's Classification)

- **SISD**: Single Instruction (stream), Single Data (stream).
  - Simple computers
- **SIMD**: Single Instruction (stream), Multiple Data (streams)
  - Vector or array computers
- **MISD**: Multiple Instruction (streams), Single Data (stream)
  - Fault-tolerant computers
  - Redundant computing on same data and voting on results
- **MIMD**: Multiple Instruction (streams), Multiple Data (streams)
  - Multi-Core computer systems in distributed systems network

## SOAP vs REST

### Simple Object Access Protocol (SOAP)

- XML based WSDL interface on top of HTTP.
- WSDL (Web Service Description Language) describes the web service interface:
  1. **Functionality Description** of the services in standard taxonomy.
  2. **Contract of Parameter Types** and return type of function (service) calls.
  3. **Binding** information about hte transport protocol to be used (Ex: SOAP).
  4. **Address** information for locating the specified service.
- Sent as `<soap:Envelope>` with `<soap:header>` and `<soap:body>`.

### Representational State Transfer (REST)

- Web service methods are exposed as URL callable APIs.
- `https://web-server/path/params`

## XML (Extensible Markup Language)

- Meta language for definiing other languaes
  - BPEL, RDF, OWL, SOAP, WSDL, UDDI
- Similar to HTML but with no predefined tags

1. Case sensitive
2. Opening and closing tags must match
3. Single root element is required
4. xml tag is required at the beginning

```xml
<?xml version="1.0" encoding="UTF-8"?>
<note>
  <to>Drake</to>
  <from>Punit</from>
  <heading>Love</heading>
  <body>GOAT</body>
</note>
```

## WSDL (Web Service Description Language)

- `<definitions>` Root WSDL element
- `<types>` Defines the data types used in the service
- `<message>` Defines the messages that will be transmitted
- `<portType>` Defines the supported operations (functions)
- `<binding>` Defines the protocol and data format for the service
- `<service>` Defines the service endpoint location

```xml
<?xml version="1.0"?>
<definitions name="StockQuote">
  (namespaces used)
  <types> ... </types>
  <messages> … </messages>
  <portType>
    <operation> … </operation>
  </portType>
  <binding> … </binding>
  <service>
    <port> … </port>
  </service>
</definitions>
```

## Development Process

- **OOA**: `Requirement -> Problem -> Class -> Application -> Testing -> Deployment`
- **SOA**: within Class `Service Discovery -> Repository -> Hosting -> Registration`

## Multithreading

- **Program** is a static piece of code in memory.
- **Process** (task) is a program in execution. Semantically independent.
- **Thread** is a sequence of instructions within a process. Can be semantically dependent.
- OS manages processes and threads: scheduling, synchronization and resource allocation.

### Multithreading in Java

#### Thread Implementation in Java

##### Extend Thread Class

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

##### Implement Runnable Interface

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

##### ThreadPool and Executor

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
public class SimpleThreadPool {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(5);
        for (int i = 0; i < 10; i++) {
            String name = "B " + i;
            Runnable worker = new ThreadB(name);
            executor.execute(worker);
          }
        executor.shutdown();
        while (!executor.isTerminated()) {
        }
    }
}
```

##### Callable Interface

```java
import java.util.concurrent.Callable;
public class ThreadACallable implements Callable<String>{
  private String name;
  public ThreadACallable(String n) {
  name = n;
  }
  @Override
  public String call() throws Exception {
    Thread.sleep(1000);
    return name;
  }
}
```

#### Running Threads

```java
public class RunThreads {
  public static void main(String[] args) {
    ThreadA a1 = new ThreadA("Thread A");
    ThreadB b = new ThreadB("Thread B");
    Thread b1 = new Thread(b);
    a1.start();
    b1.start();
    try {
      a1.join();
    } catch (InterruptedException e) {
      e.printStackTrace();
    }
  }
}
```

#### Thread Synchronization

```java
class BufferClass {
  private int bufferValue = 0;
  private boolean writeable = true;
  public synchronized void write(int value) {
    while (!writeable) {
      try {
        wait();
      } catch (InterruptedException e) {
        e.printStackTrace();
      }
    }
    bufferValue = value;
    writeable = false;
    notify();
  }
  public synchronized int read() {
    while (writeable) {
      try {
        wait();
      } catch (InterruptedException e) {
        e.printStackTrace();
      }
    }
    writeable = true;
    notify();
    return bufferValue;
  }
}
```

### Multithreading in C#

#### Thread Implementation in C#

```c#
Thread thread1 = new Thread(MethodNameHere);
thread1.Start();
thread1.Join();
```

```c#
Thread thread2 = new Thread(new ThreadStart(MethodNameHere));
```

```c#
Thread thread3 = new Thread( () => MethodNameHere(para1, para2,…));
thread3.start();
```

#### Thread Monitor

```c#
public void runProducer() {
  for (int i = 0; i < 10; i++) {
    Monitor.Enter(myMainClass.bufferCellref);
    try {
      myMainClass.bufferCellref.setBuffer(i);
      Console.WriteLine("Procucer set buffer to " + i);
    } finally {
      Monitor.Exit(myMainClass.bufferCellref);
    }
  }
}

public void runConsumer() {
  for (int i = 0; i < 10; i++) {
    Monitor.Enter(myMainClass.bufferCellref);
    try {
      int j = myMainClass.bufferCellref.getBuffer();
      Console.WriteLine("Consumer gets " + j);
    } finally {
      Monitor.Exit(myMainClass.bufferCellref);
    }
  }
}

public class myMainClass {
  public static int items = 0;
  public static BufferClass bufferCellref = new BufferClass();
  public static void Main() {
    ProducerThread p = new ProducerThread(0);
    ConsumerThread c = new ConsumerThread(0);
    Thread producer = new Thread(new ThreadStart(p.runProducer));
    Thread consumer = new Thread(new ThreadStart(c.runConsumer));
    producer.Start();// two producers will be started
    consumer.Start(); // two consumers will be started
    Console.WriteLine("main thread completed");
    Console.ReadKey();
  }
}
```

- `Monitor.Wait(this)` is used to release the lock and wait for the signal from another thread.
- `Monitor.PulseAll(this)` is used to signal all the threads waiting on the lock.
- `Monitor.Enter()` does not have a timeout, so it can cause a deadlock.
- `Monitor.TryEnter()` gives up immediately if the lock is not available.
- `Monitor.Enter(buffer)` has a parameter of type `object` to lock.

#### ReaderWriterLock

Same functions as Monitor for preventing simulataneous access to a shared resource.
More efficient as it allows multiple readers to access the resource at the same time.
They do not allow overlapped read-write or write-write access.

- `ReaderWriterLock rwlock = new ReaderWriterLock();` from `System.Threading`.
- `rwlock.AcquireReaderLock(10);` to acquire a reader lock with 10ms timeout.
- `rwlock.ReleaseReaderLock();` to release a reader lock.
- `ReaderWriterLock` locks all objects between `AcquireReaderLock()` and `ReleaseReaderLock()`.
  - Similar to Java's `synchronized` block.

```c#
using System;
using System.Threading;
class MyApp {
  static Random rng = new Random();
  static byte[] buffer = new byte[100];
  static Thread writer;
  static ReaderWriterLock rwlock = new ReaderWriterLock();
  static void Main() {
    for (int i = 0; i < 100; i++) buffer[i] = (byte)(i+1);
    writer = new Thread(new ThreadStart(WriterFunc));
    writer.Start();
    Thread[] readers = new Thread[10];
    for (int i = 0; i < 10; i++) {
      readers[i] = new Thread(new ThreadStart(ReaderFunc));
      readers[i].Name = (i + 1).ToString();
      readers[i].Start();
    }
  }
}

static void WriterFunc() {
  DateTime start = DateTime.Now;
  while (DateTime.Now.Subtract(start).TotalSeconds < 10) {
    int j = rng.Next(0, 100);
    int k = rng.Next(0, 100);
    rwlock.AcquireWriterLock(500);
    try {
      Swap(ref buffer[j], ref buffer[k]);
    } finally {
      rwlock.ReleaseWriterLock();
    }
  }
  static void Swap(ref byte a, ref byte b) {
    byte temp = a;
    a = b;
    b = temp;
  }
}

static void ReaderFunc() {
  for (int i = 0; writer.IsAlive; i++) {
    int sum = 0;
    rwlock.AcquireReaderLock(Timeout.Infinite);
    try {
      for (int k = 0; k < 100; k++) sum += buffer[k];
    } finally {
      rwlock.ReleaseReaderLock();
    }
  }
}
```

### Deadlocks

1. **Deadlock Prevention** uses an algorithm to guarantee no deadlock will occur.
2. **Deadlock Avoidance** uses an algorithm to anticipate and prevent deadlock from occurring.
3. **Deadlock Detection and Recovery** uses an algorithm to detect deadlock and recover from it.

### Delegates and Events

- Delegates represent method references with specific signatures in C#.
- Events enable objects to notify others by binding methods to execute when an event occurs.
- Using delegates and events in combination allows for powerful event-driven programming in C#.

```c#
delegate double MyDelegate(int i);
class Program{
  public static void Main() {
    MyDelegate d1 = new MyDelegate(Pi_Plus);
    d1(10);
    MyDelegate d2 = new MyDelegate(E_Plus);
    d2(20);
    public static double Pi_Plus(int i) {
      return i + System.Math.PI;
    }
    public static double E_Plus(int i) {
      return i + System.Math.E;
    }
  }
}
```

```c#
using System;
public delegate void MyDelegate();
public interface EventInterface {
  event MyDelegate MyEvent;
  void EventEmitter();
}
public class EventClass : EventInterface {
  public event MyDelegate MyEvent;
  public void EventEmitter() {
    if (MyEvent != null) MyEvent();
  }
}
public class MainClass {
  static private void TouchSensor() {
    Console.WriteLine("Touch Sensor Activated");
  }
  static private void MotionSensor() {
    Console.WriteLine("Motion Sensor Activated");
  }
  static public void Main() {
    EventInterface i = new EventClass();
    i.MyEvent += new MyDelegate(TouchSensor);
    i.EventEmitter();
    i.MyEvent -= new MyDelegate(TouchSensor);
    i.MyEvent += new MyDelegate(MotionSensor);
    i.EventEmitter();
  }
}
```

## Thread Lifecycle

- **creation**: initialized and resources are allocated to it, but it has not yet started executing.
- **ready**: waiting to be scheduled and has all the necessary resources to start execution.
- **waiting**: waiting for a specific event or resource, such as I/O completion, and is not able to continue execution until that event occurs or resource becomes available.
- **running**: actively executing instructions on the CPU.
- **blocked**: waiting for a specific event or resource, but unlike "waiting," it cannot proceed until it is explicitly unblocked by another thread or system event.
- **sleeping**: intentionally suspended or delayed for a certain period of time using an operating system call or programming construct.
- **terminated**: finished execution and its resources are released back to the system for reuse.
