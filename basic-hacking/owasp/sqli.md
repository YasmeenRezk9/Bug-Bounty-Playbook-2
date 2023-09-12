# SQLI

The leading cause of SQL injection is string concatenation.

This vulnerability can be exploited to dump the contents of an application database.

#### The two most common types of SQL injection are union-based and error-based.

1. **Union-based SQL injection:** uses the “UNION” SQL operator to combine the results of two or more “SELECT” statements into a single result.
2. **Error-based SQL injection:** utilizes the errors the SQL server throws to extract information.

## <mark style="color:yellow;">MySql</mark>

Automation: using[ SqlMap](https://github.com/sqlmapproject/sqlmap).

#### Union Based

Once you know that an endpoint is vulnerable to SQL injection the next step is to exploit it:

* Figure out how many columns the endpoint contains using the “order by” operator and keep adding one to the number until you get an error:

&#x20;     \--> Order by 1 --> Order by 2 --> Order by n --> error (indicates there must be n-1 columns).

* Figure out which columns are being displayed on the page using the “union all select” statement which can be accomplished by putting an invalid value:

&#x20;    \--> Notice the numbers on the page refer to the columns displayed on the front end.

* Display the database version using mysql commands:

&#x20;     \--> @@version /  version()

&#x20;     \--> 💡Note the version down to help later

* Get a list of database tables:

```sql
union all select 1,2,group_concat(table_name) from information_schema.tables 
where table_schema = database() 
```

