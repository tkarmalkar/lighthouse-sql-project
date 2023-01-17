What issues will you address by cleaning the data?
All sessions:
Time - not sure what is the unit of time column (second or millisecond)
Country & City is populated with (not set) in few records       
Time on site - unit is not clear. Sometime null, sometime small value, sometime very high value of 1000+
Date is in incorrect format
Total transaction revenue is always null
Price format is incorrect
Currency is not populates as USD for all records

Analytics:
UserID is always null
Visit starttime is in incorret format
Unit price is in incorrect format

Products:
sentimentscore and sentimentmagintude is null for one record

Sales by sku:
No issues


Queries:
    create table public.all_session_clean as
    select 
 	fullvisitorid ,
    channelgrouping,
	time,
	country,
    city,
  	COALESCE(round(totaltransactionrevenue/1000000,2),0) as totaltransactionrevenue,
	COALESCE(transactions,0) transactions,
	COALESCE((cast(timeonsite as int)/60),0) as duration_min,
	pageviews,
	sessionqualitydim,
	cast(date as date) as date,
	visitid,
	type,
	COALESCE(productrefundamount/1000000,0) as productrefundamount,
	COALESCE(productquantity,0) productquantity,
	COALESCE(productprice/1000000,0) as productprice,
	COALESCE(cast(productrevenue as float)/1000000,2,0) as productrevenue,
	productsku,
	v2productname,
	v2productcategory,
	productvariant,
	COALESCE(currencycode,'USD') currencycode,
	itemquantity,
	itemrevenue,
	COALESCE(transactionrevenue/1000000,0) as transactionrevenue,
	transactionid,
	pagetitle,
	searchkeyword,
	pagepathlevel1,
	ecommerceaction_type,
	ecommerceaction_step,
	ecommerceaction_option
    from public.all_session;

    create table public.analytics_clean as
    select 
    visitnumber,
    visitid,
    visitstarttime,
    date,
    fullvisitorid,
    userid,
    channelgrouping,
    socialengagementtype,
    units_sold,
    pageviews,
    timeonsite,
    bounces,
    revenue,
    COALESCE(unit_price/1000000,0) as unit_price
    from public.analytics


