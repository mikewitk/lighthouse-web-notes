# MongoDB

So far, all of our "Data" is being stored in memory, and will be kept there as log as the application is running.

But as soon as the application is not running anymore, the memory will be released and be freed to be used by other application.

**Besides SAVING to the DISK, we need to LOAD from the disk**

If there are multiple computers writing on the disk, these computers need to update the data they know (load from the disk) before writing on it.

DataBase = anything that will store data

MongoDB is a server.

"waiting for connection" is the way MongoDB have to say "I am ready and waiting"

"./mongo" to run it

"show dbs" -> show databases

"use <dbName>" -> change to the selected db

"show collections" -> show the data stored. An array of objects in JS. A collection of documents

"db.<collection>.find()" -> shows whats stored inside the collection

"db.<collection>.find().pretty()" -> visualize in a better way

"db.<collection>.insert( { <object> } )" -> insert into the DB

"db.<collection>.find({name: "Juan"})" -> return the whole object(s) that contains the name Juan.

"db.<collection>.insertOne( { <pair value to be inserted> } )" -> insert one document to the specified "collection"

"db.<collection>.insertMany( [ { <pair value to be inserted> } ] )" -> insert many documents to the specified "collection"

Be mindful where you are calling mongoDB, ex: javaScript, MongoShell, etc

## Mongo DB Manual

A record in MongoDB is a `document`, which is a data structure composed of fields and value pairs. The value of fields may include other documents, arrays, and arrays of documents.



