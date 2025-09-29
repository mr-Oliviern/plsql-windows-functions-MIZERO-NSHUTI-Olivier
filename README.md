# plsql-windows-functions-MIZERO-NSHUTI-Olivier
## INTRODUCTION 
- *NAME:*MIZERO NSHUTI Olivier
- *Id:* 28333
- *course:* DATABASE DEVELOPMENT WITH PL/SQL INSY 8311

---
   
## step 1: Problem definition 

The problem of business scenario is accessing products Our analysis needs to identify the top 3 best-selling products by revenue within each sales region for the last quarter. The problem we have is that we have to rank products within their specific regions, not globally.  Also we need to calculate the total revenue of each product.
 Here there are the business context
Company Type:( global store ) a multinational selling site 
Departments: Marketing & inventory management 
Industry:  E-commerce & Retail.What this business context are expected to help the business For Marketing Department: the target is to list the top-performing products per region to focus on localized digital advertising campaigns and promotional offers.
For Inventory Management Department: the Data to validate and optimize regional warehouse stock levels, ensuring high availability for top sellers while reducing overstock of slower-moving items
Not only that but also finding a simplest way of connecting customers to their desirable products is one of our best objective that will make a positive change for salers to earn more income as a way of simplifying tasks for peaple mainly located in the cities and develop the rural ones

## Success Criteria 

1.	Top 5 products per region/quarter → RANK (): we use this to identify the best-selling items in each region every quarter 
2.	2. Running monthly sales totals → SUM () OVER (): we will use this to calculate cumulative monthly sales totals to truck growth.3.	Month-over-month revenue growth per product → we will apply LAG ()/LEAD () to compare each products revenue against the previous month and compare growth %
4.	Customer segmentation by spend classify customers into 4 quartiles (25% groups) with NTILE (4) based on lifetime electronics purchases.
5.	3-month moving average sales per product use → AVG () OVER () to smooth fluctuations in electronics sales trends

6.	## Database Schema

7.	for the information related to customers will be stored in this table
8.	<img width="401" height="164" alt="image" src="https://github.com/user-attachments/assets/6ba0d7f4-ff0e-4295-a518-7f455500260a" />



Here there are table which store data from products
<img width="390" height="242" alt="image" src="https://github.com/user-attachments/assets/33247752-64ae-48ba-8401-122f8e7b5fd7" />

 
Also this is the table which show the information for transactions
<img width="660" height="232" alt="image" src="https://github.com/user-attachments/assets/1a1b7d40-7c4b-4dd4-843b-8340e218d45f" />

Here we have the image which shows the entity relationship of those three tables 

<img width="608" height="237" alt="image" src="https://github.com/user-attachments/assets/839c1fdf-93f4-462d-8b1a-0bc250358a7c" />

## Window Functions Implementation

For Ranking: we start with: ROW_NUMBER ()
This is the codes used to ranking with ROW_NUMBER ()
select customer_ID, customer_names,region
 ,ROW_NUMBER() OVER(ORDER BY customer_names ASC) RNR from CUSTOMER; 
Here there are the screen shoot of how the table arranged
<img width="804" height="243" alt="image" src="https://github.com/user-attachments/assets/69771eb5-67ae-495a-86c6-3ab2f93ab46c" />


For Ranking with using RANK ()
This is the codes used to ranking with RANK ()
select customer_ID, customer_names,region
 ,RANK() OVER(ORDER BY customer_names ASC) RNK from CUSTOMER;Here there are the screen shoot of how the table arranged

<img width="720" height="210" alt="image" src="https://github.com/user-attachments/assets/79fc3026-4343-4eed-8513-5ece3c6b08fa" />


For Ranking with using DENSE_RANK ()
This is the codes used to ranking with DENSE_RANK ()
select customer_ID, customer_names,region
 ,DENSE_RANK() OVER(ORDER BY customer_names ASC) DRK from CUSTOMER;
 Here there are the screen shoot of how the table arranged
 
 <img width="789" height="232" alt="image" src="https://github.com/user-attachments/assets/0b6afaf5-0eb9-4231-ac7a-eda1672c58c8" />

