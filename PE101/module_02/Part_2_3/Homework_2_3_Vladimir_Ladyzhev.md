# 2.3. Подключение к базам данных SQL. Практика.

### 1. Установка Postgres - сделано.
### 2. Создание базы данных Sales superstore. Сделано. Ниже приведет фрагмент кода.
>drop table if exists orders;
>CREATE TABLE orders(
   Row_ID        INTEGER  NOT NULL PRIMARY KEY 
  ,Order_ID      VARCHAR(14) NOT NULL
  ,Order_Date    DATE  NOT NULL
  ,Ship_Date     DATE  NOT NULL
  ,Ship_Mode     VARCHAR(14) NOT NULL
  ,Customer_ID   VARCHAR(8) NOT NULL
  ,Customer_Name VARCHAR(22) NOT NULL
  ,Segment       VARCHAR(11) NOT NULL
  ,Country       VARCHAR(13) NOT NULL
  ,City          VARCHAR(17) NOT NULL
  ,State         VARCHAR(20) NOT NULL
  ,Postal_Code   INTEGER 
  ,Region        VARCHAR(7) NOT NULL
  ,Product_ID    VARCHAR(15) NOT NULL
  ,Category      VARCHAR(15) NOT NULL
  ,SubCategory   VARCHAR(11) NOT NULL
  ,Product_Name  VARCHAR(127) NOT NULL
  ,Sales         NUMERIC(9,4) NOT NULL
  ,Quantity      INTEGER  NOT NULL
  ,Discount      NUMERIC(4,2) NOT NULL
  ,Profit        NUMERIC(21,16) NOT NULL
);
>set datestyle to 'ISO, MDY';
>INSERT INTO orders(Row_ID,Order_ID,Order_Date,Ship_Date,Ship_Mode,Customer_ID,Customer_Name,Segment,Country,City,State,Postal_Code,Region,Product_ID,Category,SubCategory,Product_Name,Sales,Quantity,Discount,Profit) VALUES (1,'CA-2018-152156','11/08/2018','11/11/2018','Second Class','CG-12520','Claire Gute','Consumer','United States','Henderson','Kentucky',42420,'South','FUR-BO-10001798','Furniture','Bookcases','Bush Somerset Collection Bookcase',261.96,2,0,41.9136);
>INSERT INTO orders(Row_ID,Order_ID,Order_Date,Ship_Date,Ship_Mode,Customer_ID,Customer_Name,Segment,Country,City,State,Postal_Code,Region,Product_ID,Category,SubCategory,Product_Name,Sales,Quantity,Discount,Profit) VALUES (2,'CA-2018-152156','11/08/2018','11/11/2018','Second Class','CG-12520','Claire Gute','Consumer','United States','Henderson','Kentucky',42420,'South','FUR-CH-10000454','Furniture','Chairs','Hon Deluxe Fabric Upholstered Stacking Chairs, Rounded Back',731.94,3,0,219.582);
>INSERT INTO orders(Row_ID,Order_ID,Order_Date,Ship_Date,Ship_Mode,Customer_ID,Customer_Name,Segment,Country,City,State,Postal_Code,Region,Product_ID,Category,SubCategory,Product_Name,Sales,Quantity,Discount,Profit) VALUES (3,'CA-2018-138688','06/12/2018','06/16/2018','Second Class','DV-13045','Darrin Van Huff','Corporate','United States','Los Angeles','California',90036,'West','OFF-LA-10000240','Office Supplies','Labels','Self-Adhesive Address Labels for Typewriters by Universal',14.62,2,0,6.8714);

### 3. Запросы на вопросы из модуля 1.

>>""Вычисление total sales""

>>select sum(sales) as total_sales from orders;

>>""Вычисление total profit""

>>select sum(profit) as total_profit from orders;

>>""Вычисление profit ratio""

>>select round(sum(profit)/sum(sales), 2) as profit_ratio from orders;

>>""Определить profit per order""

>>select order_id, sum(profit) as order_profit from orders o
group by order_id
limit 20;

>>""Вычислить Sales per customer""

>>select customer_id, sum(sales) as customer_sales from orders o
group by customer_id
limit 20;

>>""Вычислить average discount""

>>select round(avg(discount)*100, 2) as "average_discount_%" from orders;

>>""Вычислить Monthly sales by segment""

>>select extract (month from order_date) as month,
extract (year from order_date) as year,
segment, sum(sales) as revenue 
from orders
group by month, year, segment
order by year, month, segment;

>>""Вычислить Monthly sales by product category""

>>select extract (month from order_date) as month,
extract (year from order_date) as year,
category, sum(sales) as revenue 
from orders
group by month, year, category
order by year, month, category;

>>""Sales and profit by customer""

>>select customer_id, sum(sales) as revenue, sum(profit) as total_profit
from orders o 
group by customer_id
order by revenue DESC
limit 20;

>>""Sales per region""
>select region, sum(sales) as revenue, sum(profit) as total_profit
from orders o 
group by region
order by revenue DESC;

