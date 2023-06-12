## make a database in this current path.

sudo mongod --dbpath ~/

----
## open mongodb

mongosh

----
## create a database / get access to database.

use database_name

----
## insert a message into the "messages" collection

db.messages.insertOne({text: "This is our first test message"})

----
##

show collections

----
##

db.dropDatabase()

----
## (equivilent of select * from PRODUCTS)

db.products.find()

----
## filters:

$lt <
$lte <=
$gt >
$gte >=
$eq ==
$ne !=

## return products in the hardware category which has a price equal to 200.00

db.products.find({category: "Hardware", price: {$eq: 200.00}})

----
## Delete all documents in the products category: (no parameters specified)

db.products.deleteMany()

----
## Delete all products with the name coffee mug. 

db.products.deleteMany({name: "Coffee mug"})

----
## Update all products that have the parameter category: "clothes" to the set price of 29.99

db.products.updateMany(
    {category: "Clothes"},
    {$set: { price: 29.99}}
)

----
## 