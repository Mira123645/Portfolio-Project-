# Portfolio-Project-
 Profiling and Analyzing the Yelp Dataset 



Part 1: Yelp Dataset Profiling and Understanding

1. Profile the data by finding the total number of records for each of the tables below:
	
i. Attribute table =10000
ii. Business table =10000
iii. Category table =10000
iv. Checkin table =10000
v. elite_years table =10000
vi. friend table =10000 
vii. hours table =10000
viii. photo table =10000
ix. review table =10000
x. tip table =10000 
xi. user table =10000
	


2. Find the total distinct records by either the foreign key or primary key for each table. If two foreign keys are listed in the table, please specify which foreign key.

i. Business = 10000 (Primary Key: id)
ii. Hours = 1562 (Primary Key: businee_id)
iii. Category = 2643 (Primary Key: businee_id)
iv. Attribute = 1115 (Primary Key: businee_id)
v. Review = 10000 (Primary Key: user_id)
vi. Checkin = 493 (Primary Key: businee_id)
vii. Photo = 10000 (Primary Key: businee_id)
viii. Tip = 537 (Primary Key: user_id)
ix. User = 10000 (Primary Key: id)
x. Friend = 11 (Primary Key: user_id)
xi. Elite_years = 2780 (Primary Key: user_id)
	



3. Are there any columns with null values in the Users table? Indicate "yes," or "no."

	Answer:
	No

	SQL code used to arrive at answer:
	select *
from user
where id is Null or name is Null or review_count is Null or yelping_since is Null or useful is Null or funny is Null or cool is null or fans is null or average_stars is Null or compliment_hot is null or compliment_more is null or compliment_profile is null or compliment_cute is null or compliment_list is Null or compliment_note is Null or compliment_plain is Null or compliment_cool is null or compliment_funny is null or compliment_writer is null or compliment_photos is null;

	
4. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:

	i. Table: Review, Column: Stars
	
		min: 1		max: 5		avg: 3.7082
		
	
	ii. Table: Business, Column: Stars
	
		min: 1		max: 5		avg:  3.6549 |
		
	
	iii. Table: Tip, Column: Likes
	
		min: 0   	max: 2     	avg: 0.0144
		
	
	iv. Table: Checkin, Column: Count
	
		min: 1		max: 53		avg:  1.9414
		
	
	v. Table: User, Column: Review_count
	
		min: 0		max: 2000		avg: 24.2995
		


5. List the cities with the most reviews in descending order:

	SELECT city,
sum (review_count) as reviews
from business
group by city
order by reviews desc;

	
	Copy and Paste the Result Below:
 ----------------+---------+
| city            | reviews |
+-----------------+---------+
| Las Vegas       |   82854 |
| Phoenix         |   34503 |
| Toronto         |   24113 |
| Scottsdale      |   20614 |
| Charlotte       |   12523 |
| Henderson       |   10871 |
| Tempe           |   10504 |
| Pittsburgh      |    9798 |
| Montréal        |    9448 |
| Chandler        |    8112 |
| Mesa            |    6875 |
| Gilbert         |    6380 |
| Cleveland       |    5593 |
| Madison         |    5265 |
| Glendale        |    4406 |
| Mississauga     |    3814 |
| Edinburgh       |    2792 |
| Peoria          |    2624 |
| North Las Vegas |    2438 |
| Markham         |    2352 |
| Champaign       |    2029 |
| Stuttgart       |    1849 |
| Surprise        |    1520 |
| Lakewood        |    1465 |
| Goodyear        |    1155 |
+-----------------+---------+
(Output limit exceeded, 25 of 362 total rows shown)


	
6. Find the distribution of star ratings to the business in the following cities:

i. Avon

SQL code used to arrive at answer:
SELECT stars,
	   SUM(review_count) AS count
           FROM business
	   WHERE city == 'Avon'
	   GROUP BY stars	

