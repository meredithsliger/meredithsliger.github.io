---
layout: default
title: NoSQL & Big Data
---

## ☁️ NoSQL & Big Data

This section highlights modern approaches to data storage and processing, including document-oriented databases like MongoDB and the larger Hadoop ecosystem that supports scalable, flexible Big Data architecture.

---

### 📦 NoSQL Overview

**NoSQL** stands for “Not Only SQL” — systems designed for non-relational data storage that prioritize scalability, flexibility, and performance over strict schema design. NoSQL systems are ideal for:

- Schema-less or semi-structured data
- High-throughput and horizontally scalable workloads
- Cloud-native, distributed systems

#### 💡 NoSQL Characteristics
- **Schema-on-read** flexibility
- **Not ACID compliant** – instead, BASE: Basically Available, Soft state, Eventually consistent
- **Horizontal scaling (scale out)** rather than vertical scaling (scale up)
- Naturally suited for **cloud environments**

---

### 🗂️ NoSQL Types

- **Key-Value Stores** – Simple key-to-value mappings.  
  _Example:_ `session:abc123` → `{userId: 54, loggedIn: true}` in Redis

- **Document Stores** – JSON-like documents with flexible fields.  
  _Example:_
  ```json
  {
    "_id": "p123",
    "name": "Coconut Water",
    "category": "Beverage",
    "nutrients": {"calories": 45, "sugar": "9g"}
  }
  ```

- **Columnar Databases** – Column-family structure used for efficient writes.  
  _Example:_ In Cassandra, a `sales_by_region` table stores region-wise sales as columns with monthly aggregates.

- **Graph Databases** – Nodes and edges with properties to model relationships.  
  _Example:_ Users and their connections in a social network:
  ```
  (User:Alice)-[:FOLLOWS]->(User:Bob)
  (User:Bob)-[:LIKES]->(Post:Post42)
  ```

---

### 🌐 MongoDB Practice

This section highlights applied work using MongoDB and a `patron` collection within a `fact` database. Tasks included inserting, updating, and querying JSON-like documents.

- **Inserting a new student patron:**
  ```js
  db.patron.insertOne({
    display: "Rachel Cunningham",
    fname: "rachel",
    lname: "cunningham",
    type: "student",
    age: 24
  });
  ```

- **Updating a student with book checkouts:**
  ```js
  db.patron.updateOne(
    { display: "Rachel Cunningham" },
    { $set: {
        checkouts: [
          {
            id: "95000",
            year: 2018,
            month: 1,
            day: 25,
            book: "5237",
            title: "Mastering the database environment",
            pubyear: 2015,
            subject: "database"
          },
          {
            id: "95001",
            year: 2018,
            month: 1,
            day: 25,
            book: "5240",
            title: "iOS Programming",
            pubyear: 2015,
            subject: "programming"
          }
        ]
      }
    }
  );
  ```

- **Querying student patrons who checked out a cloud-related book:**
  ```js
  db.patron.find(
    {
      type: "student",
      checkouts: { $elemMatch: { subject: "cloud" } }
    },
    {
      _id: 1,
      display: 1,
      age: 1
    }
  );
  ```

- **Faculty who checked out programming books:**
  ```js
  db.patron.find(
    {
      type: "faculty",
      checkouts: { $elemMatch: { subject: "programming" } }
    },
    {
      fname: 1,
      lname: 1,
      type: 1,
      _id: 0
    }
  );
  ```

- **Complex OR condition with age filter:**
  ```js
  db.patron.find(
    {
      $or: [
        { type: "faculty", checkouts: { $elemMatch: { book: "5235" } } },
        { type: "student", age: { $lt: 30 }, checkouts: { $elemMatch: { book: "5240" } } }
      ]
    }
  ).pretty();
  ```

- **Students aged 22–26:**
  ```js
  db.patron.find(
    { type: "student", age: { $gte: 22, $lte: 26 } },
    { fname: 1, lname: 1, age: 1, _id: 0 }
  );
  ```

### 🏗️ Big Data Fundamentals

**Big Data** refers to datasets characterized by:
- **Volume** – E.g., millions of ride records per day from a ride-sharing app
- **Velocity** – E.g., real-time location updates from delivery drivers
- **Variety** – E.g., GPS logs, customer reviews, profile pictures

Other key traits include:
- **Veracity** – Ensuring tweet sentiment data is not manipulated
- **Value** – Turning clickstream logs into targeted ad recommendations
- **Variability** – A hashtag may mean different things in different contexts
- **Visualization** – Using dashboards to show daily demand by city

---

### ⚙️ Hadoop Ecosystem (Simplified)

- **HDFS** – Breaks files into blocks and distributes across nodes
- **MapReduce** – Processes logs to compute average delivery time by zip code
- **Hive** – SQL-like queries on top of HDFS data
- **HBase** – Columnar store for storing user click history
- **Kafka** – Stream processor for ingesting user events in real-time

This ecosystem powers the infrastructure for scalable big data analytics, often found in large tech and e-commerce firms.

---

This page showcases experience with flexible database models and introduces the building blocks of Big Data environments used in cloud-scale analytics.
