---
description: Relative Path Overwrite
---

# RPO

### <mark style="color:yellow;">Basic Concepts</mark>

#### Ways an application can load the CSS file

```html
<!-- using the full path to the CSS file  -->
<link   href="http://example.com/style.css"   rel="stylesheet"   type="text/css"/>

<!-- using root dir of the CSS file -->
<link   href="/style.css"   rel="stylesheet"   type="text/css"/>

<!--  using a relative path  -->
<link   href="style.css"   rel="stylesheet"   type="text/css"/>
```

#### Quirks mode

Handles the poorly coded websites.

If quirks mode is enabled the browser will ignore the “content-type” of a file when processing it.

* EX: parsing the HTML file as if it's a CSS file.

### <mark style="color:yellow;">Exploitation RPO</mark>

#### Prerequisites

Meet all the following requirements to exploit RPO.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

#### Vulnerable Code Snippet

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

**Meeting requirements:**

{% tabs %}
{% tab title="¯\_(ツ)_/¯" %}
Swap Tabs
{% endtab %}

{% tab title="Path reflection" %}
The “okay/” path is displayed on the page.

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Quirks mode" %}
The “document type” tag is missing from the HTML source.


{% endtab %}

{% tab title="Wildcard path" %}
The “/home/okay/” resolves to the same page as “/home”.

<figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Relative Path" %}
When changing the URL to “/home/okay/”, the “Link” tag tries to import its stylesheet from “/home/okay.style.css”

<figure><img src="../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

#### After meeting all requirements, try to inject CSS code to turn the font red so we now know the target is vulnerable:

EX: <mark style="color:red;">%0A{}\*{color:red;}///</mark>

<figure><img src="../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

### <mark style="color:yellow;">Impact</mark>

Low severity finding.

* XSS, web defacement, and extracting sensitive data.
