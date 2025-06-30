Here is the complete MongoDB query list for all CRUD operations — Create, Read, Update, and Delete — including various use cases like filtering, updating with conditions, projections, and logical operators.

📘 MongoDB Complete CRUD Query List
🔸 C - CREATE
🔹 Insert a single document
db.products.insertOne({ name: "Shirt", price: 499, category: "men's clothing" });
🔹 Insert multiple documents
db.products.insertMany([
  { name: "Jeans", price: 999, category: "men's clothing" },
  { name: "Dress", price: 799, category: "women's clothing" }
]);
🔸 R - READ
🔹 Get all documents
db.products.find();
🔹 Get documents with a condition
db.products.find({ price: 499 });         // exact match
db.products.find({ category: "books" });  // match by category
🔹 Comparison operators
db.products.find({ price: { $gt: 500 } });    // price > 500
db.products.find({ price: { $gte: 500 } });   // price >= 500
db.products.find({ price: { $lt: 1000 } });   // price < 1000
db.products.find({ price: { $lte: 1000 } });  // price <= 1000
db.products.find({ price: { $ne: 999 } });    // price != 999
🔹 Logical operators
db.products.find({
  $and: [
    { price: { $gt: 500 } },
    { category: "men's clothing" }
  ]
});

db.products.find({
  $or: [
    { price: { $lt: 500 } },
    { category: "books" }
  ]
});

db.products.find({
  price: { $not: { $gte: 1000 } }  // price < 1000
});
🔹 Projection (return specific fields)
db.products.find({}, { name: 1, price: 1, _id: 0 });
🔹 Limit and Sort
db.products.find().limit(5);                      // Limit to 5 results
db.products.find().sort({ price: 1 });            // Sort ascending
db.products.find().sort({ price: -1 });           // Sort descending
🔸 U - UPDATE
🔹 Update one document
db.products.updateOne(
  { name: "Shirt" },
  { $set: { price: 599 } }
);
🔹 Update many documents
db.products.updateMany(
  { category: "men's clothing" },
  { $set: { discount: true } }
);
🔹 Replace a document
db.products.replaceOne(
  { name: "Shirt" },
  { name: "T-Shirt", price: 499, category: "men's clothing" }
);
🔹 Increment/Decrement a value
db.products.updateOne(
  { name: "Shirt" },
  { $inc: { price: 100 } }     // increase price by 100
);
🔹 Update using $unset (remove field)
db.products.updateOne(
  { name: "Shirt" },
  { $unset: { discount: "" } }
);
🔸 D - DELETE
🔹 Delete one document
db.products.deleteOne({ name: "Shirt" });
🔹 Delete many documents
db.products.deleteMany({ category: "expired" });
🔸 Extra: Count, Exists, etc.
🔹 Count documents
db.products.countDocuments();                          // total count
db.products.countDocuments({ category: "books" });     // count with condition
🔹 Check if a field exists
db.products.find({ discount: { $exists: true } });
🔸 Create Collection & Drop
🔹 Create collection manually
db.createCollection("products");
🔹 Drop a collection
db.products.drop();
🔹 Drop a database
use mydb;
db.dropDatabase();
✅ Pro Tips
Always back up before deleting or updating many documents.
Use .explain("executionStats") for performance analysis.
Index fields you frequently search/sort on using:
db.products.createIndex({ price: 1 });
