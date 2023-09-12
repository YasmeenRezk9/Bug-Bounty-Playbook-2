---
description: >-
  One of the easiest ways to spot a subdomain takeover vulnerability is by the
  error message.
---

# Subdomain Takeover

## <mark style="color:yellow;">Subdomain Takeover</mark>

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Occurs when a subdomain is pointing to another domain (CNAME) that no longer exists.

* An attacker can then register the non-existing domain. Now the target subdomain will point to a domain the attacker controls.

A bunch of examples and walkthroughs on exploiting different providers:

* [https://github.com/EdOverflow/can-i-take-over-xyz](https://github.com/EdOverflow/can-i-take-over-xyz)

## <mark style="color:yellow;">GitHub Takeover</mark>

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

After we have an indicator that this site is vulnerable we need to get the GitHub page the vulnerable subdomain is pointing to. We need this information so we can register the domain through github.

1. Use the "dig" command to gather the DNS records of the vulnerable domain.
2. If the domain points to the github page, try to register a domain on Github.

#### Steps to register a domain on Github:

1. Create a Github repo with the same name as the CNAME record.
2. Create an “index.html” file in the repo.
3. Set the repo as the main branch.
4. set the custom domain to the target domain you are going after.
5. When you visit the target domain you should see the page you set up.

{% tabs %}
{% tab title="¯\_(ツ)_/¯" %}
SWAP Tabs
{% endtab %}

{% tab title="1" %}
<figure><img src="../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="2" %}
<figure><img src="../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="3" %}
<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="4" %}
<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="5" %}
<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>
{% endtab %}

{% tab title="6" %}
<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}



