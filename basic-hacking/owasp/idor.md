---
description: Insecure Direct Object Reference
---

# IDOR

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption><p>IDOR</p></figcaption></figure>

#### Occurs when a user can view unauthorized data:

* developers might forget to include authentication checks when retrieving data so that attackers can supply other users' IDs to retrieve data belonging to them.
* since the user id is guessable and increments by one for every user this attack could also be scripted to exploit every user on the application.
* It's common practice to hash user IDs before storing them in a database.

**Spotted by looking for a request that contains** your user id, username, email, or some other id tied to your user.

**Also exploited to send commands to the application such as** adding an admin account, changing a user's email, or removing a set of permissions.

**Once exploited this vulnerability** can be used to retrieve sensitive information of other users or issue commands to other users.

