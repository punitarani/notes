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

## Thread Lifecycle

- **creation**: initialized and resources are allocated to it, but it has not yet started executing.
- **ready**: waiting to be scheduled and has all the necessary resources to start execution.
- **waiting**: waiting for a specific event or resource, such as I/O completion, and is not able to continue execution until that event occurs or resource becomes available.
- **running**: actively executing instructions on the CPU.
- **blocked**: waiting for a specific event or resource, but unlike "waiting," it cannot proceed until it is explicitly unblocked by another thread or system event.
- **sleeping**: intentionally suspended or delayed for a certain period of time using an operating system call or programming construct.
- **terminated**: finished execution and its resources are released back to the system for reuse.
