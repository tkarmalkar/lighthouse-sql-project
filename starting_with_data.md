Question 1: 
Repeat visitors to the site on given day

SQL Queries:
select date,count(distinct fullvisitorid),count(distinct visitid) from public.all_session
group by date;

Answer: 
Example on following day one visitor has visited more than once. 
"20160805"	59	60


Question 2: 
Identify how the website is performing against various sources of traffic.

SQL Queries:
select channelgrouping,count(1) from public.all_session
group by channelgrouping;

Answer:
Organice search is working great.



Question 3: 
Visitor who visited more than multiple product categories

SQL Queries:
select fullvisitorid,v2productcategory,count(1) from public.all_session
group by fullvisitorid,v2productcategory
having count(1) > 5
limit 100;

Answer:
Two users visited 5 categories. We can find more such users.


Question 4: 

SQL Queries:

Answer:



Question 5: 

SQL Queries:

Answer:
