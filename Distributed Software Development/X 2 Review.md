<!-- # CSE 445 Midterm 2 Cheatsheet -->

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
