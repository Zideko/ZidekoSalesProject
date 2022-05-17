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
## Powerbi
1 Start by loading the data from SQL

2 Model the data into an appropriate star schema as shown below.

![image](https://user-images.githubusercontent.com/98240082/168786563-b86c3ad7-9c4d-49a6-bb07-ca5b9f951cfd.png)


3 Filter New York and Paris from the markets table
```
= Table.SelectRows(sales_markets, each ([zone] <> ""))
```

4 Ignore all amounts in transactions sales amount that are 0 or in negatives
```
= Table.SelectRows(sales_transactions, each ([sales_amount] <> -1 and [sales_amount] <> 0))
```

5 Converting USD sales amount to Sales amount in INR by multiplying by 75
```
= Table.AddColumn(#"Ignore sales =0,-1", "Norm_Sales_Amount", each if [currency] = "USD" or [currency]= "USD#(cr)"
 then [sales_amount]*75 else [sales_amount])
 ```
6 Removing duplicate transactions
```
= Table.SelectRows(#"Converting USD to INR", each ([currency] = "INR#(cr)" or [currency] = "USD#(cr)"))
```
7 Build a report with the transformed data as shown below.
![image](https://user-images.githubusercontent.com/98240082/168786185-7e135d16-3743-4959-ace7-2772c637516e.png)








