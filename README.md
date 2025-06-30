# 📘 MongoDB CRUD Operations – Quick Reference

This guide provides commonly used MongoDB queries for performing **CRUD** operations and helpful utilities.

---

## 🔸 Create – `C`

### ➤ Insert a Single Document

```js
db.products.insertOne({ name: "Shirt", price: 499, category: "men's clothing" });
```

### ➤ Insert Multiple Documents

```js
db.products.insertMany([
  { name: "Jeans", price: 999, category: "men's clothing" },
  { name: "Dress", price: 799, category: "women's clothing" }
]);
```

---

## 🔹 Read – `R`

### ➤ Get All Documents

```js
db.products.find();
```

### ➤ Conditional Reads

```js
db.products.find({ price: 499 });                  // Exact match  
db.products.find({ category: "books" });           // Match by category  
db.products.find({ price: { $gt: 500 } });         // price > 500  
db.products.find({ price: { $gte: 500 } });        // price ≥ 500  
db.products.find({ price: { $lt: 1000 } });        // price < 1000  
db.products.find({ price: { $lte: 1000 } });       // price ≤ 1000  
db.products.find({ price: { $ne: 999 } });         // price ≠ 999  
```

### ➤ Logical Queries

```js
// AND
db.products.find({
  $and: [
    { price: { $gt: 500 } },
    { category: "men's clothing" }
  ]
});

// OR
db.products.find({
  $or: [
    { price: { $lt: 500 } },
    { category: "books" }
  ]
});

// NOT
db.products.find({
  price: { $not: { $gte: 1000 } }
});
```

### ➤ Projection (Select Fields)

```js
db.products.find({}, { name: 1, price: 1, _id: 0 });
```

### ➤ Limit and Sort

```js
db.products.find().limit(5);              // Limit results to 5
db.products.find().sort({ price: 1 });    // Sort ascending
db.products.find().sort({ price: -1 });   // Sort descending
```

---

## 🔸 Update – `U`

### ➤ Update One Document

```js
db.products.updateOne(
  { name: "Shirt" },
  { $set: { price: 599 } }
);
```

### ➤ Update Multiple Documents

```js
db.products.updateMany(
  { category: "men's clothing" },
  { $set: { discount: true } }
);
```

### ➤ Replace Entire Document

```js
db.products.replaceOne(
  { name: "Shirt" },
  { name: "T-Shirt", price: 499, category: "men's clothing" }
);
```

### ➤ Increment / Decrement Value

```js
db.products.updateOne(
  { name: "Shirt" },
  { $inc: { price: 100 } }
);
```

### ➤ Remove a Field

```js
db.products.updateOne(
  { name: "Shirt" },
  { $unset: { discount: "" } }
);
```

---

## 🔸 Delete – `D`

### ➤ Delete One Document

```js
db.products.deleteOne({ name: "Shirt" });
```

### ➤ Delete Many Documents

```js
db.products.deleteMany({ category: "expired" });
```

---

## 🔸 Extras

### ➤ Count Documents

```js
db.products.countDocuments();                           // Total
db.products.countDocuments({ category: "books" });      // Conditional
```

### ➤ Check If Field Exists

```js
db.products.find({ discount: { $exists: true } });
```

---

## 🔸 Collections and Database

### ➤ Create a Collection

```js
db.createCollection("products");
```

### ➤ Drop a Collection

```js
db.products.drop();
```

### ➤ Drop a Database

```js
use mydb;
db.dropDatabase();
```

---

## ✅ Pro Tips

* **Backup** before performing bulk deletes or updates.
* Use `.explain("executionStats")` to analyze query performance.
* **Index** frequently queried or sorted fields:

  ```js
  db.products.createIndex({ price: 1 });
  ```


