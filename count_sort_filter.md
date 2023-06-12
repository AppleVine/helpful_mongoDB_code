
## Count the amount of products:

db.products.count()

----
## Count the number of products with the category "clothes"

db.products.countDocuments({category: "Clothes"})

----
## Return all categories within products.

db.products.distinct("category")

----
## Return all categories within products that have a price greater than 25.

db.products.distinct("category", {price: {$gt: 25}})

----
## Group products by category, then provide the sum of their prices.

db.products.aggregate( [
   // Group documents by category and calculate total price of their products
   {
      $group: { _id: "$category", totalPrice: { $sum: "$price" } }
   }
] )

----
## $match: filter for products with prices greater than 25, then group the remaining documents by price and calculate the average per category. 

db.products.aggregate( [
   // Filter products by price with $match
   {
      $match: { price: { $gt: 25} }
   },
   // Group remaining documents by price and calculate average price grouped by category
   {
      $group: { _id: "$category", avgPrice: { $avg: "$price" } }
   }
] )

----
## Same step before, but sort the products by average price in descending order (-1). 

db.products.aggregate( [
   // Filter products by price with $match
   {
        $match: { price: { $gt: 25} }
   },
   // Group remaining documents by price and calculate average price grouped by category
   {
        $group: { _id: "$category", avgPrice: { $avg: "$price" } }
   },
   {
       $sort: { avgPrice: -1 }
   }
] )

----