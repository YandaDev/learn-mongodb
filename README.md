# MongoDB Notes

MongoDB is a NoSQL database management system that can manage a humongous amount of data.  
Unlike relational database management systems, MongoDB uses a NoSQL format to store and retrieve data.

![NoSQL Diagram](docs/NoSQL_Diagram.png)

**NoSQL** stands for **Not Only Structured Query Language**.  
It means data is stored in various formats besides a traditional SQL table.

![SQL vs NoSQL](docs/SQL_vs_NoSQL.png)

Rather than storing data in rows and columns within a table (as in SQL), MongoDB stores related data as a single document.

Think of each document as a single row in a SQL table:

![Rows vs Documents](docs/Rows_vs_Documents.png)

Data in each document is stored as field-value pairs, similar to JSON format (technically BSON: Binary JavaScript Object Notation).  
The general idea is that data frequently accessed together is stored together, rather than in separate tables, because SQL joins can be complex.

```js
{
   name: 'Spongebob',
   age: 30,
   gpa: 3.2,
   fullTime: false
}
{
   name: 'Patrick',
   age: 38,
   gpa: 1.5,
   fullTime: false
}
{
   name: 'Sandy',
   age: 27,
   gpa: 4,
   fullTime: true
}
```

## MongoDB Structure

- **Document:** A group of field-value pairs representing an object.  
  ![A document](docs/Document.png)

- **Collection:** A group of one or more documents.  
  ![A collection](docs/Collection.png)

- **Database:** A group of one or more collections.  
  ![A database](docs/Database.png)

This structure makes working with and scaling your database easy.

---

## Basic Commands to Get Started

- Establish the connection by initiating the MongoDB shell using the `mongosh` command.
- Type `cls` to clear the screen.
- Type `exit` to exit the MongoDB shell.

### Creating and Using Databases

- `show dbs` — Show all databases.
- `use <database_name>` — Use an existing database or create a new one.
  - Example: `use school`

A new database will not appear in the list until you add a collection to it.

### Creating a Collection

Use the `createCollection` method:

```js
db.createCollection("students")
```

To drop the current database:

```js
db.dropDatabase()
```
![Create a collection and drop a database](docs/Create_collection_and_drop_database.png)

---

## Inserting Documents

Switch to the database you want to use:

```js
use school
```

### Insert One Document

```js
db.students.insertOne({name: "Spongebob", age: 30, gpa: 3.2})
```

### Insert Multiple Documents

```js
db.students.insertMany([
  {name: "Spongebob", age: 30, gpa: 3.2},
  {name: "Patrick", age: 38, gpa: 1.5},
  {name: "Sandy", age: 27, gpa: 4}
])
```
![InsertMany method](docs/InsertMany.png)

---

## Basic Data Types in MongoDB

1. **String:** Series of text within quotes (e.g., `"Monkey D Luffy"`)
2. **Integer:** Whole numbers (e.g., `27`)
3. **Double:** Numbers with decimal portions (e.g., `3.2`)
4. **Boolean:** `true` or `false`
5. **Date Objects:** Use `new Date()` or pass a date string.
6. **Null:** Represents no value.
7. **Arrays:** A field that can have more than one value.
8. **Nested Documents:** Useful for addresses or embedded objects.

![MongoDB Data Types](docs/MongoDb_data_types.png)

---

## Sorting and Limiting Documents

To sort documents, use method chaining with `find()` and `sort()`:

```js
db.students.find().sort({name: 1})   // Sort by name in ascending (A-Z) order
db.students.find().sort({name: -1})  // Sort by name in descending (Z-A) order
db.students.find().sort({gpa: 1})    // Sort by GPA ascending
db.students.find().sort({gpa: -1})   // Sort by GPA descending
```
![Sort Name Field In Alphabetical Order](docs/Sort_Alphabetical_Order.png)  
![Sort Name Field In Reverse Alaphabetical Order](docs/Sort_R_Alphabetical_Order.png)

### Limiting Results

Use the `limit()` method to restrict the number of documents returned:

```js
db.students.find().limit(1)
```
![Limit One Document](docs/limit_1.png)

You can combine `sort()` and `limit()`:

```js
db.students.find().sort({gpa: -1}).limit(1) // Student with the highest GPA
```
![Student With The Highest GPA](docs/sort_and_limit.png)

---

## Querying Documents

The `find()` method returns all documents by default.  
To filter results, use query and projection parameters:

```js
db.students.find({query}, {projection})
```

### Query Parameter

- Filters documents based on criteria.

Examples:

```js
db.students.find({name: "Zoro"})
db.students.find({gpa: 2.5})
db.students.find({gpa: 3.8, fullTime: false})
```
![Find Method With Query Parameter](docs/find_method_query.png)  
![Find Method With Two Filters](docs/find_method_2_filters.png)

### Projection Parameter

- Specifies which fields to return.

Examples:

```js
db.students.find({}, {name: true}) // Only return names
db.students.find({}, {_id: false, name: true}) // Exclude _id, only names
db.students.find({}, {_id: false, name: true, gpa: true}) // Only names and GPA
```
![Find Method Projection Parameter](docs/projection_parameter.png)

---

## Updating Documents

You can update one or many documents.

### `updateOne` Method

- Takes two parameters: filter and update.

```js
db.students.updateOne({filter}, {update})
```

#### Example: Add or Update a Field

```js
db.students.updateOne(
  {name: "Sanji"},
  {$set: {fullTime: true}}
)
```
![Update One Method](docs/update_one_method.png)

#### Example: Update Using ObjectId

It's safer to update using the unique ObjectId, especially if names are not unique.

```js
db.students.updateOne(
  {_id: ObjectId("...")},
  {$set: {fullTime: false}}
)
```
![Update One Method_](docs/objectId_filter.png)

#### Example: Remove a Field

Use the `$unset` operator to remove a field:

```js
db.students.updateOne(
  {name: "Sanji"},
  {$unset: {fullTime: ""}}
)
```

---