````markdown
# PLP Bookstore MongoDB Scripts

This repository contains MongoDB scripts for managing the PLP Bookstore database. The scripts include queries for finding, sorting, updating, and aggregating books.

## Prerequisites

- MongoDB installed on your machine or access to a MongoDB server.
- `mongosh` (MongoDB Shell) for running commands interactively or scripts.
- Basic knowledge of MongoDB queries and aggregation pipelines.

## How to Run the Scripts

1. **Start MongoDB server** if it’s not already running:
   ```bash
   mongod
````

2. **Open MongoDB shell (`mongosh`)**:

   ```bash
   mongosh
   ```

3. **Switch to the bookstore database:**

   ```js
   use plp_bookstore
   ```

4. **Run queries or scripts:**

   * To find books in a specific genre:

     ```js
     db.books.find({ genre: "fiction" }).pretty()
     ```

   * To find books in stock published after 2010 with specific fields:

     ```js
     db.books.find(
       { in_stock: true, publish_year: { $gt: 2010 } },
       { title: 1, author: 1, price: 1 }
     ).pretty()
     ```

   * To sort books by price ascending:

     ```js
     db.books.find().sort({ price: 1 }).pretty()
     ```

   * To paginate results (5 books per page):

     ```js
     // Page 1
     db.books.find().limit(5).pretty()

     // Page 2
     db.books.find().skip(5).limit(5).pretty()
     ```

   * To run aggregation pipelines (example: average price by genre):

     ```js
     db.books.aggregate([
       {
         $group: {
           _id: "$genre",
           average_price: { $avg: "$price" }
         }
       }
     ])
     ```

5. **Creating indexes for performance:**

   * Create index on title:

     ```js
     db.books.createIndex({ title: 1 })
     ```

   * Create compound index on author and published\_year:

     ```js
     db.books.createIndex({ author: 1, published_year: 1 })
     ```

6. **Checking query performance with explain():**

   ```js
   db.books.find({ title: "Animal Farm" }).explain("executionStats")
   ```

## Notes

* Replace queries with your own filters as needed.

---

