# Web Cache Poisoning

Web cache poisoning is a technique attackers use to force caching servers to serve malicious requests.&#x20;

* By web cache poisoning, self XSS can be turned into stored XSS.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

### Steps

* Find an unkeyed value -> using the param miner plugin
* Try to exploit the unkeyed value in some way -> (self xss)
* Try to make the server cache the malicious HTTP response
* See if our exploit worked -> Looking at the HTTP response headers

#### Indicators

* The “X-cache” header is set to “miss” and the “Age” header is set to 0.
* Path.
* Adding a random GET parameter to the request should cause the response to be cached.

#### Response Headers

The “X-Cache” response header:

* If set to “hit”, the page was served from the cache.
* If set to “miss”, the page isn't served from the cache.

The “Age” response header:

* contains the seconds the page has been cached for.

