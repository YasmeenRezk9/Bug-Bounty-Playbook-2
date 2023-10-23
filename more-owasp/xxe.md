---
description: XML External Entity
---

# XXE

### <mark style="color:yellow;">Extensible Markup Language (XML)</mark>

A language designed to store and transport data similar to JSON.

#### basic structure of XML

<figure><img src="../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

**Document Type Definition (DTD):** defines the structure and the legal elements and attributes of an XML document.

**Entity:** acts as a variable.

**External Entity:** loads its data from an external source such as url or a file on disk.

* 💡Note: to read the data the entity must be returned in the response.
* EX: \<!DOCTYPE foo\[ \<!ENTITY ext SYSTEM "file:///path/to/file" > ]>

### <mark style="color:yellow;">XML External Entity(XXE) Attack</mark>

#### Description

Appears when an application parses XML.

#### Impact

Read arbitrary files which can lead to fully compromising a machine.

#### Indicator

Whenever you see XML you should test for XXE.

* \<?xml version="1.0" encoding="UTF-8"?>

#### Exploitation

💡If the server does not block external entities the response will be reflected

To test for XXE -> put in a malicious external entity and replace each node value with it.

<mark style="color:green;">**Scenario:**</mark> Retrieving the contents of the /etc/passwd file

<figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption><p>XML Normal code</p></figcaption></figure>

TO DO:

1. Create an external entity to grab the data in the /etc/passwd file
2. Store it in the entity xxe
3. Place the variable in the node

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