Copy and Paste the Resulting Table Below (2 columns – star rating and count):
id                     | city |  id  | average_stars |
+-stars | count |
+-------+-------+
|   1.5 |    10 |
|   2.5 |     6 |
|   3.5 |    88 |
|   4.0 |    21 |
|   4.5 |    31 |
|   5.0 |     3 |
+-------+-------+

ii. Beachwood

SQL code used to arrive at answer:
SELECT stars,
	   SUM(review_count) AS count
           FROM business
	   WHERE city == 'Beachwood'
	   GROUP BY stars	


Copy and Paste the Resulting Table Below (2 columns – star rating and count):
		
-------+-------+
| stars | count |
+-------+-------+
|   2.0 |     8 |
|   2.5 |     3 |
|   3.0 |    11 |
|   3.5 |     6 |
|   4.0 |    69 |
|   4.5 |    17 |
|   5.0 |    23 |
+-------+-------+

7. Find the top 3 users based on their total number of reviews:
		
SQL code used to arrive at answer:
select name, review_count from user
order by review_count desc;	
		
	Copy and Paste the Result Below:
+--------+--------------+
| name   | review_count |
+--------+--------------+
| Gerald |         2000 |
| Sara   |         1629 |
| Yuri   |         1339 |
+--------+--------------+


8. Does posting more reviews correlate with more fans?

	Please explain your findings and interpretation of the results:
	
Not Necissarly but also the amount of time that they have been yelping. The longer they 
		have been yelping and the more reviews they give has a higher fan count.


SELECT id,
	  name,
	  review_count,
	  fans,
	   yelping_since
	   FROM user
	   ORDER BY fans DESC

                 ------------------------+-----------+--------------+------+---------------------+
		| id                     | name      | review_count | fans | yelping_since       |
                +------------------------+-----------+--------------+------+---------------------+
		| -9I98YbNQnLdAmcYfb324Q | Amy       |          609 |  503 | 2007-07-19 00:00:00 |
		| -8EnCioUmDygAbsYZmTeRQ | Mimi      |          968 |  497 | 2011-03-30 00:00:00 |
		| --2vR0DIsmQ6WfcSzKWigw | Harald    |         1153 |  311 | 2012-11-27 00:00:00 |
		| -G7Zkl1wIWBBmD0KRy_sCw | Gerald    |         2000 |  253 | 2012-12-16 00:00:00 |
		| -0IiMAZI2SsQ7VmyzJjokQ | Christine |          930 |  173 | 2009-07-08 00:00:00 |
		| -g3XIcCb2b-BD0QBCcq2Sw | Lisa      |          813 |  159 | 2009-10-05 00:00:00 |
		| -9bbDysuiWeo2VShFJJtcw | Cat       |          377 |  133 | 2009-02-05 00:00:00 |
		| -FZBTkAZEXoP7CYvRV2ZwQ | William   |         1215 |  126 | 2015-02-19 00:00:00 |
		| -9da1xk7zgnnfO1uTVYGkA | Fran      |          862 |  124 | 2012-04-05 00:00:00 |
		| -lh59ko3dxChBSZ9U7LfUw | Lissa     |          834 |  120 | 2007-08-14 00:00:00 |
		| -B-QEUESGWHPE_889WJaeg | Mark      |          861 |  115 | 2009-05-31 00:00:00 |
		| -DmqnhW4Omr3YhmnigaqHg | Tiffany   |          408 |  111 | 2008-10-28 00:00:00 |
		| -cv9PPT7IHux7XUc9dOpkg | bernice   |          255 |  105 | 2007-08-29 00:00:00 |
		| -DFCC64NXgqrxlO8aLU5rg | Roanna    |         1039 |  104 | 2006-03-28 00:00:00 |
		| -IgKkE8JvYNWeGu8ze4P8Q | Angela    |          694 |  101 | 2010-10-01 00:00:00 |
		| -K2Tcgh2EKX6e6HqqIrBIQ | .Hon      |         1246 |  101 | 2006-07-19 00:00:00 |
		| -4viTt9UC44lWCFJwleMNQ | Ben       |          307 |   96 | 2007-03-10 00:00:00 |
		| -3i9bhfvrM3F1wsC9XIB8g | Linda     |          584 |   89 | 2005-08-07 00:00:00 |
		| -kLVfaJytOJY2-QdQoCcNQ | Christina |          842 |   85 | 2012-10-08 00:00:00 |
		| -ePh4Prox7ZXnEBNGKyUEA | Jessica   |          220 |   84 | 2009-01-12 00:00:00 |
		| -4BEUkLvHQntN6qPfKJP2w | Greg      |          408 |   81 | 2008-02-16 00:00:00 |
		| -C-l8EHSLXtZZVfUAUhsPA | Nieves    |          178 |   80 | 2013-07-08 00:00:00 |
		| -dw8f7FLaUmWR7bfJ_Yf0w | Sui       |          754 |   78 | 2009-09-07 00:00:00 |
		| -8lbUNlXVSoXqaRRiHiSNg | Yuri      |         1339 |   76 | 2008-01-03 00:00:00 |
		| -0zEEaDFIjABtPQni0XlHA | Nicole    |          161 |   73 | 2009-04-30 00:00:00 |
		+------------------------+-----------+--------------+------+---------------------+
	
	
