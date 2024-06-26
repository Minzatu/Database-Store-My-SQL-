# Database Project for **Store**#

The scope of this project is to use all the SQL knowledge gained throught the Software Testing course and apply them in practice.

Database Created: **Store**

Tools used: MySQL Workbench

## Database description:
<li>**Customers** - details about personal data of customers;</li>
<li>**Items** -details about the products  name,quantity in stock and price per unit ; </li>
<li>**Shippers** - details about the courier companies;</li>
<li>**Order_statuses**-details about the statuses of the order;</li>
<li>**My_store** - contains the relationship between products id and order id ;</li>
<li>**Order_items** contains details about the products: quantity and prices;</li>
<li>**Orders** is more of a summary that incorporate information about customers,courier companies and more datailed information about orders;</li>

 The scope is to obtain information related to customers and their orders, in order for the process to take place without problems and delays . 
 Accesing this databases  I can assure that everything goes as planned without  any delays involved. 


## Database Schema

 You can find below the database schema that was generated through Reverse Engineer and which contains all the tables and the relationships between them.

The tables are connected in the following way:

<li>**Customers** is connected with **Orders** through a **parent** relationship which was implemented through **Customers.id** as a primary key and **id_customer** as a foreign key</li>
<li>**Items** is connected with **Order_itmes** through a **parent** relationship which was implemented through **Itmes.id** as a primary key and **.id_product_** as a foreign key</li>
<li>**Items** is connected with **My store** through a **parent** relationship which was implemented through **Items.id** as a primary key and **.id_product_** as a foreign key</li>
<li>**My store** is connected with **Orders** through a **child** relationship which was implemented through **Orders.id** as a primary key and **.id_order_** as a foreign key </li>
<li>**Shipper** is connected with **Orders** through a **parent** relationship which was implemented through **Shipper.id** as a primary key and **.id_shipper_** as a foreign key</li> 
<li>**Shipper** is connected with **Orders** through a **parent** relationship which was implemented through **Shipper.id** as a primary key and **.id_shipper_** as a foreign key</li> 
<li>**Order_statuses** is connected with **Orders** through a **parent** relationship which was implemented through **order_statuses.id** as a primary key and **.id_order_status_** as a foreign key</li>

## Database Queries:


### DDL (Data Definition Language)

The following instructions were written in the scope of CREATING the structure of the database (CREATE INSTRUCTIONS)

 ```
CREATE DATABASE store ;
USE store;
```

```
CREATE TABLE products (
 Id int  primary key auto_increment,
   name varchar(50) NOT NULL,
  quantity_in_stock  int NOT NULL,
  unit_price int not null);
```

```
CREATE TABLE shippers (
 id  int primary key auto_increment,
  name varchar(50) NOT NULL);
```
  
```CREATE TABLE customers (
  id int primary key auto_increment,
  first_name  varchar(50) NOT NULL,
  last_name varchar(50) NOT NULL,
  birth_date  date DEFAULT NULL,
  phone  varchar(50)  NULL,
  address  varchar(50) NOT NULL,
  city  varchar(50) NOT NULL,
  state char(2) NOT NULL);
```
  
```
CREATE TABLE order_statuses (order_statuses,
order_statuses
id int primary key auto_increment,
name varchar(50) NOT NULL);
```

```
CREATE TABLE orders (
     id  int primary key auto_increment,
     id_customer  int ,
     id_shipper int ,
     order_status int,
     order_date date NOT NULL,
     shipped_date date,
	foreign key(id_customer) references customers(id),
	foreign key(id_shipper) references shippers(id),
	foreign key(id_order_status) references order_statuses(id));
```
	
```
CREATE TABLE order_items (
  id int primary key auto_increment,
  id_product  int,
  quantity int NOT NULL,
  unit_price int  NOT NULL,
  foreign key (id_product) references products(id));
```
 
```
CREATE TABLE My_store (
id int primary key auto_increment,
id_order int,
id_product int,
foreign key(id_order) references orders(id),
foreign key(id_product) references products(id));
```
```
Create table failed_orders(
id int, 
order_id int, 
comments varchar (2000));
```


