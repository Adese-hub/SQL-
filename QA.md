What are your risk areas? Identify and describe them.

Missing Values 
Repeated Unique values 
Redundanct info

QA Process:
Describe your QA process and include the SQL queries used to execute it.
Dropping columns 
Filtering the table using "where"
Select *
FROM all_sessions

ALTER TABLE all_sessions
DROP COLUMN totaltransactionrevenue,
DROP COLUMN transactions,
DROP COLUMN productrefundamount,
DROP COLUMN productquantity,
DROP COLUMN productvariant;

SELECT *
FROM all_sessions
WHERE timeonsite IS NULL;