9. Are there more reviews with the word "love" or with the word "hate" in them?

	Answer: There are more views with the word "love" than the word "hate"
	love has 1780, while hate only has 232 

	
	SQL code used to arrive at answer:
select count(*)
, (select count(*) from review where text like '%love%')
from review
where text like '%hate%';
	
	
10. Find the top 10 users with the most fans:

	SQL code used to arrive at answer:
	select Name, Fans from User
order by Fans desc;
	
	Copy and Paste the Result Below:
+-----------+------+
| name      | fans |
+-----------+------+
| Amy       |  503 |
| Mimi      |  497 |
| Harald    |  311 |
| Gerald    |  253 |
| Christine |  173 |
| Lisa      |  159 |
| Cat       |  133 |
| William   |  126 |
| Fran      |  124 |
| Lissa     |  120 |
| Mark      |  115 |
| Tiffany   |  111 |
| bernice   |  105 |
| Roanna    |  104 |
| Angela    |  101 |
| .Hon      |  101 |
| Ben       |   96 |
| Linda     |   89 |
| Christina |   85 |
| Jessica   |   84 |
| Greg      |   81 |
| Nieves    |   80 |
| Sui       |   78 |
| Yuri      |   76 |
| Nicole    |   73 |
+-----------+------+
	
		

Part 2: Inferences and Analysis

1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.
	
i. Do the two groups you chose to analyze have a different distribution of hours?
 The 4-5 star group seems to have shorter hours then the 2-3 star group.
Please note the query returned only three businesses so not a great sample size.

ii. Do the two groups you chose to analyze have a different number of reviews?
Yes and no, one of the 4-5 star group has a lot more reviews but then the other
4-5 star group has close to the same number of reviews as the 2-3 star group
         
iii. Are you able to infer anything from the location data provided between these two groups? Explain.
No, every business is in a different zip-code.

SQL code used for analysis:
ELECT B.name,
			   B.review_count,
			   H.hours,
			   postal_code,
			   CASE
				  WHEN hours LIKE "%monday%" THEN 1
				  WHEN hours LIKE "%tuesday%" THEN 2
				  WHEN hours LIKE "%wednesday%" THEN 3
				  WHEN hours LIKE "%thursday%" THEN 4
				  WHEN hours LIKE "%friday%" THEN 5
				  WHEN hours LIKE "%saturday%" THEN 6
				  WHEN hours LIKE "%sunday%" THEN 7
			   END AS ord,
			   CASE
				  WHEN B.stars BETWEEN 2 AND 3 THEN '2-3 stars'
				  WHEN B.stars BETWEEN 4 AND 5 THEN '4-5 stars'
			   END AS star_rating
		FROM business B INNER JOIN hours H
		ON B.id = H.business_id
		INNER JOIN category C
		ON C.business_id = B.id
		WHERE (B.city == 'Las Vegas'
		AND
		C.category LIKE 'shopping')
		AND
		(B.stars BETWEEN 2 AND 3
		OR
		B.stars BETWEEN 4 AND 5)
		GROUP BY stars,ord
		ORDER BY ord,star_rating ASC
		
		
