# Myntra Product & Database Dissection

## 📌 Project Overview

This project explores the **product, database, and analytics architecture of a large-scale fashion e-commerce platform using Myntra as a real-world reference**.

The project focuses on understanding how a structured relational database can support key e-commerce operations such as:

* Product catalog management
* User and address management
* Shopping carts and wishlists
* Order processing
* Inventory management
* Payments
* Shipments
* Reviews and ratings
* Business and product analytics

The project combines **database design concepts with practical SQL analytics** to demonstrate how structured data can support business decision-making.

---

## 🏢 Company Overview

Myntra is an Indian fashion and lifestyle e-commerce platform founded in 2007 and acquired by Flipkart in 2014.

The platform connects users, brands, and sellers through an online shopping ecosystem covering categories such as:

* Clothing
* Footwear
* Accessories
* Beauty Products

From a data perspective, a large e-commerce platform requires structured systems for managing products, customers, orders, inventory, payments, and user interactions.

> **Note:** This project is an educational database modeling and analytics exercise based on publicly observable e-commerce workflows. It does not represent Myntra's actual internal database architecture.

---

## 🎯 Project Objectives

The main objectives of this project are to:

1. Understand the database structure required for an e-commerce platform.
2. Identify important entities and their attributes.
3. Model relationships between different entities.
4. Understand one-to-many and many-to-many relationships.
5. Apply primary and foreign key concepts.
6. Design SQL queries for common business questions.
7. Connect database design with product and business insights.

---

## 🧩 Core Platform Features

The database model covers major e-commerce components:

| Feature           | Purpose                                           |
| ----------------- | ------------------------------------------------- |
| User Accounts     | Stores customer information and purchase history  |
| Product Catalog   | Manages products, brands, categories, and pricing |
| Shopping Cart     | Tracks products users intend to purchase          |
| Secure Payments   | Records payment methods and transaction status    |
| Reviews & Ratings | Captures customer feedback                        |
| Wishlist          | Tracks products users are interested in           |
| Inventory         | Maintains product stock information               |
| Orders            | Stores customer purchases and order information   |
| Shipments         | Supports delivery and logistics tracking          |

---

## 🗄️ Key Entities

The proposed database model contains the following major entities:

* **Users**
* **UserAddresses**
* **Brands**
* **Categories**
* **Products**
* **ProductImages**
* **Inventory**
* **Carts**
* **CartItems**
* **Orders**
* **OrderItems**
* **Payments**
* **Shipments**
* **Reviews**
* **Wishlist**

These entities represent the major data components required to support an e-commerce workflow.

---

## 🔗 Database Relationships

### One-to-Many Relationships

Examples include:

```text
Users → Orders
Orders → OrderItems
Products → Inventory
Products → Reviews
Brands → Products
Categories → Products
```

### Many-to-Many Relationships

Many-to-many relationships are handled using junction tables.

```text
Orders ↔ Products
       ↓
   OrderItems
```

```text
Carts ↔ Products
       ↓
    CartItems
```

### Hierarchical Relationship

Categories can be organized using a parent-child structure:

```text
Categories
    ↓
Parent Category
    ↓
Subcategory
```

Foreign keys help maintain relationships and data integrity between related tables.

---

## 💻 SQL & Analytics

The project focuses on practical SQL questions that could be useful for e-commerce analytics.

### 1. Top-Selling Products

```sql
SELECT 
    p.product_name,
    SUM(oi.quantity) AS total_sold
FROM order_items oi
JOIN products p 
    ON oi.product_id = p.product_id
JOIN orders o 
    ON oi.order_id = o.order_id
WHERE o.order_date >= '2026-02-01'
GROUP BY p.product_name
ORDER BY total_sold DESC
LIMIT 10;
```

**Business Use:**
Helps identify products with high sales volume for merchandising and inventory planning.

---

### 2. Users With Items in Cart

```sql
SELECT 
    u.user_id,
    u.name,
    COUNT(ci.cart_item_id) AS items_in_cart
FROM users u
JOIN cart c 
    ON u.user_id = c.user_id
JOIN cart_items ci 
    ON c.cart_id = ci.cart_id
WHERE c.created_at >= NOW() - INTERVAL '7 days'
GROUP BY u.user_id, u.name
HAVING COUNT(ci.cart_item_id) > 0;
```

**Business Use:**
Can support analysis of shopping intent and potential cart abandonment.

---

### 3. Average Rating by Brand

```sql
SELECT 
    b.brand_name,
    AVG(r.rating) AS avg_rating
FROM brands b
JOIN products p 
    ON b.brand_id = p.brand_id
JOIN reviews r 
    ON p.product_id = r.product_id
GROUP BY b.brand_name
ORDER BY avg_rating DESC;
```

**Business Use:**
Provides a way to analyze customer feedback at the brand level.

---

## 📊 Business & Product Insights

A well-structured e-commerce database can support analysis in several areas:

### Revenue Optimization

Analyze product sales, purchasing patterns, and sales trends.

### Inventory Management

Monitor stock levels and identify products that may require replenishment.

### Customer Engagement

Analyze carts, wishlists, reviews, and purchase history.

### Product Strategy

Compare product and brand performance across categories and price ranges.

### Operational Analytics

Use structured order, payment, shipment, and inventory data to analyze operational performance.

---

## 🛠️ Skills & Concepts Demonstrated

### SQL

* SELECT
* WHERE
* JOIN
* GROUP BY
* HAVING
* ORDER BY
* Aggregate Functions
* Date Filtering
* Subqueries / analytical querying

### Database Concepts

* Primary Keys
* Foreign Keys
* Relational Integrity
* One-to-Many Relationships
* Many-to-Many Relationships
* Junction Tables
* Hierarchical Data Modeling
* Entity-Relationship Modeling

### Business Analytics

* Product Performance
* Sales Analysis
* Customer Behavior
* Inventory Analysis
* Brand Performance
* E-commerce Metrics

---

## 📁 Project Structure

```text
Myntra-Product-Database-Dissection/
│
├── README.md
├── SQL/
│   └── myntra_analysis.sql
│
├── ER_Diagram/
│   └── myntra_er_diagram.png
│
└── Documentation/
    └── project_documentation.pdf
```

*Update the folder names above to match the actual files in your repository.*

---

## 🎓 Key Takeaways

This project demonstrates how **relational database design and SQL analytics can support an e-commerce platform**.

The main learning outcomes include:

* Designing entities around real-world business processes.
* Understanding relationships between customers, products, orders, and inventory.
* Using junction tables to model many-to-many relationships.
* Maintaining data integrity through primary and foreign keys.
* Writing SQL queries to answer practical business questions.
* Translating database information into product and business insights.

---

## 🚀 Future Improvements

Potential extensions to this project include:

* Building the complete database using PostgreSQL/MySQL.
* Creating an ER diagram with all relationships.
* Adding sample datasets.
* Writing advanced SQL queries using CTEs and window functions.
* Creating an e-commerce analytics dashboard using Power BI or Tableau.
* Adding customer segmentation and product recommendation analysis.
* Developing ML models for demand forecasting or customer behavior prediction.

---

## 👨‍💻 Author

**Ganesh Vedpathak**

This project was created as part of a practical learning portfolio focused on **SQL, database design, data analytics, and data science**.
