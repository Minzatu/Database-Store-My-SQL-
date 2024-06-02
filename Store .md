# Database Project for **Store**#

The scope of this project is to use all the SQL knowledge gained throught the Software Testing course and apply them in practice.

Application under test: **Store**

Tools used: MySQL Workbench

### Database description:###
<li>**Customers** - details about personal data of customers;</li>
<li>**Items** -details about the products  name,quantity in stock and price per unit ; </li>
<li>**Shippers** - details about the courier companies;</li>
<li>**Order_statuses**-details about the statuses of the order;</li>
<li>**My_store** - contains the relationship between products id and order id ;</li>
<li>**Order_items** contains details about the products: quantity and prices;</li>
<li>**Orders** is more of a summary that incorporate information about customers,courier companies and more datailed information about orders;</li>

 The scope is to obtain information related to customers and their orders, in order for the process to take place without problems and delays . 
 Accesing this databases  I can assure that everything goes as planned without  any delays involved. 


***Database Schema***

 You can find below the database schema that was generated through Reverse Engineer and which contains all the tables and the relationships between them.

The tables are connected in the following way:

<li>**Customers** is connected with **Orders** through a **parent** relationship which was implemented through **Customers.id** as a primary key and **id_customer** as a foreign key</li>
<li>**Items** is connected with **Order_itmes** through a **parent** relationship which was implemented through **Itmes.id** as a primary key and **.id_product_** as a foreign key</li>
<li>**Items** is connected with **My store** through a **parent** relationship which was implemented through **Items.id** as a primary key and **.id_product_** as a foreign key</li>
<li>**My store** is connected with **Orders** through a **child** relationship which was implemented through **Orders.id** as a primary key and **.id_order_** as a foreign key </li>
<li>**Shipper** is connected with **Orders** through a **parent** relationship which was implemented through **Shipper.id** as a primary key and **.id_shipper_** as a foreign key</li> 
<li>**Shipper** is connected with **Orders** through a **parent** relationship which was implemented through **Shipper.id** as a primary key and **.id_shipper_** as a foreign key</li> 
<li>**Order_statuses** is connected with **Orders** through a **parent** relationship which was implemented through **order_statuses.id** as a primary key and **.id_order_status_** as a foreign key</li>

## Database Queries##


## DDL (Data Definition Language)##

  The following instructions were written in the scope of CREATING the structure of the database (CREATE INSTRUCTIONS)

 <li>**CREATE DATABASE store ;
        USE store;</li> 

<li><strong>CREATE TABLE products</strong> (
 Id int  primary key auto_increment,
   name varchar(50) NOT NULL,
  quantity_in_stock  int NOT NULL,
  unit_price int not null); </li>

<li>CREATE TABLE shippers (
 id  int primary key auto_increment,
  name varchar(50) NOT NULL); </li>
  
  
<li>CREATE TABLE customers (
  id int primary key auto_increment,
  first_name  varchar(50) NOT NULL,
  last_name varchar(50) NOT NULL,
  birth_date  date DEFAULT NULL,
  phone  varchar(50)  NULL,
  address  varchar(50) NOT NULL,
  city  varchar(50) NOT NULL,
  state char(2) NOT NULL); </li>
  

<li>CREATE TABLE order_statuses (order_statusesorder_statuses
id int primary key auto_increment,
name varchar(50) NOT NULL); </li>

<li>CREATE TABLE orders (
     id  int primary key auto_increment,
     id_customer  int ,
 id_shipper int ,
     id_order_status int,
	 order_date date NOT NULL,
	shipped_date date  ,
	foreign key(id_customer) references customers(id),
	foreign key(id_shipper) references shippers(id),
	foreign key(id_order_status) references order_statuses(id)); </li>
	
<li>CREATE TABLE order_items (
  id int primary key auto_increment,
  id_product  int,
  quantity int NOT NULL,
  unit_price int  NOT NULL,
  foreign key (id_product) references products(id)); </li>
 

<li>CREATE TABLE My_store(
id int primary key auto_increment,
id_order int,
id_product int,
foreign key(id_order) references orders(id),
foreign key(id_product) references products(id)); </li>

