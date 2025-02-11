<!-- Problem 2: Online Store Inventory and Orders System -->

CREATE TABLE products (
	product_id SERIAL PRIMARY KEY,
	product_name VARCHAR(50) NOT NULL,
	price INT,
	stock_quantity INT
);

CREATE TABLE customers (
	customer_id SERIAL PRIMARY KEY,
	first_name VARCHAR(50) NOT NULL,
  last_name VARCHAR(50) NOT NULL,
  email VARCHAR(100) UNIQUE NOT NULL
);

CREATE TABLE orders (
	order_id SERIAL PRIMARY KEY,
	customer_id INT,
	order_date DATE,
	FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);

CREATE TABLE order_items (
	order_id INT,
	product_id INT,
	quantity INT,
	FOREIGN KEY (order_id) REFERENCES orders(order_id),
	FOREIGN KEY (product_id) REFERENCES products(product_id),
	PRIMARY KEY (order_id, product_id)
)

INSERT INTO products (product_name, price, stock_quantity)
VALUES ('Shoes', 98, 1),
       ('Apples', 2, 144),
       ('Guns', 400, 20),
       ('Bigger shoes', 99, 2),
       ('Beta fish', 30, 13),
       ('Pools', 1200, 7000);

INSERT INTO customers (first_name, last_name, email)
VALUES ('Albert', 'Bumbleford', 'xxxsniper420xx@hotmail.com'),
   		 ('Bob', 'Burgerstone', 'no@why.com'),
		   ('Cathy', 'Cathy', 'cathysquared@google.com'),
		   ('Donald', 'Donk', 'e@mail.com');

INSERT INTO orders (customer_id, order_date)
VALUES (1, '2025-01-10'),
       (2, '2026-06-11'),
       (3, '2020-03-02'),
       (4, '1025-12-23'),
       (1, '2025-02-14');

INSERT INTO order_items (order_id, product_id, quantity)
VALUES	(1, 1, 1),  
  		  (1, 3, 2),
		    (2, 2, 10),
		    (2, 5, 2),
        (3, 2, 1000),
        (3, 4, 10),
        (3, 5, 999),
        (4, 1, 1),
		    (4, 6, 10);

SELECT product_name, stock_quantity FROM products

SELECT products.product_name, order_items.quantity 
FROM order_items
JOIN products ON products.product_id = order_items.product_id
WHERE order_items.order_id = 3;

SELECT orders.order_id, order_items.product_id, order_items.quantity
FROM orders
JOIN order_items ON orders.order_id = order_items.order_id
WHERE orders.customer_id = 1

<!-- Below is simulating Donald(id = 4) buying (order_id = 4) 1 shoes and 10 pools -->
UPDATE products
SET stock_quantity = products.stock_quantity - order_items.quantity
FROM order_items 
WHERE products.product_id = order_items.product_id
AND order_items.order_id = 4


DELETE FROM order_items
WHERE order_id = 1

DELETE FROM orders
WHERE order_id = 1