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

```csharp
Thread thread1 = new Thread(MethodNameHere);
thread1.Start();
thread1.Join();
```

```csharp
Thread thread2 = new Thread(new ThreadStart(MethodNameHere));
```

```csharp
Thread thread3 = new Thread( () => MethodNameHere(para1, para2,…));
thread3.start();
```

#### Thread Monitor

```csharp
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

```csharp
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

```csharp
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

```csharp
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

```csharp
[ServiceContract]
public interface IService1{
    [OperationContract]
    string welcome(string yourName);
}
ServiceReference1.Service1Client myClient = new ServiceReference1.Service1Client();
MessageBox.Show(myClient.welcome("Janaka"));
```

```csharp
[ServiceContract]
public interface IService1 {
    [OperationContract]
    [WebGet ( UriTemplate= "/Welcome/{yourName}")]
    string welcome(string yourName);
}
```

## JSON

- Object is typically the root element. `Object { string: value of any type }`

```csharp
Using newtonSoft :
using Newtonsoft.Json;
static void processJsonNewtonSoft(String data) {
    results p = JsonConvert.DeserializeObject<results>(data);
    Console.WriteLine(p.lower_case_letters);
}
```

## XML

- **Elements** define data that are integral to the document. Elements form a rooted tree.
- **Attributes** provide additional information about an element. Stored linearly in the element.

```xml
<?xml version="1.0" encoding="UTF-8">
<instructor course=“Service-Oriented Computing" >
 <name>
  <first>John</first>
  <last>Doe</last>
 </name>
</instructor>
```

1. Unique root element
2. All elements must be enclosed between an opening and closing tag
3. Nested tags are allowed but cannot overlap
4. Element tag name and content must meet the same rules as variable names
5. Tag names must be defined/declared in the Document Type Definition

- Attributes must always be enclosed in double (or single) quotes
- Attributes are contained within the opening tag of an element
- Duplicate attributes are not allowed within an element

### XML Related Technologies

- HTML, XHTML, XAML: Markup languages for presentation
- XPath, XQL: Parser and query languages
- XSL, XSSLT: Stylesheet languages
- DOM, SAX: APIs for parsing and querying XML documents
- DTD, XML Schema: Document type definitions and schemas

### XML Parsers

- **DOM**: Document Object Model.
  - Parses the entire document into a tree structure in memory.
  - MSXML: Microsoft XML parser supports DOM and SAX.
- **SAX**: Simple API for XML.
  - Parses the document in a streaming fashion.
- **XPath**: XML Path Language.
  - Query language for XML documents.

### XML classes in .NET

- `System.XML` namespace contains classes for reading, writing, and manipulating XML documents.
- `XmlDocument` class represents an XML document. Similar but simpler than `MSXML` DOM.
  - `.SelectSingleNode()` : `XmlNode` is the base class for all XML nodes in the DOM.
    - `.ChildNodes()` : `XmlNodeList` is a collection of `XmlNode` objects.
    - `.Attributes()` : `XmlNamedNodeMap` is a collection of `XmlAttribute` objects.
  - `XmlDocumentType`, `XmlElement`, `XmlLinkedNode` are classes derived from `XmlNode`.
  - `ParentNode`, `LastChild`, `NextSibling`, `PreviousSibling`, `Prefix`, `PreserveWhitespace`, `Schemas` and `Value` are methods of `XmlNode`.
- `XmlTextReader` and `XmlValidatingReader` classes are used to stream XML documents (SAX).
- `XmlTextWriter` class is used to write XML documents.

```csharp
void OutputNode (XmlNode node) {
    If (node == null) exit;
    Console.WriteLine (“Type={0}\tName={1}\tValue={2}”,
    node.NodeType, node.Name, node.Value);
    if (node.HasChildNodes) {
        XmlNodeList children = node.ChildNodes;
        foreach (XmlNode child in children)
            OutputNode (child);
    }
}
```

```text
preorder(p)
    if p != null then
        visit(p)
        for each child c of p do
            preorderTraverse(c)
```

```text
inorder(p)
    if p != null then
        inorderTraverse(p.left)
        visit(p)
        inorderTraverse(p.right)
```

```text
postorder(p)
    if p != null then
        for each child c of p do
            postorderTraverse(c)
        visit(p)
```

### DTD: Document Type Definition

- Provides organization and rules (grammar and structure) for XML documents.
- Can be a separate file (global DTD) or embedded in the XML document.
- Not XML based and requires a separate parser. Restricted to string type of data.

