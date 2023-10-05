# Directory Traversal

If an application uses user-supplied input to interact with files on the system then there is a chance the endpoint is vulnerable to directory traversal.

* If you find this vulnerability make sure to look for config files, source code, or if it is in an upload functionality try overwriting files on disk.

### Source Code Snippet

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### &#x20;Exploitation

The GET parameter “page” is loaded into a variable called “file”:&#x20;

* on line 10 the file is opened and read out to the page and as it appears there are no additional checks.
* In case improperly implemented, attackers leverage the “../” technique to load any file they want.

EX: [https://example.com/?page=index.html](https://example.com/?page=index.html)&#x20;

* can exploit this vulnerability to retrieve the “/etc/passwd” file from the operating system.
* [https://example.com/?page=](https://example.com/?page=index.html)../../../../../../etc/passwd
* Retrieving /etc/passwd content.

#### 💡NOTE

* “../” characters will traverse back one directory so can be used to retrieve sensitive files by traversing up or down the file structure.
* The “/etc/passwd” file is used to store information on each user account in a Linux system.

