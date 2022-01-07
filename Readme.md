# MongoDB

![MongoDB](https://github.com/adarsh-chakraborty/Getting-Started-with-MongoDB/blob/main/assets/banner.png)

## What is MongoDB

MongoDB is a database offered by the company of the same name. The database was officially named MongoDB, with “Mongo” being short for the word humongous.

## How it works

Where in SQL world, we have Schemas and tables, In MongoDB is a **NoSQL** solution, here we have collections, these collections we have so called documents.. these documents looks like JavaScript Objects.

**Documents are stored in JSON (BSON) data format, in key value pairs.**

We can store nested data in there, which makes working with Complex data super efficient, where in SQL we would had to Join tables, from table A, table B etc, Here we can save it in a logical way directly in database instead of maintaining relationships.

## Schemaless architecture

MongoDB provides flexible Schemaless architecture, where MySQL would scream if we our one record looks different from other, SQL is strict about having all the records under some Schema so all the records share same attributes where in MongoDB, One document can totally be different from the other.

## Installing MongoDB

Install the following softwares from the mongodb official site: 

- Community Server
- Compass
- MongoDB Shell

*MongoD is a service which is our server and It'll run in background and Shell is what we will need to execute commands/query, which then talks to actual server running on the machine and shows output on the screen.*

## Basic MongoDB Commands

While using MongoDB, We don't really have to create databases or collections in advance, while executing the query, If it doesn't exists, MongoDB creates it for you on the fly.

```
show dbs
```
  >Lists all available databases on the system.
  ---
```
use database_name
```
  >Selects the database you want to work with. 
  ---

```
db.products.insertOne({'product_name': 'Rubber Duck'});
```
  >Inserts a new document in the products collection. It will create products collection if it doesn't exist.  
  >We can omit quotes in the key name on mongodb shell but not for value.
  ---
```
db.products.find();
```
  >Finds all documents in the products collection.  
  ---
  ```
db.dropDatabase();
```
  >Drops the current database.

That were some basic commands to start with.

---
  
# CRUD Operations

CRUD basically means *Create, Read, Update, Delete* operations. We have Methods available to perform such operations on mongoDB.

`CREATE:`
```javascript
insertOne(data, options)
insertMany(data, options)
```


`READ:`
```javascript
find(filter, options)
findOne(filter, options)
```

`UPDATE:`
```javascript
updateOne(filter, data, options)
updateMany(filter, data, options)
replaceOne(filter, data, options)
```

`DELETE:`
```javascript
deleteOne(filter, options)
deleteMany(filter, options)
```

---

## Inserting Documents

`insertMany()` allows us to Insert many elements into the database, It takes an Array of Objects that we want to Insert to database.

```javascript
db.users.insertMany([
    {
        name: 'Adarsh',
        age: 23
    },
    {
        name: 'Mark,
        age: 30
    }
]);
```

`insertOne()` simply takes one object and Inserts it to the database, If `_id` is not specified it creates an Unique `ObjectId()` and assigns it to `_id` field. This property must be unique otherwise it will throw exception while writing to database.

## Finding Documents

We know that `find()` a cursor to all the documents in the collection, we can actually pass some filter and options to filter through documents.

For that, we need to pass an object to `find()` method and specify our filter.

```javascript
db.users.find({name: 'Adarsh'}).toArray();
```

Now, find method will return cursor to all the documents with `name: 'Adarsh'` and we convert all of it to an Array by `toArray()` method.

`findOne()` will return only the first document that matches the filter, if no filter is passed, It simply returns the first document in database.

- Finding all the users whose age is greater than 20.

```javascript
db.users.find({age: {$gt: 20}});
```

Here, we passed an object to `age` property, and in the object we defined an special operator `$gt` which means greater than.

## Updating Documents 

We can update documents by using `updateOne()` and `updateMany()` methods.  

While trying to update, MongoDB has no way to know how to update the documents so we have to explicitly tell it how to update, for these we use special operators available to describe the changes we wanna make on mongodb.These operators names start with `$` sign.

Here, we pass two arguements to update function
- First is the filter to select which document to update.
- Second is an object with a special property `$set`.
- The value `$set` property is the new update that we want to perform on the document.
- The `$set` operator replaces the value of a field with the specified value.

```javascript
db.users.updateOne({name: 'Adarsh'}, {$set: {age: 23}});
```

Making some change on all the documents: 

```javascript
db.users.updateMany({}, {$set: {isAdmin: false}});
```

`updateMany()` has no filter, so it will peform the `$set` operation on all the documents in the collection, so isAdmin is now false for all users.


There is another `update()` method, which we can use without `$set` operator but it basically overwrites the document with the data we provide, for such replacement task we can use `replaceOne()` method.

```javascript
db.users.replaceOne({_id: '02'}, {
    name: 'Adarsh Chakraborty',
    age: 23,
    isAdmin: true
});
```

Here, the document with `id: 23` will be replaced by this new document, the `_id` will remain the same ofc.

## Deleting Documents 

`deleteOne()` deletes one document from database where `deleteMany()` would try to delete many documents from the database.

We can pass an object which specifies the criteria to delete the documents.

- `deleteOne({name: 'Adarsh'});` deletes one document where `name` is `Adarsh`. (First Matched Document would be deleted).
- `deleteMany({name: 'Max'});` deletes all documents where `name` is `Max`.
- `deleteMany({});` deletes all the documents from a collection as no filter is passed.
- `deleteOne({});` deletes the first document from the collection as no filter is passed. 

---

# Projection

By default, queries in MongoDB return all fields in matching documents. To limit the amount of data that MongoDB sends to applications, you can include a projection document to specify or restrict fields to return. It is passed in 2nd arguement in `find()`, `findOne()` methods.

```
db.inventory.find( { status: "A" }, { item: 1, status: 1, _id: 0 } );
```

- `1` means Include.
- `0` means Exclude or Suppress.
- `_id` is always included by default, to supress the `_id` as well.
- We have to explicitly exclude it by setting `{ _id: 0 }` in projection.

# Embedded Documents 

MongoDB provides you a cool feature which is known as Embedded or Nested Document. Embedded document or nested documents are those types of documents which contain a document inside another document.

OR, In other words, when a collection has a document, this document contains another document, another document contains another sub-document, and so on, then such types of documents are known as embedded/nested documents.  


It's a core feature of MongoDB.

- MongoDB can store upto `100 levels` of Nested documents.
- The maximum BSON document size is 16 megabytes.

# Schema and Modeling Data

Before you ask **"Isn't MongoDB Schema Less??!!"**, yes It is Schema-less, It allows us to store data without having a proper Schema but Sometimes and mostly we would like to keep data in a proper Schema.

Like a Product will have some Details like Id, Product Name, Stock and Price, 
Then Orders would contain the Products, UserId, Payment details etc.

So, MongoDB enforces no Schema on us but Having Schema is Important, It's just we can store Schemaless stuff.
