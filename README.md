<span style="color:#6495ED; font-size:24px; font-weight:bold;">Mint Classics Data Insights & Warehouse Optimization using SQL</span> <br>
<span style="color:#6495ED; font-size:20px; font-weight:bold;">Author: Linh Khanh Nguyen (Kolor)</span>

--

## Table of contents
1. [Introduction](#introduction)
2. [SQL queries](#meth)
3. [Result Discussions](#section3)
4. [Summary](#summary)

## Introduction  <a name="introduction"></a>

The main goal of this project is to analyze data with the goal of supporting inventory-related business decisions of the fictional Mint Classics Company using SQL. 

## SQL queries <a name="meth"></a>

Here is some code that I used to develop the analysis. 
 
```sql
SELECT
    p.productcode,
    p.productname,
    p.quantityinstock,
    (SELECT COUNT(*) FROM orderdetails od WHERE p.productcode = od.productcode) AS order_count
FROM
    products p
HAVING
    order_count = 0;
```
Result

![](pics/Screenshot 2023-09-18 at 10.37.54 PM.png)
<br><br>

```sql
SELECT
    p.productline,
    SUM(p.quantityinstock) AS total_inventory,
    w.warehousecode,
    w.warehousename,
    w.warehousepctcap
FROM
    products p
JOIN
    warehouses w ON p.warehousecode = w.warehousecode
GROUP BY
    p.productline, w.warehousecode, w.warehousename, w.warehousepctcap
ORDER BY
    total_inventory DESC;
```
Result

![](pics/Screenshot 2023-09-18 at 11.00.37 PM.png)
<br><br>

```sql
SELECT
    YEAR(o.orderdate) AS sales_year,
    MONTH(o.orderdate) AS sales_month,
    COUNT(o.ordernumber) AS total_orders,
    SUM(od.quantityordered) AS total_quantity_ordered,
    SUM(od.quantityordered * od.priceeach) AS total_sales
FROM
    orders o
JOIN
    orderdetails od ON o.ordernumber = od.ordernumber
GROUP BY
    sales_year, sales_month
ORDER BY
    sales_year, sales_month;
```
Result

![](pics/Screenshot 2023-09-18 at 11.14.54 PM.png)
<br><br>

```sql
SELECT
    p.productline,
    COUNT(*) AS total_products,
    SUM(p.quantityinstock) AS total_inventory,
    AVG(p.buyprice) AS avg_buyprice,
    AVG(p.MSRP) AS avg_msrp
FROM
    products p
GROUP BY
    p.productline
ORDER BY
    total_inventory DESC;
```
Result

![](pics/Screenshot 2023-09-18 at 11.27.00 PM.png)
<br><br>

```sql
SELECT
    YEAR(paymentdate) AS payment_year,
    MONTH(paymentdate) AS payment_month,
    COUNT(*) AS total_payments,
    SUM(amount) AS total_amount
FROM
    payments
GROUP BY
    payment_year, payment_month
ORDER BY
    payment_year, payment_month;
```
Result

![](pics/Screenshot 2023-09-18 at 11.48.37 PM.png)
<br><br>

-- Calculate the capacity utilization for each warehouse
```sql
SELECT
    w.warehousecode,
    w.warehousename,
    w.warehousepctcap,
    SUM(p.quantityinstock) AS total_quantity_in_stock
FROM
    warehouses w
JOIN
    products p ON w.warehousecode = p.warehousecode
GROUP BY
    w.warehousecode, w.warehousename, w.warehousepctcap;
```
Result

![](pics/Screenshot 2023-09-19 at 12.14.38 AM.png)
<br><br>

-- Scenario 1: Check if any warehouse has capacity utilization below 70%
```sql
SELECT
    warehousecode,
    warehousename,
    warehousepctcap,
    total_quantity_in_stock
FROM
    (SELECT
        w.warehousecode,
        w.warehousename,
        w.warehousepctcap,
        SUM(p.quantityinstock) AS total_quantity_in_stock
    FROM
        warehouses w
    JOIN
        products p ON w.warehousecode = p.warehousecode
    GROUP BY
        w.warehousecode, w.warehousename, w.warehousepctcap) AS warehouse_utilization
WHERE
    warehousepctcap < 70;
```
Result

![](pics/Screenshot 2023-09-19 at 5.49.40 PM.png)
<br><br>

-- Scenario 2: Check if any warehouse has capacity utilization above 90%
```sql
SELECT
    warehousecode,
    warehousename,
    warehousepctcap,
    total_quantity_in_stock
FROM
    (SELECT
        w.warehousecode,
        w.warehousename,
        w.warehousepctcap,
        SUM(p.quantityinstock) AS total_quantity_in_stock
    FROM
        warehouses w
    JOIN
        products p ON w.warehousecode = p.warehousecode
    GROUP BY
        w.warehousecode, w.warehousename, w.warehousepctcap) AS warehouse_utilization
WHERE
    warehousepctcap > 90;
```
Result

![](pics/Screenshot 2023-09-19 at 6.00.42 PM.png)
<br><br>

## Result Discussion <a name="section3"></a>
First, the analysis identified products that have not been ordered, which is 1985 Toyota Supra. Based on this, Mint Classics should decide to promote it, offer discounts, or even consider discontinuing it if it is still not generating any demand.

Secondly, the analysis showed that the classic car product line has the highest inventory level, while the train product line has the lowest inventory level. It also showed which warehouse each product line is stored at, and the percentage capacity of each warehouse. This information can help the business understand whether certain warehouses are close to their storage limits. Thus, all of the information can be crucial for logistics and optimizing stock distribution. Product lines with high inventory levels (classic car and vintage car) are stored at warehouses that still have a lot of capacity left, while product lines with lower inventory levels are stored at warehouses with lower capacity remaining. The analysis further consolidates that classic car and vintage car product lines have the most number of total products, which suggests these product lines are the most popular and have diversity in their product offerings. The fact that these product lines have high inventory levels shows that Mint Classics can ensure that products are readily available to meet customer demand. This can lead to improved customer satisfaction and loyalty. The warehouses that store inventories of these two product lines also have higher capacity left than other warehouses, indicating that Mint Classics' warehouses operate efficiently and are not overburdened.





## Summary <a name="summary"></a>

Blah blah

## More 

To view the GitHub repo for this website, click [here](https://github.com/WilliamRoth82/BozandtheBozzers).
