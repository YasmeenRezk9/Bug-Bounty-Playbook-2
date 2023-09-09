---
description: >-
  Once you hear about a new exploit you will need to quickly find a POC for it
  and start mass scanning all  of your targets for that vulnerability.
---

# Known Vulnerabilities

### There are only three steps when using this approach:

1. Determine your target tech stack.
2. Search for any vulnerabilities in that tech stack.
3. Run the exploits.

## <mark style="color:yellow;">Identifying technologies</mark>

1. Wappalyzer
2. Powered By

## <mark style="color:yellow;">Identifying the vulnerabilities</mark>

1. **Google**

Try typing the following search queries into Google:

* \<TECHNOLOGY> \<VERSION> vulnerabilities
* \<TECHNOLOGY> \<VERSION> exploits

2. **ExploitDB**

ExploitDB provides us with the proof of concept(POC) code as well.

* Online: [ https://www.exploit-db.com/ ](https://www.exploit-db.com/)
* CL: [https://gitlab.com/exploit-database/exploitdb](https://gitlab.com/exploit-database/exploitdb)

&#x20;         \--> searchsploit “name of technology”

3. **CVE**

To exploit a CVE you need the proof of concept(POC) exploit code, without that you're stuck.

* [https://nvd.nist.gov/vuln/search](https://nvd.nist.gov/vuln/search)

## <mark style="color:yellow;">Finding the POC</mark>

1. Github
2. ExploitDB

## <mark style="color:yellow;">Exploitation</mark>

Run the exploit on your target and review the results to see if they are vulnerable or not.

