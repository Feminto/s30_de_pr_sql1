# Sql1

1. Problem 1: Big Countries (https://leetcode.com/problems/big-countries/)

    --Solution

    SELECT  name,
            population,
            area
    FROM world
    WHERE area >= 3000000
    OR population >= 25000000;

2. Problem 2: Nth Highest Salary (https://leetcode.com/problems/nth-highest-salary/)

    --Solution

    CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
    BEGIN
    RETURN (
        # Write your MySQL query statement below.
            SELECT  DISTINCT IFNULL(salary,null)
            FROM (SELECT    salary,
                            DENSE_RANK() OVER(ORDER BY salary DESC) AS rnk
                FROM employee
                ) a
            WHERE rnk = N
        );
    END

3. Problem 3: Delete Duplicate Emails (https://leetcode.com/problems/delete-duplicate-emails/)

    --Solution

    DELETE FROM person
    WHERE id NOT IN  
        (SELECT DISTINCT id FROM
            (SELECT id,
                    email,
                    ROW_NUMBER() OVER(PARTITION BY email ORDER BY id) rwn
            FROM person) a
        WHERE rwn = 1
        );