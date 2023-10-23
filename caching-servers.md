# Caching Servers

### &#x20;How do caching servers work?

Cach servers work by saving a user's request and then serving that saved request to other users when they call the same endpoint.

* The server **only** gets called if the response is not found in the caching server.

**A cache key:** is an index entry that uniquely identifies an object in a cache.

The caching server determines if two requests are identical using the **cache key.**

#### Example

<figure><img src=".gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* “user 1” requests the “example.com/kop?somthing=ok” -> response not found in the caching server -> forwarded to the web server answering the response.
* users 2 and 3 make the same request -> response found in the caching server -> web server not contacted -> old response shown instead.



