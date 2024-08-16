# This includes 

## SELECT -
1. select * from table_1
2. select col_1 from table_1
3. select col_1, col_2 from table_1

## DISTINCT - operates on column to find the distinct/unique values
eg: 

| 	Name | 	coloe	  
| 	:-----:	 | 	:-----:	 | 
|   Zach	|	Green
|    David	|	Green
|   Claire	|	Yellow
|   David	|	Red

1. Select Distinct (Name) from table_1 -> Zach, David, Claire
2. Select Distinct (color) from table_2 -> Green, Yellow, Red

eg: we have multiple movie rating associations like, IMDB, RT etc
Find the number of rating orgs available?
Sol : Select Distinct (rating_orgs) from table_1

## COUNT - 
1. Select count(Name) from film - 4
2. Select count(color) from film - 4
3. Select count(*) from film - 4
4. Select count(Distinct Name) from film - 3


## WHERE - 
* WHERE clause appears immediately after FROM clause(FROM xyz WHERE pqr)
* operations that can be used =, >, <, <=, >=, AND, OR, NOT
1. Select name, color from table_1 WHERE name="David"
2. Select name, color from table_1 WHERE name="David" AND color="Green"

## ORDER BY - 
* Always put ORDER BY towards the end
* use ASC to ascending order and DESC for descending order
* Select col_1, col_2 from table_1 ORDER BY col_2 ASC
1. Select * from table_1 ORDER BY col_1 ASC, col_2 DESC - first sorts the table in col_1 ascending order and if two col1 has same values then sorts based on col2 


## LIMIT - 
* limits the output to certain number of instances only
1. Select * from table_1 ORDER BY sales LIMIT 3 - gives 3 least records with sales
2. Select * from table_1 ORDER BY sales DESC LIMIT 3 - gives 3 records with highest sales
  

## BETWEEN - 
* use with WHERE clause
1. Select * from table_1 WHERE amount BETWEEN 8 AND 9 - gives the result from 8 to 8.9999 (9 is excluded)
2. Select * from table_1 WHERE amount NOT BETWEEN 8 AND 9 - gives the results other than 8 and 9

## IN - 
* use with WHERE clause
1. Select * from table_1 WHERE name IN('Google','Amazon') - displays all the records whose has name as Google and Amazon
2. Select * from table_1 WHERE name NOT IN('Google','Microsoft') - displays all the other records except the records whose names are Google and Microsoft

## LIKE and ILIKE
* get all the records whose email ends with '@gmail.com' OR 
* get all the records whose names starts with 'Ani'
* % used for sequence of characters 
* _ used for single character

1. Select name where name LIKE 'A%' - names that starts with A
2. Select name where name LIKE '%A' - names that ends with A

ILIKE is case insensitive, Like is case sensitive 
eg: customers whose first name starts with A and last name ends with s
1. Select name Where first_name LIke 'A%' and last_name LIKE 'S%' - returns all the firstname thats starts with A and lastname with S
2. Select name where first_name ILIKE 'a%' and last_name ILIKE 's%' - returns all the firstname that starts with A/a and lastname s/s



## GROUP BY -
1. Aggregate functions - AVG(), COUNT(), MAX(), MIN(), SUM()
eg: orders table

| Order_id  |   Product_id   |  Product_name     |  Product_price    |
|   :-----: |   :-----:      |      :-----:      |      :-----:      |
|    1     |      3     |     apple    |      230      |
|    2     |      6     |    banana    |      150      |
|    3     |      8     |    orange    |      200      |
|    4     |      3     |     apple    |      230      |
|    5     |      7     |     mango    |      350      |
|    6     |      6     |    banana    |      150      |


I need the output as
| 	product_id | 	product_sum	  
| 	:-----:	 | 	:-----:	 |  
| 	3	| 	460	|  
| 	6	| 	300	|  
| 	8	| 	200	| 
| 	7	| 	350	|  

SOlution : Select product_id, SUM(product_price) from orders_table GROUP BY product_id
                    ^                                                           ^   what ever is there after select has to be  after group by
| 	product_id | 	number_of_items	  
| 	:-----:	 | 	:-----:	 |  
| 	3	| 	2	|  
| 	6	| 	2	|  
| 	8	| 	1	| 
| 	7	| 	1	|  

Solution : Select product_id, COUNT(product_id) FROM orders_table GROUP BY product_id
                    ^                                                       ^       
                    these two should always be the same (after select and after group by)

## Having
* Having is used after GROUP BY statement to filter records based on aggregate function(after - SUM, COUNT, AVG, MAX, MIN)
* Where cannot be used after GROUP BY clause, so instead use HAVING

1. SELECT company, SUM(sales) WHERE company !="Google" GROUP BY company HAVING SUM(sales)>1000
eg: We are launching a platium service for our most loyal customers. We will assign platinum status to customers that have had 40 or more transaction payments. what customer_ids are eligible for platinum status ?
Solution : Select customer_ids, COUNT(transactions) FROM payments Group by customer_ids Having COUNT(transactions)>=40

## AS clause 
* AS clause is used for alias (rename)
1. Select customer_id, COUNT(*) AS num_of_transactions FROM payments_table

# JOINS 
1. Inner Joins
2. Outer Joins
3. Full Joins 
4. Unions

- Joins allows us to combine two or more tables together

# Inner Join - 
Given two tables, Registration table and Login table

Registration Table 

| 	reg_id | 	name	  
| 	:-----:	 | 	:-----:	 |  
| 	1	| 	Andrew	|  
| 	2	| 	Bob	|  
| 	3	| 	Charlie	| 
| 	4	| 	David	|  

Login Table 

| 	login_id | 	name	  
| 	:-----:	 | 	:-----:	 |  
| 	1	| 	Xavier	|  
| 	2	| 	Andrew	|  
| 	3	| 	Yolanda	| 
| 	4	| 	Bob	|

![alt text](image.png)

Result Table - Select * from Registration Inner Join Login Where Registration.name = Login.name

| 	reg_id | 	name	 |  login_id    |   name 
| 	:-----:	 | 	:-----:	 |  :-----:	    |  :-----:	 |  
| 	1	| 	Andrew	|   2       |       Andrew      |
| 	2	| 	Bob	|       4       |       Bob         |

