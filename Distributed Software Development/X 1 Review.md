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
