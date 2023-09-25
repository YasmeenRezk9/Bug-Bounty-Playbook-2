---
description: >-
  Compromising the authentication process will lead to account takeover (ATO)
  vulnerabilities and depending on the accounts you takeover it could also lead
  to privilege escalation.
---

# Authentication

## <mark style="color:yellow;">HTTP Basic Auth</mark>

Each time you send a request your clear text username and password are sent as a base64 encoded authentication header making it very susceptible to eavesdropping attacks.

<figure><img src="../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

The authorization header is just a base64 encoded string of the username and password:

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

An attacker may change authentication information to gain ATO.

## Json Web Token (JWT)

💡Popular among API endpoints.

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

User attempts to login -> system sends credentials to the back end API -> backend verifies the credentials and if they are correct -> generates a JWT token sent to the user proving identity.

#### Consists of three parts separated by dots:&#x20;

1. Header -> specifies the algorithm used to generate the signature.
2. Payload -> used for access control.
3. Signature -> makes sure the token has not been modified or tampered with.

#### Signature methods to sign a JWT token:

1. None
2. HMAC
3. RSA

#### EX

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

### None Algorithm

Any JWT token will be valid as long as the signature is missing.

💡Done manually or you can use a Burp plugin called “Json Web Token Attacker”.

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

### Brute Force Secret Key

JWT tokens will either use an HMAC or RSA algorithm to verify the signature.

#### To crack these keys:

* [https://github.com/AresS31/jwtcat](https://github.com/AresS31/jwtcat)
* [https://github.com/lmammino/jwt-cracker](https://github.com/lmammino/jwt-cracker)
* [https://github.com/mazen160/jwt-pwn](https://github.com/mazen160/jwt-pwn)
* [https://github.com/brendan-rius/c-jwt-cracker](https://github.com/brendan-rius/c-jwt-cracker)
* GitHub Dorking: “jwt cracker”

#### RSA to HMAC

**RSA** uses a private key to generate the signature and a public key for verifying the signature.

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption><p>RSA</p></figcaption></figure>

**HMAC** uses the same key for generating and verifying the signature.

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption><p>HMAC</p></figcaption></figure>

## <mark style="color:yellow;">Security Assertion Markup Language (SAML)</mark>&#x20;

An authentication scheme that allows a user to log in with a single ID and password to any of\
several related, yet independent, software systems.

* the goal of SSO is to use one set of credentials across multiple websites.

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

Login to target website AKA service provider (SP) -> forwarded to the SSO website -> credentials will be sent to the ID -> ID checks the supplied credentials against a database if there is a match ✅ -> forwarded back to the SP with our SAML assertion that contains our identity.

#### Original SAML Response

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### XML Signature Removal

On some systems, it is possible to bypass this verification by removing the signature value or the entire signature tag from the assertion or message.

1. Removing the signature value:

* Try to make the “SignatureValue” data blank so it looks like "\<ds:SignatureValue>\</SignatureValue>"

2. Completely remove the signature tags from the request:

* using the SAML Raider plugin in Burp -> clicking the “Remove SIgnatures” button

This would allow an attacker to supply another user's email giving them full access to their account.

### XMLComment Injection

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>