2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.
		
i. Difference 1:
 The businesses that are open tend to have more reviews than ones that
		are closed on average.
		
			Open:   AVG(review_count) = 31.757
			Closed: AVG(review_count0 = 23.198    
         
ii. Difference 2:
 The average star rating is higher for businesses that are open than
		businesses that are closed.
	
			Open:   AVG(stars) = 3.679
			Closed: AVG(stars) = 3.520
	
         
SSQL code used for analysis:
	
		SELECT COUNT(DISTINCT(id)),
			   AVG(review_count),
			   SUM(review_count),
			   AVG(stars),
			   is_open
		FROM business
		GROUP BY is_open


3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.

Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:
	
i. Indicate the type of analysis you chose to do:
      Predicting whether a business will stay open or close. We wish not to explicitly
		examine the text of the reviews, but this would be an interesting analysis.
         
ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:
      To better help businesses understand the importance of different factors which
		will help their business stay open. Some data that may be important; number of
		reviews, star rating of business, hours open, and of course location location
		location. We will gather the latitude and longitude as well as city, state, 
		postal_code, and address to make processing easier later on. Categories and 
		attributes will be used to better distinguish between different types of 
		businesses. `is_open` will determine which business is open and which business 
		have closed (not hours) but permanently.
	
iii. Provide the SQL code you used to create your final dataset:

SELECT B.id,
			   B.name,
			   B.address,
			   B.city,
			   B.state,
			   B.postal_code,
			   B.latitude,
			   B.longitude,
			   B.review_count,
			   B.stars,
			   MAX(CASE
			   WHEN H.hours LIKE "%monday%" THEN TRIM(H.hours,'%MondayTuesWednesThursFriSatSun|%') 
			   END) AS monday_hours,
			   MAX(CASE
			   WHEN H.hours LIKE "%tuesday%" THEN TRIM(H.hours,'%MondayTuesWednesThursFriSatSun|%') 
			   END) AS tuesday_hours,
			   MAX(CASE
			   WHEN H.hours LIKE "%wednesday%" THEN TRIM(H.hours,'%MondayTuesWednesThursFriSatSun|%') 
			   END) AS wednesday_hours,
			   MAX(CASE
			   WHEN H.hours LIKE "%thursday%" THEN TRIM(H.hours,'%MondayTuesWednesThursFriSatSun|%') 
			   END) AS thursday_hours,
			   MAX(CASE
			   WHEN H.hours LIKE "%friday%" THEN TRIM(H.hours,'%MondayTuesWednesThursFriSatSun|%') 
			   END) AS friday_hours,
			   MAX(CASE
			   WHEN H.hours LIKE "%saturday%" THEN TRIM(H.hours,'%MondayTuesWednesThursFriSatSun|%') 
			   END) AS saturday_hours,
			   MAX(CASE
			   WHEN H.hours LIKE "%sunday%" THEN TRIM(H.hours,'%MondayTuesWednesThursFriSatSun|%') 
			   END) AS sunday_hours,
			   GROUP_CONCAT(DISTINCT(C.category)) AS categories,
			   GROUP_CONCAT(DISTINCT(A.name)) AS attributes,
			   B.is_open
		FROM business B
		INNER JOIN hours H
		ON B.id = H.business_id
		INNER JOIN category C
		ON B.id = C.business_id
		INNER JOIN attribute A
		ON B.id = A.business_id
		GROUP BY B.id
