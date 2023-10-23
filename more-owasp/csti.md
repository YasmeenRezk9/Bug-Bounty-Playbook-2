---
description: Client-Side Template Injection
---

# CSTI

### <mark style="color:yellow;">Angular Basics</mark>

#### Description

Angular is a client-side template framework and you can embed user input into these templates.

#### Template

An HTML snippet that tells Angular how to render the component in an Angular application.

* allows to dynamically generate HTML code based on the arguments passed to it.
* Ex: \<h1>Welcome \{{Username\}}!\</h1>

#### Expressions

Expressions are Javascript-like code snippets that can contain literals, operators, and variables.

* Angular expressions are evaluated against the Scope object.
* Ex: “\{{Username\}}”

#### Scope Object

The scope is just an object and you can define variables and functions in it.

By default, the scope object contains another object called “constructor” which contains a function also called "constructor":

* used to dynamically generate and execute code.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### <mark style="color:yellow;">CSTI</mark>

#### Description

Arises when applications using a client-side template framework dynamically embed user input in web pages.

#### Impact

Used to trigger XSS payloads.

#### Indicators

Try to use the expression “\{{1+1\}}” which gets evaluated to “2” -> app vulnerable to CSTI.

#### Prevention

Using sandbox.

### <mark style="color:yellow;">CSTI (XSS)</mark>

💡NOTE: search for sandbox bypass for the Angular version to get the XSS payload to execute.

Inject an Angular expression payload:

* \{{constructor.constructor('alert(1)')()\}}

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

The page causes the application to dynamically generate and execute our payload!
