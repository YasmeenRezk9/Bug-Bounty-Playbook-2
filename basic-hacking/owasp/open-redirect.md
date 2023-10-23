# Open Redirect

### Source Code snippet

* User-supplied input is being passed to a redirect function.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

### Goal

Forcing the application to redirect to an attacker-controlled site.

EX: redirecting to Google, if it does then the application is <mark style="color:red;">vulnerable</mark>.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Open Redirect</p></figcaption></figure>

### &#x20;Impact

* Considered a low-impact vulnerability.
* Can be chained with other bugs such as SSRF, OATH bypass, and other things giving you greater impact.

