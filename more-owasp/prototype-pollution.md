---
description: No limit to what you can potentially do with this vulnerability.
---

# Prototype Pollution

**JS is a prototype-based language.**

* JS objects inherit features from one another using Prototypes meaning if the prototype object is modified in one object it will apply to every other object.
* Prototypes are used to overwrite functions, variables, and anything else.

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption><p>Prototype Figure</p></figcaption></figure>

### Exploitation

**Goal:** setting the “admin” variable to true.

<figure><img src="../.gitbook/assets/image (38).png" alt=""><figcaption><p>Vulnerable code snippet</p></figcaption></figure>

During the merge process if it comes across a prototype object it will add that to the user object.

#### To do:

* Sending a prototype object with a variable called “admin” which is set to “true”
* The admin object inherited the admin variable from the modified prototype object.
* When the line checks to see if admin.admin is set to true it will pass.

<figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>
