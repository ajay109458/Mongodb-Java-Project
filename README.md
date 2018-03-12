# Configure Java application with MongoDB

## Adding libraries 

Note: Any one of the below step mentioned in this section is required.

### Java project ( with Jars ) 
* Download mongo-java-driver JAR 
* Create a lib folder in project and copy above downloaded JAR
* Import java to build path.

### Maven based project
```
<dependencies>
    <dependency>
        <groupId>org.mongodb</groupId>
        <artifactId>mongo-java-driver</artifactId>
        <version>2.12.3</version>
    </dependency>
</dependencies>
```

### Gradle based project
```
dependencies {
    testCompile 'junit:junit:4.11'
    testCompile 'org.hamcrest:hamcrest-all:1.3'
   +-------------------- ========= GOLDEN ======== -------------------------+
   | compile 'compile 'org.mongodb:mongo-java-driver:2.12.3'                |
   +------------------------------------------------------------------------+
}
```

## Sample Application
```
import com.mongodb.client.MongoDatabase; 
import com.mongodb.MongoClient; 
import com.mongodb.MongoCredential;  

public class MongoDBSampleApplication { 
   
   public static void main( String args[] ) {  
      
      // Creating a Mongo client 
      MongoClient mongo = new MongoClient( "localhost" , 27017 ); 
   
      // Creating Credentials 
      MongoCredential credential; 
      credential = MongoCredential.createCredential("username", "databasename", 
         "password".toCharArray()); 
      System.out.println("Connected to the database successfully");  
      
      // Accessing the database 
      MongoDatabase database = mongo.getDatabase("databasename"); 
      System.out.println("Credentials ::"+ credential);  
      
      // Create collection 
      database.createCollection("firstcollection"); 
      
      // Get documents from collection
      MongoCollection<Document> collection = database.getCollection("firstcollection);
      
      // Insert a document in the collection
      Document document = new Document("title", "Software Developer") 
      .append("id", 1)
      .append("name", "Ajay Yadav") 
      .append("age", 26) 
      .append("by", "Ajay Yadav");  
      
      collection.insertOne(document); 

   } 
}
```

## MongoDB Java 

#### Connect to database server
```
MongoClient mongoClient = new MongoClient(new MongoClientURI("mongodb://localhost:27017"));
```

Note: If you’re connecting to a local instance on the default port, you can simply use:
```
MongoClient mongoClient = new MongoClient();
```

#### Creating and getting a database
```
DB database = mongoClient.getDB("TheDatabaseName");
```

#### Getting collection from database
```
DBCollection collection = database.getCollection("TheCollectionName");
```

#### Creating a document and save it to databse
* Create a document 
```
List<Integer> books = Arrays.asList(27464, 747854);
DBObject person = new BasicDBObject("_id", "jo")
                            .append("name", "Jo Bloggs")
                            .append("address", new BasicDBObject("street", "123 Fake St")
                                                         .append("city", "Faketon")
                                                         .append("state", "MA")
                                                         .append("zip", 12345))
                            .append("books", books);
```
* Save document to database
```
MongoClient mongoClient = new MongoClient();
DB database = mongoClient.getDB("Examples");
DBCollection collection = database.getCollection("people");
    
collection.insert(person);
```

## Simplify CRUD operation with JONGO (ODM - Object document mapper)
 Jongo is Jackson-based ODM. [Jongo Documentation](http://jongo.org/)
 
## Other ODM for MongoDB
* Morphia
* Spring Data
* MongoJack
* Jongo
* Grails MongoDB GORM
* Casbah
