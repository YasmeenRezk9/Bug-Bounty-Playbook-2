---
description: Content Security Policy Bypass
---

# CSP Bypass

### <mark style="color:yellow;">Content Security Policy (CSP)</mark>

A special HTTP header is used to mitigate certain types of attacks such as cross-site scripting (XSS).

* **If set up improperly,** it introduces misconfigurations and allows attackers to completely bypass the CSP.

**CSP header value**&#x20;

* made up of directives separated with a semicolon “;”

#### Some CSP Directives <a href="#detailed-csp-directives" id="detailed-csp-directives"></a>

<table><thead><tr><th width="224">Value</th><th>Description</th></tr></thead><tbody><tr><td>Script-src</td><td>describes where we can load javascript files from.</td></tr><tr><td>Default-src</td><td>acts as a catchall for everything else.</td></tr><tr><td>Media-src</td><td>describes where we can load audio and video files from.</td></tr><tr><td>frame-ancestors</td><td>describes which sites can load this site in an iframe.</td></tr><tr><td>Style-src</td><td>describes where we can load stylesheets from.</td></tr></tbody></table>

#### Special Directive Sources <a href="#special-directive-sources" id="special-directive-sources"></a>

<table><thead><tr><th width="226">Value</th><th>Description</th></tr></thead><tbody><tr><td>'none'</td><td>No URLs match.</td></tr><tr><td>'self'</td><td>Refers to the origin site with the same scheme and port number.</td></tr><tr><td>'unsafe-inline'</td><td><p>Allows the usage of inline scripts or styles.         </p><p>EX: (onclick, tags, javascript:,)</p></td></tr><tr><td>'unsafe-eval'</td><td>Allows the usage of eval in scripts.</td></tr><tr><td>sth.ex.com</td><td>Only load resources from specified domain</td></tr></tbody></table>

#### Structure of a CSP header Example

```html
Content-Security-Policy: default-src 'none'; script-src 'self'; connect-src 'self'; img-src 'self'; style-src 'self'; frame-ancestors 'self'; form-action 'self';
```

### <mark style="color:yellow;">Ways to bypass CSP</mark>

