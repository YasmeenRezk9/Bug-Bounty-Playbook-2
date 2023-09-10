# SQLI

The main cause of SQL injection is string concatenation.

This vulnerability can be exploited to dump the contents of an application database.

#### The two most common types of SQL injection are union-based and error-based.

1. **Union-based SQL injection:** uses the “UNION” SQL operator to combine the results of two or more “SELECT” statements into a single result.
2. **Error-based SQL injection:** utilizes the errors thrown by the SQL server to extract information.

## <mark style="color:yellow;">MySql</mark>

Automation: using[ SqlMap](https://github.com/sqlmapproject/sqlmap).

### Manual Exploitation

#### 1.  Union Based

Once you know that an endpoint is vulnerable to SQL injection the next step is to exploit it:

*