1. **Element**: `<!ELEMENT element-name (#PCDATA)>`
2. **Attribute**: `<!ATTLIST element-name attribute-name attribute-type attribute-value>`
3. **PCDATA**: `(#PCDATA)` parsed character data to be processed by the parser.
4. **CDATA**: `(#CDATA)` character data to be included in the document as is.

```xml
<?xml version="1.0" encoding="utf-8"?>
<!ELEMENT book (title, author, isbn)>
<!ELEMENT title (#PCDATA)>
<!ELEMENT author (#PCDATA)>
<!ELEMENT isbn (#PCDATA)>

<note>
  <body>Please remember to call me &lt;tomorrow&gt;.</body>
</note>

<message>
  <content><![CDATA[This is a message that contains <markup> characters.]]></content>
</message>
```

### XML Schema

- Provides a formal definition of the structure of an XML document. More powerful than DTD.
- Parse 44 (19 + 25) data types: schema, element, complexType, sequence, boolean, integer, string, etc.

- Complex type: A complex type is a type that is composed of other types.
  - **sequence**: All members must appear in the given order
  - **choice**: Only one of the list members is allowed
  - **all**: All members must appear (unless minOccurs=“0" ), but can be in any order

```xml
<?xml version="1.0" encoding="utf-8"?>
<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="book">
    <xs:complexType name="Person">
    <xs:sequence>
        <xs:element name="Name" type="xs:string"/>
        <xs:element name="Address" type="xs:string" minOccurs="0"/>
        <xs:choice>
        <xs:element name="Email" type="xs:string"/>
        <xs:element name="Phone" type="xs:string"/>
        </xs:choice>
        <xs:all>
        <xs:element name="Age" type="xs:integer" minOccurs="0"/>
        <xs:element name="Gender" type="xs:string" minOccurs="0"/>
        </xs:all>
    </xs:sequence>
    </xs:complexType>
  </xs:element>
</xs:schema>
```

### XPath

- `/` (Root): Selects the root node of the document. `/rootElement`
- `//` (Descendants): Selects all matching nodes, regardless of their location in the document. `//element`
- `.` (Current node): Represents the current node in the document. `.//element`
- `..` (Parent): Selects the parent of the current node. `//element/..`
- `@` (Attribute): Selects attributes of an element. `//element/@attribute`
- `*` (Wildcard): Matches any element node. `/rootElement/*`
- `[]` (Predicate): Filters nodes based on a specific condition. `//element[@attribute="value"]`
- `|` (Union): Combines the results of two or more XPath expressions. `//element1 | //element2`
- `and` (Logical AND): Returns true if both conditions in the expression are true. `//element[@attribute1="value1" and @attribute2="value2"]`
- `or` (Logical OR): Returns true if at least one condition in the expression is true. `//element[@attribute="value1" or @attribute="value2"]`
- `not()` (Logical NOT): Returns true if the argument is false, and false otherwise. `//element[not(@attribute="value")]`
- `text()` (Text content): Selects the text content of an element. `//element/text()`
- `contains()` (Contains substring): Returns true if the first argument string contains the second argument string. `//element[contains(@attribute, "substring")]`
- `starts-with()` (Starts with substring): Returns true if the first argument string starts with the second argument string. `//element[starts-with(@attribute, "substring")]`

- In XPath, a document is represented as a tree of nodes, which can be classified into three types:
  - Element nodes, Attribute nodes, Text nodes
- An XPath expression is a path from one part of the document to another part of a document.
- An expression consists of a sequence of nodes, functions, function return values, and variables.
- The value of an expression can be one of the four XPath data types:

  - Node-set, Boolean, Floating-point number, String of Unicode characters.

- `XPathDocument` creates an XPath document from an XML documents; which is based on DOM model: The entire XML file is loaded into memory for queries.
- `XPathNavigator` provides a mechanism for performing XPath queries;
- `XPathNodeIterator` represents node sets generated by XPath queries and lets you iterate over them

```csharp
using System;
using System.Xml;
using System.Xml.XPath;

class MyApp {
    static void Main() {
        // Load the XML document
        XPathDocument doc = new XPathDocument("data.xml");
        XPathNavigator nav = doc.CreateNavigator();

        // Select the desired nodes using XPath
        XPathNodeIterator iterator = nav.Select("/Courses/Course");

        // Iterate through the selected nodes
        while (iterator.MoveNext()) {
            // Extract and display the "Name" element value
            XPathNodeIterator nameIterator = iterator.Current.Select("Name");
            if (nameIterator.MoveNext()) {
                string name = nameIterator.Current.Value;
                Console.WriteLine("Course Name: {0}", name);
            }

            // Extract and display the "Duration" attribute value
            XPathNodeIterator durationIterator = iterator.Current.Select("@Duration");
            if (durationIterator.MoveNext()) {
                string duration = durationIterator.Current.Value;
                Console.WriteLine("Duration: {0}", duration);
            }

            Console.WriteLine();
        }
    }
}
```

### `XmlTextReader`

- XmlDocument: Navigate and manipulate in-memory XML document tree
- XmlTextReader: Fast, forward-only, read-only interface for reading XML documents
- More memory-efficient than XmlDocument
- Suitable for searching specific elements, attributes, or content items
- Built-in recursion for easier searching

```csharp
XmlTextReader reader = null;
try {
 reader = new XmlTextReader (“Courses.xml”);
 reader.WhitespaceHandling = WhitespaceHandling.None;
 while (reader.Read ()) {
  Console.WriteLine (“Type={0}\tName={1}\tValue={2}”,
  reader.NodeType, reader.Name, reader.Value);
 }
}
finally {
 if (reader != null)
  reader.Close();
}
```

## XML Example

```csharp
XmlDocument doc = new XmlDocument();
doc.Load("addressbook.xml");

XmlNodeList stateList = doc.GetElementsByTagName("state");
XmlNodeList zipcodeList = doc.GetElementsByTagName("zipcode");

for (int i = 0; i < stateList.Count; i++)
{
    Console.WriteLine(stateList[i].InnerText);
    Console.WriteLine(zipcodeList[i].InnerText);
    Console.WriteLine("=======");
}
```

```csharp
static void OutputNode(XmlNode node) {
    if (node == null)
        System.Environment.Exit(1);

    if (node.HasChildNodes)
    {
        XmlNodeList children = node.ChildNodes;
        foreach (XmlNode child in children)
            OutputNode(child);
    }

    Console.WriteLine("Type={0}\tName={1}", node.NodeType, node.Name);
} // This is post-order traversal
```

## JSON Example

```csharp
A pCode = JsonConvert.DeserializeObject<A>(responsereader);
Console.WriteLine(A.postalCodes[0].postalCode);
```

```csharp
public class PostalCode {
    public string adminCode2;
    public string adminCode1;
    public string adminName2;
    public double lng;
    public string countryCode;
    public string postalCode;
    public string adminName1;
    public string placeName;
    public double lat;
}

public class JsonResponse {
    public List<PostalCode> postalCodes;
    public string status;
    public int code;
}

class Program {
    static void Main(string[] args) {
        string filePath = "path/to/your/file.json";
        string responsereader = File.ReadAllText(filePath);

        JsonResponse response = JsonConvert.DeserializeObject<JsonResponse>(responsereader);
        Console.WriteLine(response.postalCodes[0].adminName1);
        Console.WriteLine(response.code);
    }
}
```

## Web Application

### ASP.NET

- `ASPX` (Active Server Pages Extended) server-side scripting language that lets you create dynamic web pages.
- `ASCX` (Active Server Controls Extended) server-side user control that lets you create reusable UI components.
- `ASMX` (Active Server Methods Extended) or `SVC` (Service) file that contains web service code.
- `DLL` (Dynamic Link Library) file that contains compiled code of custom classes and controls.
- `Global.asax` file that contains application-level event handlers and global application elements.
- `Web.config` configuration file that contains settings for the web application.

- `Bin/` contains compiled code and `DLL` files.
- `App_Code/` contains source code files.
- `App_Data/` contains data (text, XML and database) files.
- `App_WebReferences/` contains store references to web services.

#### Controls

- **HTML controls** are standard HTML elements rendered on client but can `RunAt="Server"`.
- **Web controls** are server-side controls that are rendered as HTML elements on the client.
  - **Simple controls**, **Button controls**, **List controls**, **Calendar controls**, and **Validation controls**.
  - **Data-bound controls** used to bind data to a data source (e.g. database)

#### Class Library

```csharp
using someLibrary;
namespace myLibrary
    public class MyClass
        public static void method()
            SomeClass.someMethod();
```

#### State Management

- `ViewState["name"]` is a hidden field that stores the state of the page and its controls.
- `Cookies` are small key-value pairs stored on the browser or the client machine.
- `Session` is a server-side object that stores information about a user across multiple requests.

```csharp
using System.Web;
using System.Web.UI.Page;
public partial class _Default : Page
    protected void Page_Load(object sender, EventArgs e)
        if (!IsPostBack)
            ViewState["name"] = "value";
        else
            HttpCookie cookie = new HttpCookie("cookieID");
            cookie["name"] = "value";
            cookie.Expires = DateTime.Now.AddDays(1);
            Response.Cookies.Add(cookie);
        HttpCookie cookie = Request.Cookies["cookieID"];
        string name = cookie["name"];
```

#### Caching

- **Temporal locality**: data used recently is likely to be used again soon.
- **Spatial locality**: data near recently used data is likely to be used soon.

1. **Output Caching**: The entire xhtml page from aspx is cached.
   - `<%@ OutputCache Duration="10" VaryByParam="None" %>`
2. **Fragment Caching**: Fragments of a page specified through user controls to cache partial data
3. **Data Caching**: Individual data objects are cached.
   - `Cache.Insert("MyDataObject", myDataObject, null, DateTime.Now.AddMinutes(5), TimeSpan.Zero);`
4. **Multi-layer Caching**: All of the above + API/Service caching.

##### `System.Web.Caching.Cache`

- `Cache["key"] = value;` to add or update an item in the cache.
- **Automated Expiration** by setting `AbsoluteExpiration` or `SlidingExpiration`.
- **Define Dependencies** by setting `CacheDependency` to invalidate cache when dependency changes.
- **Automated Callback** by setting `CacheItemRemovedCallback` to execute when item is removed.
- **Manage threads** automatically by setting `CacheItemPriority` to manage memory usage.

- `Cache` class cannot be inherited. Instance is available to all pages of the session.
  - `Add()` adds item to existing cache such as dependencies, expiration, priority or callback.
  - `Remove()` removes item from the application's Cache object.
  - `Get()` retrieves item from the application's Cache object.
  - `GetType()` returns the Type of the current instance.
  - `ToString()` returns a string that represents the current object.
  - `Insert(string key, Object item, CacheDependency dependencies, DateTime absoluteExpiration, TimeSpan slidingExpiration, CacheItemPriority priority, CacheItemRemovedCallback onRemoveCallback)`
- `CacheDependency` can be used with file/db, cache key, array of either or another dependency.

```csharp
protected void btnAddItem_Click(Object sender, EventArgs e)
    string item = "item";
    Cache.Insert("itemKey", item, null, DateTime.Now.AddMinutes(5), TimeSpan.Zero, CacheItem.Priority.Normal, onRemoveCallback);
private void onRemoveCallback(string key, object value, CacheItemRemovedReason reason) {}
```

```csharp
List<Book> objCache = (List<Book>)System.Web.HttpRuntime.Cache.Get("BooksKey");
bool itemRemoved = false;
CacheItemRemovedCallback onRemove = new CacheItemRemovedCallback(this.RemovedCallback);
if (objCache == null)  {
    DBContextDataContextDataContext myDB = new DBContextDataContextDataContext();
    IQueryable<Book> q = from b in myDB.Books select b;
    ListBox1.Items.Clear();
    foreach (Book child in q)
        ListBox1.Items.Add(child.Title + " " + child.Isbn + " " + "$" + child.Price);
    objCache = q.ToList<Book>();
    SqlCacheDependency dependency = new SqlCacheDependency(myDB.GetCommand(q) as SqlCommand);
    HttpContext.Current.Cache.Add("BooksKey", objCache, dependency, DateTime.MaxValue, TimeSpan.Zero, CacheItemPriority.Default, new CacheItemRemovedCallback(onRemove));
}
```

#### Security

```csharp
<configuration>
    <system.web>
        <authentication mode="Forms">
            <forms name="LoginForm" loginUrl="Login.aspx" timeout="30">
                <credentials passwordFormat="Clear">
                    <user name="Alice" password="abc" />
                    <user name="Bob" password="123" />
                </credentials>
            </forms>
            <deny users="?" />
        </authentication>
    </system.web>
</configuration>
```

```csharp
<script language="C#" runat="server">
    void LoginFunc(Object sender, EventArgs e)
        if (FormsAuthentication.Authenticate(txtUserName.Text, txtPassword.Text))
            FormsAuthentication.RedirectFromLogin(UserName.Text, false);
        else
            Output.Text = "Invalid login";
</script>
```
