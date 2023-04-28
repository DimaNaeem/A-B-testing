# A-B-testing
The project features review inferential statistics and create analysis plan to analyze the A/B test results to determine whether or not the experiment was successful.

#### TOOLS USED : SQL, PYTHON

SQL

1.What is the average amount spent per user for the control and treatment groups?

WITH total_per_user AS (
    SELECT uid, SUM (spent) AS total_spent
    from activity 
    group by uid)
    select g."group", AVG(coalesce(total_spent,0))
    from groups g
    left join  total_per_user a 
    on g.uid = a.uid
    GROUP by g."group";
    
Control: $3.375, Treatment: $3.391


2.How many users in control group from CANADA?

SELECT count(*) 
 FROM users u
 join groups g
   on u.id = g.uid
   where g.group = 'A' and country = 'CAN';


767

3. What was the conversion rate of all users?

SELECT COUNT (Distinct uid) AS total_converted_users,
  (SELECT COUNT(Distinct id) FROM users) AS total_users,
  COUNT (DISTINCT uid) *100.0 / (SELECT COUNT (DISTINCT id) FROM users) AS conversion_rate
  
FROM activity;

4.28%

4. As of February 1st, 2023, how many users were in the A/B test?

SELECT COUNT(*) as total_users
FROM groups
where join_dt <= '2023-02-01' and "group" IN ('A', 'B');


 41,412


