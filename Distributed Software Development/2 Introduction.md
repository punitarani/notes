# Introduction to Distributed Software Development

## XML

- XML stands for Extensible Markup Language that is used to store and transport data.
- It is used for defining data types and for exchanging data between applications.
- It is similar to HTML but has no predefined tags and is more flexible.
- Some common languages and protocols that use XML are:
  - BPEL (Business Process Execution Language)
  - RDF (Resource Description Framework)
  - OWL (Ontology Web Language)
  - SOAP (Simple Object Access Protocol)
  - WSDL (Web Services Description Language)
  - UDDI (Universal Description, Discovery and Integration)
- XML definition rules
  - Case sensitive
  - Opening and closing tags must match
  - Documents must have a root element
  - Documents are recommended to have an XML declaration

## WSDL

- WSDL stands for Web Services Description Language.
- It is an XML-based language that describes the functionality offered by a web service.
- The 4 critical aspects of a WSDL document are:
  1. **Functionality Description** of the services in standard taxonomy.
  2. **Contract of Parameter Types** and return type of function (service) calls.
  3. **Binding** information about hte transport protocol to be used (Ex: SOAP).
  4. **Address** information for locating the specified service.
- The last 3 aspects can be automatically generated.
- Web services described in WSDL can be searched and matched with the requirement.
- Web services described in WSDL provides the remote call detail.

### Main Components of WSDL

- **definitions**: Root WSDL element
- **types**: What data types will be transmitted?
- **message** What messages will be transmitted?
- **portType**: What operations(functions) will be supported?
- **binding**: How will the messages be transmitted? What SOAP-specific details are there?
- **service**: Where is the service located?

## SOAP

- SOAP stands for Simple Object Access Protocol.
- It is used to transport messages between web services and clients.
- A SOAP message is an XML document that contains:
  - **Envelope**: The root element of a SOAP message.
  - **Header**: Contains information about the message.
  - **Body**: Contains the actual message.
- SOAP messages are sent over HTTP.
