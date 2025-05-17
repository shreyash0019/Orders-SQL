# E-commerce Orders SQL

This repository contains a SQL script for managing e-commerce orders. The script creates tables for customers, products, orders, and order items, and includes sample data inserts.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Schema](#schema)
  - [Customers Table](#customers-table)
  - [Products Table](#products-table)
  - [Orders Table](#orders-table)
  - [Order Items Table](#order-items-table)
- [Sample Data](#sample-data)
- [License](#license)

## Installation

To set up the database, you need to have a SQL database management system like MySQL or PostgreSQL installed. Then, you can use a database client or command line to run the SQL script.

1. Clone the repository:
    ```bash
    git clone https://github.com/<your-username>/ecommerce-orders-sql.git
    cd ecommerce-orders-sql
    ```

2. Open the SQL script `orders.sql` in your database client or command line interface and execute it to create the tables and insert sample data.

## Usage

The SQL script `orders.sql` contains the necessary commands to create and populate the following tables:

- `customers`: Stores customer information.
- `products`: Stores product information.
- `orders`: Stores order information.
- `order_items`: Stores details of the items in each order.

You can modify the script to suit your needs or use it as a starting point for your own e-commerce database schema.

## Schema

### Customers Table

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100) UNIQUE,
    phone VARCHAR(15),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

- `customer_id`: Unique identifier for each customer.
- `first_name`: Customer's first name.
- `last_name`: Customer's last name.
- `email`: Customer's email address (unique).
- `phone`: Customer's phone number.
- `created_at`: Timestamp of when the customer record was created.

### Products Table

```sql
CREATE TABLE products (
    product_id INT PRIMARY KEY AUTO_INCREMENT,
    product_name VARCHAR(100),
    description TEXT,
    price DECIMAL(10, 2),
    stock_quantity INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

- `product_id`: Unique identifier for each product.
- `product_name`: Name of the product.
- `description`: Description of the product.
- `price`: Price of the product.
- `stock_quantity`: Quantity of the product in stock.
- `created_at`: Timestamp of when the product record was created.

### Orders Table

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY AUTO_INCREMENT,
    customer_id INT,
    order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    status VARCHAR(20),
    total_amount DECIMAL(10, 2),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);
```

- `order_id`: Unique identifier for each order.
- `customer_id`: Identifier for the customer who placed the order.
- `order_date`: Timestamp of when the order was placed.
- `status`: Status of the order (e.g., Pending, Completed).
- `total_amount`: Total amount for the order.
- Foreign key constraint to link `customer_id` to the `customers` table.

### Order Items Table

```sql
CREATE TABLE order_items (
    order_item_id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT,
    product_id INT,
    quantity INT,
    price DECIMAL(10, 2),
    FOREIGN KEY (order_id) REFERENCES orders(order_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);
```

- `order_item_id`: Unique identifier for each order item.
- `order_id`: Identifier for the order this item belongs to.
- `product_id`: Identifier for the product.
- `quantity`: Quantity of the product ordered.
- `price`: Price of the product at the time of the order.
- Foreign key constraints to link `order_id` to the `orders` table and `product_id` to the `products` table.

## Sample Data

The script includes sample data inserts for the `customers`, `products`, `orders`, and `order_items` tables. This data can be used to test the database schema and perform queries.

```sql
-- Insert sample data into customers table
INSERT INTO customers (first_name, last_name, email, phone) VALUES
('John', 'Doe', 'john.doe@example.com', '123-456-7890'),
('Jane', 'Smith', 'jane.smith@example.com', '987-654-3210');

-- Insert sample data into products table
INSERT INTO products (product_name, description, price, stock_quantity) VALUES
('Laptop', 'A high-performance laptop', 999.99, 10),
('Smartphone', 'A latest model smartphone', 699.99, 20);

-- Insert sample data into orders table
INSERT INTO orders (customer_id, status, total_amount) VALUES
(1, 'Pending', 999.99),
(2, 'Completed', 699.99);

-- Insert sample data into order_items table
INSERT INTO order_items (order_id, product_id, quantity, price) VALUES
(1, 1, 1, 999.99),
(2, 2, 1, 699.99);
```


