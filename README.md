# Data-Scientist-Role-Play-Profiling-and-Analyzing-the-Yelp-Dataset-Coursera

-- Part 1: Yelp Dataset Profiling and Understanding

1. Profiling the data.
-- Total number of records for each table:	
i. Attribute table =10 000
ii. Business table =10 000
iii. Category table =10 000
iv. Checkin table =10 000
v. elite_years table =10 000
vi. friend table = 10 000
vii. hours table =10 000
viii. photo table = 10 00
ix. review table = 10 000
x. tip table = 10 000
xi. user table =10 000
-- SQL  Code used:
SELECT
          COUNT(*) AS Total
FROM
          Table Name


-- 2.The total distinct records by either the foreign key or primary key for each table.



i. Business = id(PK) = 10 000
ii. Hours 
business_id(FK) = 1562

iii. Category 
business_id(FK) = 2643

iv. Attribute 
business_id(FK) = 1115

v. Review 
id(PK) = 10 000
business_id(FK) = 8090
user_id(FK) = 9581

vi. Checkin 
business_id(FK) = 493

vii. Photo 
id(PK) = 10 000
business_id(FK) = 6493

viii. Tip 
user_id(FK) = 537
business _id(FK) =3979

ix. User 
id(PK) = 10 000

x. Friend 
user_id(FK) =11

xi. Elite_years 
user_id(FK) = 2780

-- PK=Primary Key,FK=Foreign Key


-- SQL Code used:

SELECT
         COUNT(Distinct(key))
From
       Table Name;

-- Note: Primary Keys are denoted in the ER-Diagram with a yellow key icon.	



-- 3. Are there any columns with null values in the Users table?

	Answer: There are no columns with null values.
	
	
	-- SQL code used to arrive at answer:

SELECT
         COUNT(*)
From
      User
WHERE
            id IS NULL OR
            name IS NULL OR
            review_count IS NULL OR
            yelping_since IS NULL OR
            useful IS NULL OR
            funny IS NULL OR
            cool IS NULL OR
            fans IS NULL OR
            average _stars IS NULL OR
            compliment_hot IS NULL OR
            compliment_more IS NULL OR
            compliment_profile IS NULL OR
            compliment_cute IS NULL OR
            compliment_list IS NULL OR
            compliment_note IS NULL OR
            compliment_plain IS NULL OR
            compliment_cool IS NULL OR
            compliment_funny IS NULL OR
            compliment_writer IS NULL OR
            compliment_photos IS NULL
-- Results 



+----------+
| COUNT(*) |
+----------+
|        0 |
+----------+

	
-- 4.Smallest (minimum), largest (maximum), and (mean) value for the following fields:

	i. Table: Review, Column: Stars
	
		min:1		max:5		avg:3.7082
		
	
	ii. Table: Business, Column: Stars
	
		min:1.0		max:5.0		avg:3.6549
		
	
	iii. Table: Tip, Column: Likes
	
		min:0		max:2		avg:0.0144
		
	
	iv. Table: Checkin, Column: Count
	
		min:1		max:53		avg:1.9414
		
	
	v. Table: User, Column: Review_count
	
		min:0		max:2000		avg:24.2995
-- SQL Code used:

SELECT
         MIN(column), MAX(column), AVG(column)
FROM
          Table Name
		


-- 5. Cities with the most reviews in descending order:

	SQL code used to arrive at answer:

SELECT 
        City, SUM(review_count) AS Total_reviews
FROM
       Business 
GROUP BY city
ORDER BY Total_Reviews DESC;
	
	
	 Results:
