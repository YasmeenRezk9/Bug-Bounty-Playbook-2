# Databases

## <mark style="color:yellow;">Google Firebase</mark>

If we find an application using Firebase, append “/.json” to the url, and if there isn't authentication we can export the entire DB.

EX:&#x20;

* vuln-domain.firebaseio.com/.json

## <mark style="color:yellow;">ElasticSearch DB</mark>

💡Note: It's unauthenticated by default and always be on the lookout for port **9200**.

💡NoSQL database that uses JSON-like documents to store data.

💡Interesting indexes to search for:&#x20;

* Username, Email, Password, Token, Secret, and Key.

Once you have identified that your target has port 9200 open you can easily check if it is an ElasticSearch database by hitting the root directory with a GET request.

1. **Shodan:** port:"9200" elastic
2. Once you know an endpoint has an exposed Elastic Search db try to find:-

**All the indexes(Databases) that are available:**

**-->** “/\_cat/indices?v” endpoint with a GET request.

**-->**  “/\_stats/?pretty=1” endpoint with a GET request.

**List all of the field names:**

**-->** “/\_all/\_search?q=INDEX\_NAME\_HERE”

**-->** “/INDEX\_NAME\_HERE/\_mapping?pretty=1”

**Query all values that contain a specific field name:**

**-->** “/\_all/\_search?q=\_exists:INDEX\_NAME\_HERE\&pretty=1”

## <mark style="color:yellow;">Mongo Database</mark>

💡NoSQL database that uses JSON-like documents to store data.

💡Note: It's unauthenticated by default and always be on the lookout for port **27017**.

#### Steps to exploit:

1. See if port 27017 is open or any other MongoDB associate port.
2. Test the endpoint to see if it's missing authentication.
3. Connect to the database and extract the data using the Mongo CLI:

&#x20;       \--> mongo \<IP>

4. If we can run arbitrary commands against the system then authentication has not been set up and we can do whatever you want.

## Notes

| Name          | Endpoint                |
| ------------- | ----------------------- |
| Firebase DB   | \*.firebaseio.com/.json |
| Elasticsearch | Port:9200               |
| MongoDB       | Port:27017              |
| CouchDB       | Port:5985,6984          |
| CassandraDB   | Port:9042,9160          |