<li> Create table failed_orders(
id int, 
order_id int, 
comments varchar (2000)); </li>


 <p>After the database and the tables have been created, a few ALTER instructions were written in order to update the structure of the database, as described below:</p> 

 ** Change the name of the column  ** 
 <li>alter table order_items change unit_price total_price int;</li> 
 **- change the properties of one column** 
 <li> alter table customers modify column city varchar ( 25); </li> 
**- change the name of the tables**
 <li> rename table products to items;
      rename table items to products; </li>
**- delete a column  from the  table  **
<li>alter table customers drop column country; </li>
** adding column properties (adding auto-increment)
<li>alter table failed_orders add primary key(id);</li>


 
  
  <li>DML (Data Manipulation Language)</li>

  In order to be able to use the database I populated the tables with various data necessary in order to perform queries and manipulate the data. 
  In the testing process, this necessary data is identified in the Test Design phase and created in the Test Implementation phase. 

   **Below you can find all the insert instructions that were created in the scope of this project: **

 
<li> insert into items (id,name, quantity_in_stock,unit_price) values 
(1,'notebook',35,13),
(2,'pencils',100, 5),
(3,'color books',250,10),
(4,'white pages',1500,1),
(5,'blue pen Stabilus',250,15),
(6,'red pen Stabilus',350,16),
(7,'sparkler pencils',354,6); </li>

<li> insert into shippers(name) values
('Sameday'),
('Fancourier'),
('Cargus'); </li>

<li> INSERT INTO  customers (first_name ,last_name ,birth_date ,phone, address, city ,state) VALUES
 ('Laura','Popescu','1986-03-28','0721965979','10 Ovidiu','Brasov','BV'),
 ('Ines','Cismas','1986-04-13','07321564987','141 Piata clujului','Cluj napoca','CJ'),
 ('Freddi','Kruger','1985-02-07','07654987123','251 Piata Unirii','Moinesti','BC'),
 ('Alin','Mihalache','1974-04-14','0745659798','30 calea bucuresti','Brasov ','BV'),
 ('Mara ','Ionescu','1973-11-07','0745789123','5 Aurel Vlaicu','Poiana Marului','BV'),
('Elsa','Mirica','1991-09-04','0745897546','7 grigore antipa','Fagaras','BV'),
 ('Ileana','Dumitrache','1964-08-30','0745789456','50 1 Decembrie','Timisoara','TM'),
 ('Romina','Popescu','1993-07-17','0712654789','538 Mosinee Center','Sf Gheoghe ','CV'),
 ('Romola','Mirica','1992-05-23','0721321654','35 Mircea cel batran','Sf Gheorghe','CV'),
('Liana','Minzatu','1969-10-13','0745789123','489 Grivitei','Brasov ','BV'); </li>

<li> insert into order_statuses (name ) values
('Processed'),
('Shipped'),
('Delivered'); </li>


<li> insert into orders ( Id_customer,id_shipper,id_order_status,order_date,shipped_date) values 
(1,3,2,'2024-05-12','2024-05-16'),
(3,2,1,'2024-06-01','2024-06-03'),
(5,3,2,'2024-06-02','2024-06-12'),
(5,1,3,'2024-05-15','2024-05-26'),
(6,2,3,'2024-06-24','2024-06-27'),
(7,1,2,'2024-06-16','2024-06-23'),
(8,2,3,'2024-07-04','2024-07-05'),
(9,3,3,'2024-05-12','2024-05-18' ); </li>


<li> insert into order_items(id_product,quantity, unit_price ) values 
(1,10,123),
(3,2,10),
(4,1000,1000),
(6,70,1120),
(7,20,120),
(2,25,50),
(5,45,675); </li>

<li> insert into  my_store (id_order,id_product) values
(81,5),
(85,4),
(82,6),
(86,1),
(88,3),
(87,7),
(86,5); </li>
<li> insert into failed_orders(order_id, comments) values 
(1,'problems related to the transport '),
(2,'refused payment'); </li>
  After the insert, in order to prepare the data to be better suited for the testing process, I updated some data in the following way:

  ** update table orders set processing_time = 4 where id=81;
      update table orders set processing_time = 2 where id=82; 
          update customers set country ='Romania'where id =2;**


  <h2>DQL (Data Query Language)</h2>

After the testing process, I deleted the data that was no longer relevant in order to preserve the database clean: 

