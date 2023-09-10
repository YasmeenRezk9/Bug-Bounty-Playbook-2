---
description: Acts as a proxy and allows you to inspect, modify, replay to web requests.
---

# Burp Suite

## <mark style="color:yellow;">Proxy</mark>

#### HTTP History tab

Things to Notice:

* when a POST method is being used, think of Stored XSS, Cross-site request forgery
* When seeing a URL with an email, username, or ID in it, think IDOR.
* when seeing a JSON MIME type, think back-end API.

## <mark style="color:yellow;">Target</mark>

#### Site map tab

* allows one to view requests from a specific target.
* useful when hitting an undocumented API endpoint.
* clicking on a folder in the sitemap will only show requests from that path.

## <mark style="color:yellow;">Intruder</mark>

Go to the intruder tab in case want to fuzz or brute force with Burp.

💡Note: Professionals use “Turber Intruder” which hits a whole lot harder and a whole lot faster.

#### Basic usage

* Click the “Clear” button to reset everything
* Select the value we are trying to modify and press the “Add” button
* Selected the attack type
* Click on the “Payloads” tab
* Select the payload type and the payload list
* Press “Start attack”
* Inspect the HTTP responses to determine if there is anything suspicious.

## <mark style="color:yellow;">Repeater</mark>

Once the request is sent to the Repeater tab:

* We can modify the request to test for vulnerabilities and security misconfigurations.
* Once the request is modified we can hit the Send button to send the request.
* The response will be shown in the Response window.