For Ranking with using PERCENT_RANK ()
This is the codes used to ranking with PERCENT_RANK ()
select customer_ID, customer_names,region
 ,PERCENT_RANK() OVER(ORDER BY customer_names ASC) PRK from CUSTOMER;
Here there are the screen shoot of how the table arranged

<img width="671" height="256" alt="image" src="https://github.com/user-attachments/assets/5a858468-a7ab-4d20-a3fa-15cde104aa30" />

By showing the image of ranking with using all categories hare there are screen shoot which show it 

<img width="957" height="211" alt="image" src="https://github.com/user-attachments/assets/840d8b99-61ed-43f2-8fcf-400f1dda3cc4" />

   HERE THERE ARE THE SREEN SHOOT WHICH SHOWS HOW THE TABLES ARE JOINED 
FOR THE FIRST WE JOINED CUSTOMER TABLES WITH TRANSACTIONS TABLE THIS IS HOW IT LOOKS LI
<img width="790" height="256" alt="image" src="https://github.com/user-attachments/assets/deff3549-df0f-44bb-8400-b63c7aae22c2" />

So after joining table we are going to the step of AGGREGATE
Aggregate      FOR SUM () OF amount which are received in our company 
This table sum the total amount but also grouped by  customer_id and product_id
<img width="260" height="81" alt="image" src="https://github.com/user-attachments/assets/1a3a26cf-3de7-4357-8639-df14f7a6fefe" />


For the second aggregate of AVG () for average amount we calculated the average amount for every customer but are grouped by customer_id and product_id here we have the screen shoot that shows how the output is that I it for avg () in SQL

<img width="845" height="263" alt="image" src="https://github.com/user-attachments/assets/807cc7f6-f6c1-4fe5-bcbf-fd47fdd8ec02" />
For min () is the other step we are going to show how it looks. Therefore we are going to looks like

<img width="840" height="287" alt="image" src="https://github.com/user-attachments/assets/7854f2db-87b7-413e-af7c-7fb49ae0219f" />
The next is to find the max () amount in the transactions table 
Here we have the screen shoot of table which shows maximum amount 

<img width="956" height="153" alt="image" src="https://github.com/user-attachments/assets/fb3b5056-0baa-443d-b490-52033692a663" />
For the other aggregate we are going to check for ROWS vs RANGE
For ROWS this is the table which shows how the rows are ordered by using amount

<img width="529" height="190" alt="image" src="https://github.com/user-attachments/assets/73b2d1c5-ebc7-49cc-844d-148d2bfd5372" />
For RANGE here we have the screen shoot of how the table of range must look like

<img width="594" height="241" alt="image" src="https://github.com/user-attachments/assets/7b8810c9-ab13-4a0b-acb9-19ab3d8427ed" />

Navigation: LAG (), LEAD ()
We start with LAG () this is the table which shows the LAG () IN our table of transactions

<img width="852" height="153" alt="image" src="https://github.com/user-attachments/assets/f98edea8-5c4b-4ff1-b05d-bfdbcb7c0f50" />
For the next we are going to se the LEAD () navigation 

<img width="689" height="260" alt="image" src="https://github.com/user-attachments/assets/d0fd9a26-c49a-4d84-9f9a-abf8447dec39" />

Distribution: NTILE (4), CUME_DIST ()
We have come from the distribution of our tables 

We are going to start with NTILE (4 here we have the screen shoot of how this function are shown and used 

<img width="872" height="198" alt="image" src="https://github.com/user-attachments/assets/3316de06-9c82-499f-ac75-c4f482060e99" />

After using NTILE (4 we are going to use the other navigation which called 
CUME_DIST () as we use this function here we have the screen shoot of our table which shows it in good way 

<img width="880" height="194" alt="image" src="https://github.com/user-attachments/assets/7276a368-d6b3-4386-8db3-1e76dd535761" />
