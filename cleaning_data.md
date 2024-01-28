What issues will you address by cleaning the data?

Lack of unique columns in some tables 
Loading problem 
Missing and irrelevant Columns: 

productRefundAmount
productQuantity
productPrice
productRevenue
    
Queries:

ALTER TABLE all_sessions
DROP COLUMN productRefundAmount,
DROP COLUMN	productQuantity,
DROP COLUMN productPrice,
DROP COLUMN productRevenue;


Below, provide the SQL queries you used to clean your data.

CREATE TEMPORARY TABLE temp_table AS
SELECT 	
	sales_by_sku.total_ordered,  sales_by_sku. , all_sessions.visitid 
FROM 
    all_sessions
LEFT JOIN 
   sales_by_sku ON all_sessions.productsku = sales_by_sku.productsku
WHERE total_ordered > 0;




