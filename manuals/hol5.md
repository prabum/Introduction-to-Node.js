# Introduction to Node.js
# HOL5 – Working with data
## Description
MongoDB is one of the most commonly used databases for Node.js, and during this lab we are going to move the static **products** collection to one in MongoDB. Preceding this exercise, you should have MongoDB installed, but before we start you’ll need to do some setup.
## Before you begin
* Install the **mongodb** npm package (you know how right?)
* Create a new folder called *MongoDB* in your course folder.
* Open the MongoDB installation folder and browse the bin folder (default *C:\Program Files\MongoDB\Server\3.2\bin on Windows*, */usr/local/mongodb* on Mac OS X)
* Copy all files to the folder you created in previous step.
* In the new *MongoDB* folder, create a new directory called **data\db**. Eg "mkdir .\data\db"
* Open a console/terminal and browse to the new *MongoDB* folder
* Type **mongod --httpinterface --rest** and hit ENTER

You should now have MongoDB server started and you should be able to browse to [http://localhost:28017/](http://localhost:28017/) using your favorite browser.

## Exercise 
1. Create a new file called *hol5.js* and copy the entire content from *hol3.js*
2. Remove the declaration of the *products* collection and add:
```js
var mongoDb = require('mongodb');
var url = "mongodb://localhost:27017/hol5Db"
var products;
```
### Create the database connection
Continue by adding the section below:
```js
mongoDb.MongoClient.connect(url, function(err,db){
     products = db.collection("products");
});
```
This statement creates a database called **hol5Db** (if it doesn't exist). After successfully connected, it will create a collection called "**products**".

### Update all operations
We are now ready to update the **GET** and **POST** operations to use the newly created collection. Remember that you should still respond the same way you did before…

#### To query for **all** products use this syntax:
```js
products.find().toArray(function(err, products){
   // respond from here...
});
```
#### To query for a single instance use this syntax:
```js
products.findOne( {id:id}, function(err, product) {
   // respond from here...
});
```
**Note** *{id:id}* is the query you'll use.

**Hint:** The incoming query parameter (req.query.id) is a string, which you’ll need to convert using the *Number()* function. 

#### To insert a product to a collection, use this syntax:
```js
products.insert(req.body, function (err, ret) {  
  res.send(ret);
});
```

 
## Try it out
Use Postman as you did in Hol3. You can start by inserting the whole collection:
```js
[
    {id:1, name:"Twix", price:2.9},
    {id:2, name:"Snickers", price:2.5},
    {id:3, name:"Daim", price:3.2}
]
```

## Optional
Update your unit test to work with the new data. Don't forget to update the require statement at the top to use *hol5.js*
