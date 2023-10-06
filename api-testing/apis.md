---
description: There are several types of APIs, and they are each slightly different.
---

# APIs

💡If you come across an API endpoint the first step is to figure out what type of API it is.

## <mark style="color:yellow;">Rest API</mark>

#### Signs

* Request and response data are JSON strings.
* The application is issuing a PUT request.
* The HTTP response contains a MIME type of JSON.

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>REST API</p></figcaption></figure>

#### Cons

* ⚠️ Rest API requires the client to send multiple requests to different endpoints on the API to query data from the backend database.

## <mark style="color:yellow;">Remote Procedure Call (RPC)</mark>

Fairly basic, each HTTP request maps to a particular function.

💡XMLRPC uses XML while JSONRPC uses JSON for its encoding type.

* If this endpoint was a JSONRPC API the data would be contained in a JSON string instead of an XML doc.

#### Signs

* The file name is “xmlrpc.php”.
* the request body contains two tags called “methodCall” and “methodName”.
* The request only uses two, GET and POST methods.

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## <mark style="color:yellow;">Simple Object Access Protocol (SOAP)</mark>

Like an advanced version of XMLRPC:

* Both use XML for encoding and HTTP to transfer messages.

#### Signs

The message is first wrapped in a “[soapenv:Envelope](soapenv:Envelope)” tag which contains the header and body tags.

* header part is optional and contains information about the message itself like values related to authentication, and complex types.
* body is the part of the XML document which actually contains our message:

```xml
<!-- SOAP body we are calling a method named “ GetCitiesByCountry ” and an argument called “CountryName ” with a string 
value of “gero et”  -->
<soapenv:Body> 
<web:GetCitiesByCountry> 
<!--type: string--> 
<web:CountryName>gero et</web:CountryName> 
</web:GetCitiesByCountry> 
<soapenv:Body>
```

## <mark style="color:yellow;">GraphQL API</mark>

A data query language developed by Facebook acts as an alternative to REST API.

* a single request can be used to gather all the necessary information from the backend.
* missing authentication by default graphQL endpoints can be vulnerable to other bugs such as IDOR.

#### Directory brute force paths to check for graphQL:

* /graphql
* /graphiql
* /graphql.php
* /graphql/console

**Once you find an open graphQL instance** you need to know what queries it supports using [the introspection system](https://graphql.org/learn/introspection/).

💡Types that start with a “\_\_” can be ignored as those are part of the introspection system.

Once an interesting type is found you can query its field values, an example:

* Show all the available queries on the endpoint:

&#x20;     \--> example.com/graphql?query={\_\_schema{types{name,fields{name\}}\}}

Once an interesting type is found, query its field values:

&#x20;     \--> example.com/graphql?query={TYPE\_1{FIELD\_1,FIELD\_2 \}}

Once the query is submitted it will pull the relevant information and return the results.

**EX:**

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>
