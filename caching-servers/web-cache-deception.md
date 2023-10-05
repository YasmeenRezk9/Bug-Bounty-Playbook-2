# Web Cache Deception

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

Web cache deception works by sending the victim a URL which will cache the response for everyone to see.

* Only possible due to path confusion, sometimes the caching server is configured to cache any page ending with a specific extension (css, JPG, PNG, ect):

&#x20;     \-> Cache all static pages no matter what the response headers say.

**EX:** “example.com/nonexistent.css”, The caching server would cache this response **regardless** of what the response headers say.

## <mark style="color:yellow;">Exploitation</mark>

1. Find a page exposing sensitive information.&#x20;
2. Check for path confusion.
3. See if the response is cached.
4. See if the cached response is public.

#### To test for web cache deception, try one of the several path-confusing payloads

* example.com/nonexistent.css
* example.com/%0Anonexistent.css
* example.com/%3Bnonexistent.css
* example.com/%23nonexistent.css
* example.com/%3fname=valnonexistent.css

## <mark style="color:yellow;">Path confusion</mark>

All about the web server interpreting a request one way while the caching server interprets it a different way.

* occurs when an application loads the same resources no matter what the path is.

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

* As we can see above, any path after “/” will essentially be passed to the same function giving the same results.
* EX: both the “example.com” and “example.com/something'' URLs would be sent to the same catch\_all function.

### Techniques cause path confusion

#### Path parameter&#x20;

When additional paths are added to the request passed to the same backend function.

* Server sees: example.com/account.php/
* The caching server sees: example.com/account.php/nonexistent.css

#### Encoded newline (\n)&#x20;

Some proxies and web servers stop reading after the new line character but the caching server does not.

* The server sees: example.com/account.php
* The caching server sees: example.com/account.php%0Anonexistent.css

#### Encoded semicolon (;)&#x20;

Some web servers treat semicolons(;) as parameters, and the caching server may treat the request as a separate resource.

* The server sees: “example.com/account.php” with the parameter “nonexistent.css”
* The caching server sees: “example.com/account.php%3Bnonexistent.css”

#### Encoded pound (#)&#x20;

Web servers often process the pound character as an HTML fragment identifier and stop parsing the URL after that, the caching server may not recognize this.

* The server sees: “example.com/account.php
* Caching server sees: “example.com/account.php%23nonexistent.css”

#### Encoded question mark (?)&#x20;

Web servers treat question marks(?) as parameters but the caching server treats the response differently.

* The server sees: “example.com/account.php”
* The Caching server sees: “example.com/account.php%3fname=valnonexistent.css”

