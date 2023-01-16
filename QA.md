What are your risk areas? Identify and describe them.
all_sessions:
The table may not get loaded on a given day.
The currencycode may not get populated even though there was a revenue transaction.

analytics:
The table may not get loaded on a given day.
 

QA Process:
Describe your QA process and include the SQL queries used to execute it.

Validation of daily loading in 'all_session' table:
select date,count(1) from public.all_session
group by date
order by date desc

Validation of null currency in  'all_session' table:
select * from public.all_session
where currencycode is null
and totaltransactionrevenue is not null;

Validation of daily loading in 'analytics' table:
select date,count(1) from public.analytics
group by date
order by date desc;