+-----------------+---------------+
| city            | Total_reviews |
+-----------------+---------------+
| Las Vegas       |         82854 |
| Phoenix         |         34503 |
| Toronto         |         24113 |
| Scottsdale      |         20614 |
| Charlotte       |         12523 |
| Henderson       |         10871 |
| Tempe           |         10504 |
| Pittsburgh      |          9798 |
| Montréal        |          9448 |
| Chandler        |          8112 |
| Mesa            |          6875 |
| Gilbert         |          6380 |
| Cleveland       |          5593 |
| Madison         |          5265 |
| Glendale        |          4406 |
| Mississauga     |          3814 |
| Edinburgh       |          2792 |
| Peoria          |          2624 |
| North Las Vegas |          2438 |
| Markham         |          2352 |
| Champaign       |          2029 |
| Stuttgart       |          1849 |
| Surprise        |          1520 |
| Lakewood        |          1465 |
| Goodyear        |          1155 |
+-----------------+---------------+
(Output limit exceeded, 25 of 362 total rows shown)
	

	
-- 6. Find the distribution of star ratings to the business in the following cities:

i. Avon

-- SQL code used to arrive at answer:

SELECT 
         Review_count AS COUNT, stars AS star_rating
From
        business
WHERE 
          city=“Avon”
GROUP BY stars;


 -- Resulting Table Below (2 columns – star rating and count):

+-------+-------------+
| COUNT | star_rating |
+-------+-------------+
|    10 |         1.5 |
|     6 |         2.5 |
|    88 |         3.5 |
|    21 |         4.0 |
|    31 |         4.5 |
|     3 |         5.0 |
+-------+-------------+


ii. Beachwood

-- SQL code used to arrive at answer:

SELECT 
         Review_count AS COUNT, stars AS star_rating
From
        business
WHERE 
          city=“Beachwood”
GROUP BY stars;


-- Resulting Table Below (2 columns – star rating and count):
		

+-------+-------------+
| COUNT | star_rating |
+-------+-------------+
|     8 |         2.0 |
|     3 |         2.5 |
|     3 |         3.0 |
|     3 |         3.5 |
|    69 |         4.0 |
|     3 |         4.5 |
|     4 |         5.0 |
+-------+-------------+

-- 7.Top 3 users based on their total number of reviews:
		
	SQL code used to arrive at answer:
SELECT 
          name,
          review_count
From
        user
ORDER BY review_count DESC
LIMIT 3;

-- Result:
+--------+--------------+
| name   | review_count |
+--------+--------------+
| Gerald |         2000 |
| Sara   |         1629 |
| Yuri   |         1339 |
+--------+--------------+		


-- 8. Does posing more reviews correlate with more fans?
       
SQL CODE:
SELECT
         name,
         review_count,
         fans,
FROM
        user
ORDER BY fans DESC
LIMIT 3
-- Interpretation of the results:
	
+--------+--------------+------+
| name   | review_count | fans |
+--------+--------------+------+
| Amy    |          609 |  503 |
| Mimi   |          968 |  497 |
| Harald |         1153 |  311 |
+--------+--------------+-----
-- No, it doesn’t not.If you take the top 3 users based on fans and compare it against review_count it doesn’t correlate. For instance Amy has the most fans but the 

least number of reviews and Harald has the most number of reviews but the least fans.

-- 9. Are there more reviews with the word "love" or with the word "hate" in them?

	-- Answer: Yes

	
	-- SQL code used to arrive at answer:

	SELECT
                     COUNT(*)
            From
                    review 
             Where
                       text LIKE “%love%”

-- Results:
+----------+
| COUNT(*) |
+----------+
|     1780 |
+----------+

           SELECT
                     COUNT(*)
           From
                    review
          Where 
                    text LIKE “%hate%”
-- Results:

    +----------+
| COUNT(*) |
+----------+
|      232 |
+----------+
	
-- 10.Top 10 users with the most fans:

	SQL code used to arrive at answer:
SELECT
          name,
          fans 
From
         user
ORDER BY fans Desc
LIMIT 10;
	
	 -- Results:

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
+-----------+------+


	
		

-- Part 2: Inferences and Analysis


-- 1.Picked one city (Toronto) and Category(Food)and group by star rating .
	
-- i. Do the two groups you chose to analyze have a different distribution of hours?

-- Yes, restaurant that open late on Saturday have 4-5 stars and the ones that open earlier have 2-3 stars.

-- ii. Do the two groups you chose to analyze have a different number of reviews?
         
-- Yes ,The restaurant with 4-5 stars have more reviews than the ones with 2-3 stars



