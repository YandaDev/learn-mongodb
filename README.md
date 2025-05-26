# MongoDB Notes
MongoDB is a NoSQL database management system that can manage a humongous amount of data
Unlike relational database Management systems, MongoDB uses a NoSQL format to store and retrieve data.

![NoSQL Diagram](docs/NoSQL_Diagram.png)

NoSQL means N=Not O=Only S=Structured Q=Query L=Language
It's where data is stored in various formats besides a traditional SQL table

![SQL vs NoSQL](docs/SQL_vs_NoSQL.png)

Rather than storing our data in rows and columns with a table using SQL, we store related data as a single document

Think of each document as a single row in a table in SQL
![Rows vs Documents](docs/Rows_vs_Documents.png)

Data in each document is stored as field value-pairs
Similar to a JSON format, but it's technically BSON, Binary JavaScript Object Notation but it behaves very similarly for all intents and purposes
The general idea is that data which is frequently accessed together is stored together, rather than in separate tables because SQL joins are complex
``
{
   name: 'Spongebob',
   age: 30,
   gpa: 3.2,
   fullTime: false, 
}
{
   name: 'Patrick',
   age: 38,
   gpa: 1.5,
   fullTime: false, 
}
{
   name: 'Sandy',
   age: 27,
   gpa: 4,
   fullTime: true, 
}

``

Here is how a NoSQL database is arranged

A document
Is a group of field value-pairs to represent an object
![A document](docs/Document.png)

A collection
Is a group of one or more documents
![A collection](docs/Collection.png)

A databse
Is a group of one or more collections
![A database](docs/Database.png)

This makes working with and scaling our databse easy

Basic commands to get started
Establish the connection by initiating the MongoDB shell using the `mongsh` command
Type `cls` to clear the screen
Type `exit` to exit out of the MongoDB shell

Create and use databases in MongoDB
Type `show dbs` to show all database, this will give you the list of all current databases

Type `use <select database name if exist>` to use an existing database
Type `use <new database name>` to create a new database
`use school`

After creating a new database it doesn't show immeditately when showing a list of database until you add a collection to it

To create a collection to our databasewe use the createCollection method
It ends with a parenthes just like a function in typical programming languages
`db.createCollection()`
Within a set of parenthesis we pass in an argument for a name for the collection wrapped in double quotes or single quotes depending on your preference
`db.createCollection("students")`

To drop a current database we use `db.dropDatabase()` method
![Create a collection and drop a database](docs/Create_collection_and_drop_database.png)


How to insert documents into a MongoDB database
Switch of to the database that you want to use `use school `

Using the insertOne() method

Type `db.<the name of the collection if it's found within the database/ if it doesn't exis one will be created for you>.insertOne().
`db.students.insertOne()`

Within the set of parenthes we place a document which is enclosed within a set of currly braces 

Within  the set of currly braces we can list as many field-value pairs as we would like

Each field-value pair is comma separated
`db.students.insertOne({name:Spongebob", age:30, gpa:3.2})`

To return all documents we use the find method
`db.students.find()`
![InserOne and find methods](docs/InsertOne_and_find_method.png)

You can insert more than one document at a time by using the insertMany() function

place all documents to be inserted within an array by adding a set of square brakets

Within a set of square brackets add a set of currly braces all comma separates and within each set of currly braces list all of the different field value pairs
`db.students.insertMany([{}, {}, {}])
The array contains several documents
Each document is enclosed with a set of currly brackets
Within each document you can have as many field-value pairs as you like, they all don't need to be consistent
![InsertMany method](docs/InsertMany.png)

Basic data types in MongoDB
1. A string 
- Is a series of text within quotes (double/single)
- They can contain spaces i.e Monkey D Luffy
- They can contain number i.e Brook99 .numbers a treated differently, we read them more as characters rather than actual numbers

2. Intergers
- An interger is a whole number.

3. Doubles
- A double is a number that contain decimal portions

4. Booleans
- Are either true or false
- Kind of like a light switch, it's only on or off, there's only two states 

5. Date objects
To create a date object you can use the `new` keyword followed by a call to the date constructor
If you don't pass any arguments to the date constructor, you'll use the current time in the UTC time-zone, otherwise you pass a date in time and you could add the time as well

6. null
- means no value

7. Arrays
- much like in mordern programming languages is kind of like a variable that has more than one value, but in MongoDB we  have a field that can have more than one value

8. Nested documents
- Good for addresses
- To create a nested document you use a set of currly braces,within the nested document we can list some field value pairsCo
![MongoDB Data Types](docs/MongoDb_data_types.png)

How to sort and limit documents in MongoDB

To sort documents into some sort of order we type `db.<name of the collection>.find()` then do method chaining, after the find method we add. and call the sort method

The sort()
Takes a document by which field wwould we like to sort
Below shows how to sort names in alphabetical order 1
![Sort Name Field In Alphabetical Order](docs/Sort_Alphabetical_Order.png)

Below shows how to sort names in reverse alphabetical order -1
![Sort Name Field In Reverse Alaphabetical Order](docs/Sort_R_Alphabetical_Order.png)
 