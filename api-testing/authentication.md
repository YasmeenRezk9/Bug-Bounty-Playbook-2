---
description: >-
  Compromising the authentication process will lead to account takeover (ATO)
  vulnerabilities and depending on the accounts you takeover it could also lead
  to privilege escalation.
---

# Authentication

## <mark style="color:yellow;">HTTP Basic Auth</mark>

Each time you send a request your clear text username and password are sent as a base64 encoded authentication header making it very susceptible to eavesdropping attacks.

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

The authorization header is just a base64 encoded string of the username and password:

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

An attacker may change authentication information to gain ATO.