-- SQL code used for analysis:

Select
    b.name,
    c.category,
    b.city,
    h.hours,

CASE
        WHEN stars BETWEEN 2 AND 3 THEN "2-3 stars"
        WHEN stars BETWEEN 4 AND 5 THEN "4-5 stars"
    END AS star_rating,
    b.review_count
FROM
    business b
        INNER JOIN
    hours h ON b.id=h.business_id
    category c ON c.business_id=b.id
WHERE 
    city="Toronto"
        AND category="Food"
        AND star_rating IN ("2-3 stars","4-5 stars")
GROUP BY name
ORDER BY star_rating:
		
-- 2. Group business based on the ones that are open and the ones that are closed.
		
-- i. Difference 1:Most of the businesses that open late on Saturday are closed.
         
         
-- ii. Difference 2: In most cases, the business that have a high star rating are still open.
         
         
         
-- SQL code used for analysis:

SELECT 
         b.name,
         b.stars,
          h.hours,
CASE
          WHEN is_open = 1 THEN “open”
          WHEN is_open = 0 THEN “close”
END AS open_or_closed
FROM 
         business b
                INNER JOIN
         hours h ON b.id= h.business_id
ORDER BY stars DESC;

	
-- 3.Analysis on the Yelp dataset.

	
-- i.Type of analysis:

   -- Analysis on how the number of reviews correlates with the number of checkins.
         
-- ii.Type of data needed :

-- The total number of reviews and the average number of checkins. I chose this data because I wanted verify that most people visit and check-in at restaurants that have more reviews because they believe if there are more reviews the possibility of falsifying them is low.

I also wanted to show that people who check-in at restaurants are most likely to leave a review             
                  
-- iii. Output of your finished dataset:
+----------------------------------------------------+-------------------+---------------+
| name                                               | SUM(review_count) |  AVG(c.Count) |
+----------------------------------------------------+-------------------+---------------+
| Cracker Barrel Old Country Store                   |              1782 | 2.43939393939 |
| LongHorn Steakhouse                                |               882 |  2.2619047619 |
| John Christ Winery                                 |               864 |           2.0 |
| Chagrin Valley Little Theatre                      |               116 | 1.86206896552 |
| Panda Chinese Restaurant                           |               304 | 1.63157894737 |
| Courtyard Cleveland Willoughby                     |               660 | 1.58333333333 |
| Highland Square Tavern                             |                72 | 1.58333333333 |

| Pizza Cutter                                       |               198 | 1.55555555556 |
| Burger King                                        |                 8 |           1.5 |
| Rite Aid                                           |               204 | 1.35294117647 |
| Wah Sun                                            |                27 | 1.33333333333 |
| CVS Pharmacy                                       |               114 | 1.31578947368 |
| Davitino's Restaurant                              |               304 |        1.3125 |
| Spudnut Shop Donuts                                |               420 |           1.3 |
| Red Wagon Farm                                     |               143 | 1.27272727273 |
| Chapman's Food Mart                                |                95 | 1.26315789474 |
| Atlas Cinemas                                      |               184 | 1.26086956522 |
| Berkshire Hills Golf Course                        |                56 |          1.25 |
| Galleria Gowns                                     |                64 |          1.25 |
| Stella's Pizza & Italian Restaurant                |               192 |          1.25 |
| Brownie's Market                                   |                32 |         1.125 |
| Case Western Reserve University Faclty Dntl Prctce |                 3 |           1.0 |
| Dairy Queen                                        |                33 |           1.0 |
| Days Inn Willoughby/Cleveland                      |                84 |           1.0 |
| Dons C A R S                                       |                 4 |           1.0 |
+----------------------------------------------------+-------------------+---------------+
(Output limit exceeded, 25 of 29 total rows shown)

         
-- iv. Provide the SQL code you used to create your final dataset:
 Select 
         b.name, SUM(review_count),AVG(c.Count)
From
        business b
               INNER JOIN
         checkin c on b.id=c.business_id
GROUP BY name
ORDER BY AVG(c.Count) DESC