<p>After the database and the tables have been created, a few ALTER instructions were written in order to update the structure of the database, as described below:</p> 

**Change the name of the column** 
 ```
 alter table order_items change unit_price total_price int;
```
 **Change the properties of one column** 
 ```
 alter table customers modify column city varchar ( 25);
```
**Change the name of the tables**
 ```
 rename table products to items;
 rename table items to products;
```
**Delete a column  from the  table**
```
alter table customers drop column country;
```
**Adding column properties (adding auto-increment)**
```
alter table failed_orders add primary key(id);
```


 ### DML (Data Manipulation Language)
 
In order to be able to use the database I populated the tables with various data necessary in order to perform queries and manipulate the data. 
In the testing process, this necessary data is identified in the Test Design phase and created in the Test Implementation phase. 

**Below you can find all the insert instructions that were created in the scope of this project:**

``` 
insert into items (id,name, quantity_in_stock,unit_price) values 
(1,'notebook',35,13),
(2,'pencils',100, 5),
(3,'color books',250,10),
(4,'white pages',1500,1),
(5,'blue pen Stabilus',250,15),
(6,'red pen Stabilus',350,16),
(7,'sparkler pencils',354,6);
```

```
insert into shippers(name) values
('Sameday'),
('Fancourier'),
('Cargus');
```

```
INSERT INTO  customers (first_name ,last_name ,birth_date ,phone, address, city ,state) VALUES
 ('Laura','Popescu','1986-03-28','0721965979','10 Ovidiu','Brasov','BV'),
 ('Ines','Cismas','1986-04-13','07321564987','141 Piata clujului','Cluj napoca','CJ'),
 ('Freddi','Kruger','1985-02-07','07654987123','251 Piata Unirii','Moinesti','BC'),
 ('Alin','Mihalache','1974-04-14','0745659798','30 calea bucuresti','Brasov ','BV'),
 ('Mara ','Ionescu','1973-11-07','0745789123','5 Aurel Vlaicu','Poiana Marului','BV'),
('Elsa','Mirica','1991-09-04','0745897546','7 grigore antipa','Fagaras','BV'),
 ('Ileana','Dumitrache','1964-08-30','0745789456','50 1 Decembrie','Timisoara','TM'),
 ('Romina','Popescu','1993-07-17','0712654789','538 Mosinee Center','Sf Gheoghe ','CV'),
 ('Romola','Mirica','1992-05-23','0721321654','35 Mircea cel batran','Sf Gheorghe','CV'),
('Liana','Minzatu','1969-10-13','0745789123','489 Grivitei','Brasov ','BV');
```

```
insert into order_statuses (name ) values
('Processed'),
('Shipped'),
('Delivered');
```

```
insert into orders ( Id_customer,id_shipper,id_order_status,order_date,shipped_date) values 
(1,3,2,'2024-05-12','2024-05-16'),
(3,2,1,'2024-06-01','2024-06-03'),
(5,3,2,'2024-06-02','2024-06-12'),
(5,1,3,'2024-05-15','2024-05-26'),
(6,2,3,'2024-06-24','2024-06-27'),
(7,1,2,'2024-06-16','2024-06-23'),
(8,2,3,'2024-07-04','2024-07-05'),
(9,3,3,'2024-05-12','2024-05-18' );
```

```
insert into order_items(id_product,quantity, unit_price ) values 
(1,10,123),
(3,2,10),
(4,1000,1000),
(6,70,1120),
(7,20,120),
(2,25,50),
(5,45,675);
```

```
insert into  my_store (id_order,id_product) values
(81,5),
(85,4),
(82,6),
(86,1),
(88,3),
(87,7),
(86,5);
```

```
insert into failed_orders(order_id, comments) values 
(1,'problems related to the transport'),
(2,'refused payment');
```

After the insert, in order to prepare the data to be better suited for the testing process, I updated some data in the following way:

```
update table orders set processing_time = 4 where id=81;
update table orders set processing_time = 2 where id=82; 
update customers set country ='Romania'where id =2;
```


 ### DQL (Data Query Language)

