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

<table><thead><tr><th width="162">Value</th><th>Description</th></tr></thead><tbody><tr><td>Script-src</td><td>describes where we can load javascript files from.</td></tr><tr><td>Default-src</td><td>acts as a catchall for everything else.</td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr></tbody></table>

#### Special Directive Sources <a href="#special-directive-sources" id="special-directive-sources"></a>

