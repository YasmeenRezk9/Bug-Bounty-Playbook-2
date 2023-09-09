---
description: All you need is a good credential list and you're ready to go.
---

# Brute Forcing

## <mark style="color:yellow;">Login Pages</mark>

First, you need to find the endpoint you want to target:

| Name    | Endpoint                                                                    |
| ------- | --------------------------------------------------------------------------- |
| Web app | login page, Outlook mail, VPN, Router, Firewall, WordPress admin panel, etc |
| SSH     | Port:22                                                                     |
| RDP     | Port:3389                                                                   |
| VNC     | Port:5900                                                                   |
| FTP     | Port:21                                                                     |
| Telnet  | Port:23                                                                     |

## <mark style="color:yellow;">Default Credentials</mark>

Based on service brute force, try default usernames and passwords in [SecList](http://127.0.0.1:5000/s/fhxUUXRbr4vDbfeE6iMR/orwa-method-4-parts).

* use Google to search for non-existing services.

## <mark style="color:yellow;">Brute Forcing</mark>

Use the tool [Hydra ](https://github.com/vanhauser-thc/thc-hydra)to perform a brute-force attack.

