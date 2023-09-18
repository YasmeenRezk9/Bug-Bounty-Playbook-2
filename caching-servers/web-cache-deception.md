# Web Cache Deception

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

Web cache deception works by sending the victim a URL which will cache the response for everyone to see.

* Only possible due to path confusion, sometimes the caching server is configured to cache any page ending with a specific extension (css, JPG, PNG, ect):

&#x20;     \-> cache all static pages no matter what the response headers say.

EX: “example.com/nonexistent.css”, The caching server would cache this response **regardless** of what the response headers say.



