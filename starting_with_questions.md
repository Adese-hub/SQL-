Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:
Select *
From all_sessions 
JOIN sales_by_sku 
ON all_sessions.productSKU = sales_by_sku.productSKU; 

SELECT all_sessions.city, all_sessions.country, sales_by_sku.productSKU, all_session.unit_price * sales_by_sku.total_ordered AS total_price
FROM (Select * 
From all_sessions 
JOIN sales_by_sku 
ON all_sessions.productSKU = sales_by_sku.productSKU)AS joined; 

—--------------------------

SELECT 
    all_sessions.city, 
    all_sessions.country, 
    all_sessions.productSKU, 
    all_sessions.productprice * sales_by_sku.total_ordered AS total_revenue
FROM 
    all_sessions 
JOIN 
    sales_by_sku 
ON 
    all_sessions.productSKU = sales_by_sku.productSKU;

Answer: United States - Mountain View 

**Question 2: What is the average number of products ordered from visitors in each city and country?**

SQL Queries:
SELECT 
    all_sessions.city, 
    all_sessions.country, 
    all_sessions.productSKU, 
    AVG(products.orderedquantity) AS AVG_Quant
FROM 
    all_sessions 
JOIN 
    products 
ON 
    all_sessions.productSKU = products.sku
GROUP BY 
    all_sessions.city, 
    all_sessions.country, 
    all_sessions.productSKU;

Answer:

**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**

SQL Queries:

SELECT 
    all_sessions.city, 
    all_sessions.country, 
    all_sessions.productSKU, 
    COUNT(products.orderedquantity) 
FROM 
    all_sessions 
JOIN 
    products 
ON 
    all_sessions.productSKU = products.sku
GROUP BY 
    all_sessions.city, 
    all_sessions.country, 
    all_sessions.productSKU,
	products.orderedquantity
ORDER BY products.orderedquantity desc;
—---------------------------------------------

SELECT 
    all_sessions.country, 
    all_sessions.productSKU, 
    COUNT(products.orderedquantity) AS ProductQ,
    COUNT(all_sessions.productSKU) AS ProdC
FROM 
    all_sessions 
JOIN 
    products 
ON 
    all_sessions.productSKU = products.sku
GROUP BY 
    all_sessions.country, 
    all_sessions.productSKU
ORDER BY 
    ProductQ DESC;

—------------------------------

SELECT 
    TRIM(UPPER(all_sessions.country)) AS Country, 
    SUM(products.orderedquantity) AS TotalOrderedQuantity
FROM 
    all_sessions 
JOIN 
    products 
ON 
    all_sessions.productSKU = products.sku
GROUP BY 
    TRIM(UPPER(all_sessions.country))
ORDER BY 
    TotalOrderedQuantity DESC;


Answer:
"UNITED STATES"	3700334
"UNITED KINGDOM"	323996
"INDIA"	301860
"CANADA"	270109
"GERMANY"	142467
"JAPAN"	113214
"TAIWAN"	109558
"AUSTRALIA"	103347
"ITALY"	89205


**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

SELECT
    CASE WHEN city = 'not available in demo dataset' THEN Country ELSE city END AS corrected_city,
    Country,
    productsku,
    v2productname,
    v2productcategory,
    COUNT(*) AS product_count
FROM
    all_sessions
GROUP BY
    CASE WHEN city = 'not available in demo dataset' THEN Country ELSE city END,
    Country,
    productsku,
    v2productname,
    v2productcategory
HAVING
    COUNT(*) > 5
ORDER BY
    product_count DESC,
    corrected_city,  -- Use the corrected_city alias in the ORDER BY clause
    Country; 

Answer: United States - Google Kick Ball

**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:
SELECT
    CASE WHEN city = 'not available in demo dataset' THEN Country ELSE city END AS corrected_city,
    Country,
    all_sessions.productsku,
    v2productname,
    v2productcategory,
    COUNT(*) AS product_count,
    (all_sessions.productprice * sales_by_sku.total_ordered) AS ProductRevenue
FROM
    all_sessions
JOIN
    sales_by_sku ON all_sessions.productsku = sales_by_sku.productsku
GROUP BY
    CASE WHEN city = 'not available in demo dataset' THEN Country ELSE city END,  -- Use the original expression
    Country,
    all_sessions.productsku,
    v2productname,
    v2productcategory,
	(all_sessions.productprice * sales_by_sku.total_ordered)
HAVING
    COUNT(*) > 5
ORDER BY
    productrevenue DESC,
	product_count,
    corrected_city,  
    Country;

Answer:

corrected_city	country	productsku	v2productname	v2productcategory	product_count	productrevenue
Mountain View	United States	GGOENEBJ079499	Nest® Learning Thermostat 3rd Gen-USA - Stainless Steel	Home/Nest/Nest-USA/	6	23406000000
United States	United States	GGOENEBJ079499	Nest® Learning Thermostat 3rd Gen-USA - Stainless Steel	Home/Nest/Nest-USA/	9	23406000000
United States	United States	GGOENEBQ078999	Nest® Cam Outdoor Security Camera - USA	Home/Nest/Nest-USA/	10	22288000000<img width="895" alt="image" src="https://github.com/Adese-hub/SQL-/assets/148140542/22770822-4643-44a2-8981-196cf8b2312a">








