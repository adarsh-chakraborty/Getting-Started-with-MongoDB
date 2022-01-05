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