<li> delete from customers where id=2; </li>
<li> alter table customers drop column country; </li>
<li>truncate failed_orders; </li>
<li>drop table failed_orders; </li>


<h2>Data Manipulation Language </h2>


In order to simulate various scenarios that might happen in real life I created the following queries that would cover multiple potential real-life situations:

**-<strong> where</strong>**<br>
<li> select *from customers  where city='Brasov'; </li>

**-<strong> ORDER BY</strong>**<br>
**-ordering the products according to increasing price**
<li>select*from order_items order by total_price asc; </li>
**-<strong>top 3 items with highest quantity in stock</strong>**
<li> select*from order_items order by quantity limit 3;</li>

**-<strong>AND</strong><br>
<li> select *from customers where city='Brasov'and city='cluj napoca'; </li>

**- <strong>OR</strong>**<br>
<li> select *from customers where city='Brasov'or city='cluj napoca '; </li>

**-<strong>NOT</strong> **<br>
<li> select *from customers where not city='Brasov'and city='cluj'; </li>

**- <strong>like</strong>**<br>
<li> select *from items where  name  like 'S%'; </li>
<li> select *from items where  name like '%r'; </li>
<li> select *from items where  name like '%u%'; </li>
<li> select *from items where  name like '_t%'; </li> 

**-<strong>inner join</strong> **<br>
**-I want to know the name and surname of the customers and the date of the order**
<li>select first_name,last_name,order_date from orders inner join customers on orders.id_customer=customers.id;</li>
**-<strong>I want to find out the client id, the order id and the id of the ordered product**</strong> 
<li>select id_order,id_product,id_customer from my_store inner join orders on orders.id= my_store.id_order;</li>
**- <strong>I want to group the name of the product with the price per unit and the price per order;</strong>**
<li> select name,unit_price,total_price  from items join 
  order_items on items.id=order_items.id_product;</li>

**-<strong>left join</strong> **<br>
<li>  select first_name,last_name,city, id_customer from customers left join orders on customers.id = orders.id-id_customer;</li>

  
**- right join**<br>
**-assignment of products with the quantity in stock**
<li> select name, quantity from order_items right join items on order_items.id_product=items.id;</li>
**<strong> -the grouping of courier companies according to the city, where the delivery will take place</strong>**
<li> select city, id_shipper from customers right join orders on orders.id_customer=customers.id;</li>

**- <strong>cross join</strong>**<br>
<li> select city, id_shipper from customers cross join orders ;</li>
   <li>select name, quantity from order_items cross join items ;</li>
   
**<strong>-aggregate functions</strong> **<br>
**-obtaining a sales profit ranking**
<li> select*from order_items order by total_price desc;</li>

**<strong>profit manipulation for market research</strong>
<li> select Max(total_price) from order_items; </li>
<li> select Min(total_price) from order_items; </li>
 <li> select avg(total_price) from order_items; </li>
<li> select sum(total_price) from order_items; </li>

**- <strong>group by</strong>**<br>
**-grouping orders according to status**
<li> select id_order_status, count(id) from orders group by id_order_status; </li>
**<strong>-finding the customers, depending on city ;</strong>**
<li> select city, count(id) from customers group by city ; </li>

**-<strong>having</strong> **<br>
** <strong>performing a ranking of the orders according to the price > 999 and the largest quantity ordered;</strong> **
<li> select id, max(total_price) from order_items group by id having max(total_price)>999; </li>

select*from customers;
**- Subqueries **<br>
**- I want to find the product with the largest quantity in stock;**
<li>select name from items where quantity_in_stock=(select max(quantity_in_stock) from items);</li>


</ol>

<h2>Conclusions</h2>

** From this lesson I learned to create, modify, insert and manipulate information in databases. I am aware that there is a long way to go to fully understand all these tasks, but practice makes it better. 
I can query this database and find out the information necessary to pick up and send an order, thus avoiding irregularities, which could affect the quality of the service. Quality starts primarily from the accuracy and correctness of the information and its use for our benefit.
Through the various scenarios, I was able to find out exactly the delivery address, who will deliver, when and at what stage the order is.  
I can manage my stock of products, the price per piece and make a profit analysis. 
This skill will help me avoid making mistakes and manually testing an app/page  **

</ol>
