  **Sales-Insight-Analysis-in-MYSQL**

 **SQL database dump is in db_dump.sql file under the Sales-Insight-Analysis-in-MYSQL**

 **Queries perforemed :**

1. Show all customer records

  SELECT * FROM customers;

2. Show total number of customers

  SELECT count(*) FROM customers;

3. Show transactions for Chennai market (market code for chennai is Mark001

   SELECT * FROM transactions where market_code='Mark001';

4. Show distrinct product codes that were sold in chennai

   SELECT distinct product_code FROM transactions where market_code='Mark001';

5. Show transactions where currency is US dollars

   SELECT * from transactions where currency="USD"

6. Print all the columns from the transactions table
  
  > select sales.transactions.* FROM sales.transactions;
  
  > Note: .* use to print all the coulmn informations.


7. Show transactions in 2020 join by date table

First join "sales.transactions" and "date" table by performing the below queries...
   
	 SELECT sales.transactions.*, sales.date.* FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date;

Now, find the transactions which specifically for 2020 year.

    SELECT transactions.*, date.* FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020;


8. Show total revenue in year 2020,

    SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020;

In case there is currency issue, for instance to get the data in INR format from USD formated date....
       
			 SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and         sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r";
OR
      
			SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.currency="INR\r" or transactions.currency="USD\r";

9. Show total revenue in year 2020, January Month,

    
		SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and and date.month_name="January" and (transactions.currency="INR\r" or transactions.currency="USD\r");

10. Show total revenue in year 2020 in Chennai

    
		SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.market_code="Mark001";**

  **Data Analysis Using Power BI**
   
   We see that the column "sales_amount" has two different types of Currency, such as INR and USD, so we need to get all the amount details in INR and we use Conditional column add by given below formula: Note: Under Custom Column, "norm_amount" changes done.
    
     = Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)
    1. Formula to create norm_amount column