<p>After the testing process, I deleted the data that was no longer relevant and the tables that will no longer be used in order to preserve the database clean:</p>

```
delete from customers where id=2; 
alter table customers drop column country;
truncate failed_orders; 
drop table failed_orders;
```

<p>In order to simulate various scenarios that might happen in real life I created the following queries that would cover multiple potential real-life situations:</p>

**Where**<br>
```
select *from customers  where city='Brasov';
```

**Order By**<br>
_ordering the products according to increasing price_

```
select*from order_items order by total_price asc;
```

_top 3 items with highest quantity in stock_
```
select*from order_items order by quantity limit 3;
```

**AND**
```
select *from orders where extract(year from order_date) = 2024 and status='Canceled';
```

**OR**<br>
```
select *from customers where city='Brasov'or city='Cluj napoca ';
```

**NOT**<br>
```
select * from orders where not order_status = 'Cancelled';
```

**Like**<br>
```
select *from items where  name like 'S%';
select *from items where  name like '%r';
select *from items where  name like '%u%';
select *from items where  name like '_t%';
```

**Inner join**<br>
_We want to extract all the customer who have orders ongoing_
```
select first_name,last_name,order_date, order_status
from orders o
inner join customers c
on o.id_customer=c.customers.id
where order_status not in ("Shipped","Cancelled","Delivered")
```

_I want to find out the client id, the order id and the id of the ordered product_
```
select id_order,id_product,id_customer
from my_store m
inner join orders o on o.id= m.id_order;
```

_I want to group the name of the product with the price per unit and the price per order_
```
select oi.order_id, p.name, price*quantity as total_price
from products p
join order_items oi on p.id=oi.id_product;

```

**Left join**<br>
_I want to select all the customer who did not perform any order_

```
select first_name,last_name,city, id_customer
from customers c
left join orders o on c.id = o.id_customer
where o.id_customer is null;
```

  
**Right join**<br>
_Select all the failed orders_

```
select id_order, comment
from failed_orders fo
right join orders  o on fo.id_order = o.id
where fo.id_order is not null
```

_The grouping of courier companies according to the city, where the delivery will take place_
```
select c.city, s.name, c.first_name, c.last_name, o.order_id 
from shippers s
right join orders o on o.shipper_id = s.id
right_join customers c on o.id_customer=c.id
```
   
**Aggregate functions**<br>


_Profit manipulation for market research_
```
select Max(total_price) from order_items;
select Min(total_price) from order_items; 
select avg(total_price) from order_items; 
select sum(total_price) from order_items; 
```

**Group by**<br>

_Grouping orders according to status_
```
select id_order_status, count(id)
from orders
group by id_order_status;
```

_Obtaining a sales profit ranking_
```
select extract(month from order_date) as order_month, sum(p.price * oi.quantity) as total_price
from products p
inner join orders on o.product_id = p.id
inner join order_items oi on o.order_id = oi.order_id
group by order_month
order by total_price desc;
```

_Finding the customers, depending on city_
```
select city, count(id)
from customers group by city;
```

**Having + Subqueries**<br>

_Performing a ranking of the orders according to the total value > 999 and the largest quantity ordered_
```

select o.order_id, max(oi.quantity) where order_id in
(
select o.order_id, sum(p.price * oi.quantity) as total_price
from products p
inner join orders on o.product_id = p.id
inner join order_items oi on o.order_id = oi.order_id
having total_price >999
);
```

_I want to find the product with the largest quantity in stock_
```
select name
from products where quantity_in_stock = (select max(quantity_in_stock) from products);
```


<h2>Conclusions</h2>

From this lesson I learned to create, modify, insert and manipulate information in databases. I am aware that there is a long way to go to fully understand all these tasks, but practice makes it better. 
I can query this database and find out the information necessary to pick up and send an order, thus avoiding irregularities, which could affect the quality of the service. Quality starts primarily from the accuracy and correctness of the information and its use for our benefit.
Through the various scenarios, I was able to find out exactly the delivery address, who will deliver, when and at what stage the order is.  
I can manage my stock of products, the price per piece and make a profit analysis. 
This skill will help me avoid making mistakes and manually testing an app/page
