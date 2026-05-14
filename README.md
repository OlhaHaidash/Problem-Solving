# Problem-Solving

Table of Contents

[SQL 50](#sql-50)


# SQL 50

<img align="left" width="70" src="https://github.com/OlhaHaidash/Problem-Solving/blob/main/%D0%97%D0%BD%D1%96%D0%BC%D0%BE%D0%BA%20%D0%B5%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202026-04-29%20%D0%BE%2017.31.56.png"> **[Problems](https://leetcode.com/studyplan/top-sql-50/)**

**1. Select**

<details>
  <summary>Recyclable and Low Fat Products ✅</summary>

  ```sql
  SELECT product_id  
  FROM products  
  WHERE low_fats = 'Y' AND recyclable = 'Y' 
  ```

</details>


<details>
  <summary>Find Customer Referee ✅</summary>
  
  ```sql
SELECT name
FROM customer
WHERE referee_id <> 2 OR referee_id IS NULL
  ```

</details>

<details>
  <summary>Big Countries ✅</summary>
  
  ```sql
SELECT name, population, area
FROM world
WHERE area >= 3000000 OR population >=25000000
  ```

</details>

<details>
  <summary>Article Views I ✅</summary>
  
  ```sql
SELECT DISTINCT(author_id) as id
FROM views
WHERE author_id = viewer_id
  ```

</details>

<details>
  <summary>Invalid Tweets ✅</summary>
  
  ```sql
SELECT tweet_id
FROM tweets
WHERE LENGTH(content) > 15
  ```

</details>

**2. Basic Joins**

<details>
  <summary>Replace Employee ID With The Unique Identifier ✅</summary>  
  
  ```sql
SELECT eu.unique_id, e.name
FROM Employees e 
LEFT JOIN EmployeeUNI eu ON e.id = eu.id;
  ```

</details>

<details>
  <summary>Product Sales Analysis I ✅</summary>  
  
  ```sql
SELECT product_name, year, price
FROM sales s 
LEFT JOIN product p USING(product_id)
  ```

</details>

<details>
  <summary>Customer Who Visited but Did Not Make Any Transactions ✅</summary>  
  
  ```sql
SELECT customer_id, COUNT(*) AS count_no_trans
FROM visits LEFT JOIN transactions USING(visit_id)
WHERE transaction_id IS NULL
GROUP BY customer_id
ORDER BY count_no_trans
  ```

</details>

<details>
  <summary>Rising Temperature ✅</summary>  
  
  ```sql
SELECT w1.id
FROM Weather w1
JOIN Weather w2 
  ON w1.recordDate = w2.recordDate + 1
WHERE w1.temperature > w2.temperature;
  ```

</details>

<details>
  <summary>Average Time of Process per Machine ✅</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Employee Bonus ✅</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Students and Examinations ✅</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Managers with at Least 5 Direct Reports ✅</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Confirmation Rate ✅</summary>  
  
  ```sql
SELECT 
        user_id,
        ROUND(SUM(CASE WHEN action = 'confirmed' THEN 1 ELSE 0 END) :: numeric
        / COUNT(*), 2) AS confirmation_rate
FROM signups s
LEFT JOIN confirmations c USING (user_id)
GROUP BY 1
  ```

</details>

**3. Basic Aggregate Functions**

<details>
  <summary>Not Boring Movies ✅</summary>  
  
  ```sql
SELECT *
FROM cinema
WHERE id % 2 = 1 AND LOWER(description) NOT LIKE 'boring'
ORDER BY rating DESC
  ```

</details>

<details>
  <summary>Average Selling Price ✅</summary>  
  
  ```sql
SELECT p.product_id, 
        COALESCE(ROUND(SUM(price * units) :: numeric /SUM(units),2),0) AS average_price
FROM prices p
LEFT JOIN unitssold u ON p.product_id=u.product_id AND purchase_date >= start_date AND purchase_date <= end_date
GROUP BY 1
  ```

</details>

<details>
  <summary>Project Employees I ✅</summary>  
  
  ```sql
SELECT p.project_id, ROUND(AVG(experience_years), 2) AS average_years
FROM project p
LEFT JOIN employee e USING(employee_id)
GROUP BY 1
  ```

</details>

<details>
  <summary>Percentage of Users Attended a Contest ✅</summary>  
  
  ```sql
SELECT contest_id,
        ROUND(COUNT(r.user_id) :: numeric  / (SELECT COUNT(*) FROM users) * 100,2) AS percentage
FROM register r
LEFT JOIN users USING(user_id)
GROUP BY contest_id
ORDER BY 2 DESC, 1
  ```

</details>

<details>
  <summary>Queries Quality and Percentage ✅</summary>  
  
  ```sql
SELECT 
        query_name,
        ROUND(AVG(rating/position :: numeric),2) AS quality,
        ROUND(COUNT(CASE WHEN rating < 3 THEN 1 END) / COUNT(rating) :: numeric * 100,2) AS poor_query_percentage
FROM queries
GROUP BY 1
  ```

</details>

<details>
  <summary>Monthly Transactions I ✅</summary>  
  
  ```sql
SELECT
    TO_CHAR(DATE_TRUNC('month', trans_date), 'YYYY-MM') AS month,
    country,
    COUNT(id) AS trans_count,
    COUNT(CASE WHEN state = 'approved' THEN 1  END) AS approved_count,
    SUM(amount) AS trans_total_amount,
    SUM(CASE WHEN state = 'approved' THEN amount ELSE 0 END) AS approved_total_amount
FROM transactions
GROUP BY 1,2
  ```

</details>

<details>
  <summary>Immediate Food Delivery II ✅</summary>  
  
  ```sql
WITH a AS (
SELECT *,
        CASE WHEN order_date = customer_pref_delivery_date THEN 'immediate' ELSE 'scheduled' END AS status,
        CASE WHEN order_date = (MIN(order_date) OVER (PARTITION BY customer_id ORDER BY order_date)) THEN 'first order' END AS is_first_order
FROM delivery
)
SELECT
    ROUND(COUNT(CASE WHEN status = 'immediate' AND is_first_order = 'first order' THEN 1 END) :: numeric / COUNT(CASE WHEN is_first_order = 'first order' THEN 1 END) * 100,2) AS immediate_percentage
FROM a
  ```

</details>

<details>
  <summary>Game Play Analysis IV 🔲</summary>  
  
  ```sql

  ```

</details>

**4. Sorting and Grouping**

<details>
  <summary>Number of Unique Subjects Taught by Each Teacher ✅</summary>  
  
  ```sql
SELECT teacher_id, COUNT(DISTINCT subject_id) AS cnt
FROM teacher
GROUP BY 1
  ```

</details>

<details>
  <summary>User Activity for the Past 30 Days I 🔲</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Product Sales Analysis III 🔲</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Classes More Than 5 Students 🔲</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Find Followers Count 🔲</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Biggest Single Number 🔲</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Customers Who Bought All Products 🔲</summary>  
  
  ```sql

  ```

</details>

**5. Advanced Select and Joins**

<details>
  <summary>The Number of Employees Which Report to Each Employee 🔲</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Primary Department for Each Employee 🔲</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Triangle Judgement 🔲</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Consecutive Numbers 🔲</summary>  
  
  ```sql

  ```

</details>
    
<details>
  <summary>Product Price at a Given Date 🔲</summary>  
  
  ```sql

  ```

</details>
    
<details>
  <summary>Last Person to Fit in the Bus 🔲</summary>  
  
  ```sql

  ```

</details>
    
<details>
  <summary>Count Salary Categories 🔲</summary>  
  
  ```sql

  ```

</details>
  

**6. Subqueries**

<details>
  <summary>Employees Whose Manager Left the Company 🔲</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Exchange Seats 🔲</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Movie Rating 🔲</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Restaurant Growth 🔲</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Friend Requests II: Who Has the Most Friends 🔲</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Investments in 2016 🔲</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Department Top Three Salaries 🔲</summary>  
  
  ```sql

  ```

</details>

**7. Advanced String Functions / Regex / Clause**

<details>
  <summary>Fix Names in a Table 🔲</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Patients With a Condition 🔲</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Delete Duplicate Emails 🔲</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Second Highest Salary 🔲</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Group Sold Products By The Date 🔲</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>List the Products Ordered in a Period 🔲</summary>  
  
  ```sql

  ```

</details>

<details>
  <summary>Find Users With Valid E-Mails 🔲</summary>
</details>
