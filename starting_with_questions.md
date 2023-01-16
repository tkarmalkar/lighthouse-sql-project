Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**

SQL Queries:
select country,city,round(sum(totaltransactionrevenue)/1000000,2) from public.all_session
where totaltransactionrevenue is not null
group by country,city
order by round(sum(totaltransactionrevenue)/1000000,2) desc


Answer:
country city total_revenue
"United States"	"not available in demo dataset"	6092.56
"United States"	"San Francisco"	1564.32
"United States"	"Sunnyvale"	992.23
"United States"	"Atlanta"	854.44
"United States"	"Palo Alto"	608.00



**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:
select country,city,sum(productquantity) total_productquantity,count(1) num_transations,sum(productquantity)/count(1) avg_qty from public.all_session
where productquantity is not null
group by country,city
order by sum(productquantity)/count(1) desc


Answer:
Country City total_products num_session avg_qty
"United States"	"not available in demo dataset"	127	12	10
"Spain"	"Madrid"	10	1	10
"United States"	"Salem"	8	1	8
"United States"	"Atlanta"	4	1	4
"United States"	"Houston"	2	1	2




**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
select country,city,v2productcategory, round(sum(totaltransactionrevenue)/1000000,2) from public.all_session
where totaltransactionrevenue is not null
group by country,city,v2productcategory
order by sum(totaltransactionrevenue) desc


Answer:
It seems Nest products are the popular products across countries and cities




**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:
select country,city, productsku,b.name,round(sum(totaltransactionrevenue)/1000000,2) revenue,count(transactions) qty from public.all_session a
inner join  public.products b
on a.productsku=b.sku
where totaltransactionrevenue is not null
group by country,city,productsku,b.name
order by round(sum(totaltransactionrevenue)/1000000,2) desc 

Answer:
" Cam Outdoor Security Camera - USA" seems to prominent but sold at different prices.




**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:
select country, round(sum(totaltransactionrevenue)/1000000,2) revenue from public.all_session
where totaltransactionrevenue is not null
group by country
order by round(sum(totaltransactionrevenue)/1000000,2) desc

Answer:
United States is the primary market.
"United States"	13154.17	
"Israel"	602.00	
"Australia"	358.00	
"Canada"	150.15	
"Switzerland"	16.99	






