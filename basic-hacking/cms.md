---
description: >-
  When you find a CMS, test for known CVEs and misconfigurations using a sort of
  CMS-specific vulnerability scanner.
---

# CMS

## <mark style="color:yellow;">WordPress</mark>

If you find a Drupal site, use [droopescan ](https://github.com/SamJoan/droopescan)to scan it:

Once you find a site running WordPress, scan it with  [**wpscan**](http://127.0.0.1:5000/s/s0FhLkcDMqdY8oYdPmjA/part-3-web-vulnerabilities/ch9-cross-site-request-forgery)

* wpscan --url \<URL>

Always make sure to check the uploads folder "/wp-content/uploads/"

* search for sensitive information such as user emails, passwords, and paid digital products.

## <mark style="color:yellow;">Drupal</mark>

If you find a Drupal site, use [droopescan ](https://github.com/SamJoan/droopescan)to scan it:

* droopescan scan drupal -u \<URL>

## <mark style="color:yellow;">Joomla</mark>

If you find a Joomla site, use [joomscan ](https://github.com/rezasp/joomscan)to scan it:

* joomscan -u \<URL>

## <mark style="color:yellow;">Adobe AEM</mark>

If you find an Adobe AEM site, use [aem\_hacker ](https://github.com/0ang3el/aem-hacker)to scan it:

* python aem\_hacker.py -u \<URL> --host \<Our Public IP>

## <mark style="color:yellow;">Magento</mark>

If you find a Magento site, use [magescan ](https://github.com/steverobbins/magescan)to scan it:

* magescan.phar scan:all sub.example.com



