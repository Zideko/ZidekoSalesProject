# Sales Insight Data Analysis Project
## Data Analysis Using SQL
1 Load the data onto mysql workbench
2 To show all customer records
```
SELECT * FROM sales.customers;
```
3 To showtotal number of customers
```
SELECT count(*) FROM sales.customers;
```
4 Show transactions for Chennai market (market code for chennai is Mark001)
```
select * from sales.transactions where Market_code="Mark001";

```
5 Show distinct product codes that were sold in chennai
```
select distinct product_code from sales.transactions where Market_code="Mark001"
```
6 Show transactions where currency is US dollars
```
select * from sales.transactions where currency="USD";
```
7 Show transactions in 2020 join by date table
```
SELECT sales.transactions.*, sales.date.* FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020;
 
```
8 Show total revenue in year 2020
```
SELECT sum(sales_amount) FROM sales.transactions INNER JOIN sales.date 
ON sales.transactions.order_date=sales.date.date where sales.date.year=2020;
```
9 Show total revenue in year 2020, January Month
```
SELECT sum(sales_amount) FROM sales.transactions INNER JOIN sales.date 
ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.date.month_name="January"
```
10 Show total revenue in year 2020 in Chennai
```
SELECT sum(sales_amount) FROM sales.transactions INNER JOIN sales.date 
ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.transactions.market_code="Mark001";
```

