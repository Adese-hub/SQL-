Question 1: Find the total number of unique visitors (fullVisitorID) 

SQL Queries:
SELECT Count(DISTINCT fullvisitorid)
FROM all_sessions; 

Answer: 
14223

Question 2: 
Find the total number of unique visitors by referring sites 

SQL Queries:
SELECT Count(DISTINCT visitid)
FROM all_sessions; 

Answer:
14218

Question 3: Percentage of visitors that made a purchase

SQL Queries:
CREATE TEMPORARY TABLE temp_table AS
SELECT 	
	sales_by_sku.total_ordered,  sales_by_sku.productsku, all_sessions.visitid 
FROM 
    all_sessions
LEFT JOIN 
   sales_by_sku ON all_sessions.productsku = sales_by_sku.productsku
WHERE total_ordered > 0;

SELECT 	
(COUNT(DISTINCT all_sessions.visitid) / COUNT(DISTINCT temp_table.visitid)) * 100 AS purchase_percentage
FROM all_sessions

SELECT 
    (NULLIF(COUNT(DISTINCT all_sessions.visitid) / 
	COUNT(DISTINCT temp_table.visitid), 0)) 
	 * 100 AS purchase_percentage
FROM 
    all_sessions
LEFT JOIN 
    temp_table ON all_sessions.visitid = temp_table.visitid;


(SELECT 
    COUNT(DISTINCT all_sessions.visitid)
FROM 
   all_sessions
   
SELECT 
    COUNT(DISTINCT temp_table.visitid)
	
FROM 
   temp_table) Calculate Percentage Manually

Answer:50.18%


Question 4: What is the correlation between the time spent on the site and the number of order made 

SQL Queries:
SELECT 
    CORR(all_sessions.timeOnSite, sales_by_sku.total_ordered) AS correlation
FROM
    all_sessions
JOIN
    sales_by_sku ON all_sessions.productsku = sales_by_sku.productsku;

Answer: 0.004848956355494319


Question 5: What is the correlation between the orderedquantity, stocklevel, restockingleadtime the site and the number of order made 

SELECT 
    CORR(orderedquantity, stocklevel) AS corr_ordered_stock,
    CORR(orderedquantity, restockingleadtime) AS corr_ordered_restocking,
    CORR(stocklevel, restockingleadtime) AS corr_stock_restocking
FROM
    Products;
    
SQL Queries:

Answer: corr_ordered_stock	corr_ordered_restocking	corr_stock_restocking
0.7649998305900740	-0.05557791783120930	-0.034898420049630400<img width="357" alt="image" src="https://github.com/Adese-hub/SQL-/assets/148140542/f3e131d9-6b43-47a9-8df7-ce9c4daba590">

