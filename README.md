<span style="color:lightblue; font-size:24px; font-weight:bold;">Linh Khanh Nguyen (Kolor)</span> <br>
<span style="color:lightblue; font-size:24px; font-weight:bold;">Data Science Project</span>

--

## Table of contents
1. [Introduction](#introduction)
2. [Methodology](#meth)
3. [Section 2](#section2)
    1. [Subsection](#subsec2-1)
    2. [Subsection](#subsec2-2)
4. [Analysis Section](#section3)
5. [Summary](#summary)

## Introduction  <a name="introduction"></a>

The main goal of this project is to analyze data with the goal of supporting inventory-related business decisions of the fictional Mint Classics Company using SQL. 

## Methodology <a name="meth"></a>

Here is some code that we used to develop our analysis. 
 
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

## Section <a name="section2"></a>
Blah blah

### Subsection 1 <a name="subsec2-1"></a>
This is a subsection, formatted in heading 3 style

### Subsection 2 <a name="subsec2-2"></a>
This is a subsection, formatted in heading 3 style

## Analysis Section <a name="section3"></a>

Here are some graphs that we created in our analysis. We saved them to the `pics/` subfolder and include them via the usual markdown syntax for pictures.

![](pics/plot1.png)
<br><br>
Some analysis here
<br><br>
![](pics/plot2.png)
<br><br>
More analysis here.
<br><br>
![](pics/plot3.png)
<br><br>
More analysis.

## Summary <a name="summary"></a>

Blah blah

## More 

To view the GitHub repo for this website, click [here](https://github.com/WilliamRoth82/BozandtheBozzers).
