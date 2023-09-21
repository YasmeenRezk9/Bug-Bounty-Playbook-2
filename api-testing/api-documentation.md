# API Documentation

Attackers can use the API docs to find design flaws, and hidden endpoints, and get a better understanding of the application.

## <mark style="color:yellow;">Swagger API</mark>

A popular API documentation language for describing RESTful APIs expressed using JSON.&#x20;

* gives the name, path, and arguments of every possible api call.&#x20;

#### **Swagger endpoints:**

→ /api&#x20;

→ /swagger/index.html&#x20;

→ /swagger/v1/swagger.json&#x20;

→ /swagger-ui.html&#x20;

→ /swagger-resources

**Interesting findings:**

→ hidden password resets that are easily bypassable

→ hidden admin functionality&#x20;

→ SQL injection

#### **XSS**

When getting across some swagger documentation, check for these two XSS vulnerabilities:

* &#x20;[https://github.com/swagger-api/swagger-ui/issues/1262](https://github.com/swagger-api/swagger-ui/issues/1262)
* [https://github.com/swagger-api/swagger-ui/issues/3847](https://github.com/swagger-api/swagger-ui/issues/3847)

## <mark style="color:yellow;">Postman</mark>

A tool that can be used to read and write API documentation

* used to import API documentation from multiple sources.
* &#x20;[https://www.postman.com/downloads/](https://www.postman.com/downloads/)

Once you import the API docs to Postman, review each API endpoint and test it for vulnerabilities.

## <mark style="color:yellow;">Web Service Description Language (WSDL)</mark>

A file is used to describe the endpoints of a SOAP API.

* Look for an XML file that contains a “wsdl” tag:\
  → example.com/?wsdl\
  → example.com/file.wsdl
* Import this file into the “[soupUI](https://www.soapui.org/downloads/soapui/)” tool

## <mark style="color:yellow;">Web Application Description Language (WADL)</mark>&#x20;

A machine-readable XML description of HTTP-based web services used for REST APIs.

* Look for an XML document ending with “wadl”&#x20;

&#x20;      → example.com/file.wadl

* Import it using Postman -> review each API endpoint and test it for vulnerabilities.
