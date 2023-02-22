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
