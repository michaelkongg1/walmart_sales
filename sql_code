USE walmart;
SHOW TABLES;
SELECT COUNT(*) FROM walmartt;
SELECT * FROM walmartt LIMIT 10;
SELECT payment_method, COUNT(*) 
FROM walmartt 
GROUP BY payment_method;
SELECT COUNT(DISTINCT branch) FROM walmartt;

-- Q1: Find different payment methods, number of transactions, and quantity sold by payment method
SELECT 
	payment_method,
    COUNT(*) as number_of_payments, 
    SUM(quantity) as number_quantity 
FROM walmartt
GROUP BY payment_method;

-- Q2: Identify the highest-rated category in each branch
-- Display the branch, category, and avg rating
SELECT * 
FROM (
    SELECT
        branch, 
        category, 
        avg_rating,
        RANK() OVER (PARTITION BY branch ORDER BY avg_rating DESC) AS ranking
    FROM (
        SELECT
            branch,
            category,
            AVG(rating) AS avg_rating
        FROM walmartt
        GROUP BY branch, category
    ) AS avg_table
) AS ranked_table
WHERE ranking = 1;

-- Q3: Identify the busiest day for each branch based on the number of transactions
SELECT *
FROM (
	SELECT
		branch,
		day_of_week,
		number_transactions,
		RANK() OVER (
			PARTITION BY branch
			ORDER BY number_transactions DESC
		) AS rankk
	FROM (
		SELECT
			branch,
			DATE_FORMAT(STR_TO_DATE(date, '%d/%m/%y'), '%W') AS day_of_week,
			COUNT(*) AS number_transactions
		FROM walmartt
		GROUP BY branch, day_of_week
	) AS tablee
) AS tableee
WHERE rankk = 1;

-- Q4: Determine the average, minimum, and maximum rating of categories for each city
SELECT
	city,
    category,
	AVG(rating) as average,
    MAX(rating) as max,
    MIN(rating) as min
FROM walmartt
GROUP BY category, City;

-- Q5: Calculate the total profit for each category
SELECT 
	category,
	SUM(profit_margin*total) AS profit
FROM walmartt
GROUP BY category
ORDER BY profit DESC;

-- Q6: Determine the most common payment method for each branch
WITH cte AS (
		SELECT 
        branch,
        payment_method,
        number_paymentmethod,
        RANK() OVER (PARTITION BY branch ORDER BY number_paymentmethod DESC) as rankk
	FROM (
			SELECT
				branch,
				payment_method,
				COUNT(*) AS number_paymentmethod
			FROM walmartt
			GROUP BY branch, payment_method
	) AS subquery
)
SELECT * FROM cte WHERE rankk ='1';
-- Q7: Categorize sales into Morning, Afternoon, and Evening shifts
SELECT 
	branch,
    CASE 
        WHEN HOUR(STR_TO_DATE(time, '%H:%i')) < 12 THEN 'Morning'
        WHEN HOUR(STR_TO_DATE(time, '%H:%i')) BETWEEN 12 AND 17 THEN 'Afternoon'
        ELSE 'Evening'
    END AS day_time,
    COUNT(*) AS total_transactions
FROM walmartt
GROUP BY branch, day_time 
ORDER BY branch, total_transactions DESC;
-- Q8: Identify the 5 branches with the highest revenue decrease ratio from last year to current year (e.g., 2022 to 2023)

-- rdr == last_rev-cur_rev/last_rev*100

WITH revenue2022 AS
(
SELECT 
	branch,
	SUM(total) AS revenue
FROM walmartt
WHERE YEAR(STR_TO_DATE(date, '%d/%m/%y')) =2022
GROUP BY branch
),
revenue2023
AS
(
SELECT 
	branch,
	SUM(total) AS revenue
FROM walmartt
WHERE YEAR(STR_TO_DATE(date, '%d/%m/%y')) =2023
GROUP BY branch
)
SELECT 
	ls.branch,
    ls.revenue as last_revenue,
    cs.revenue as cur_revenue,
   ROUND( (ls.revenue-cs.revenue)/ls.revenue*100,2) as rev_decrease_ratio
FROM revenue2022 AS ls
JOIN
revenue2023 as cs
ON ls.branch=cs.branch
WHERE
	ls.revenue > cs.revenue  
ORDER BY 4 DESC LIMIT 5;
