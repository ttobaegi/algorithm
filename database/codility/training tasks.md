# [_Training tasks_](https://app.codility.com/programmers/trainings/6/)
`PostgreSQL 9.4`
## _SqlSum : Calculate sum of elements._
```sql
-- return the sum of the numbers in column v.

SELECT sum(v)
FROM elements
```

## _SqlEventsDelta : Compute the difference between the latest and the second latest value for each event type._
```sql
WITH CTE1 AS(
        SELECT event_type,
        COUNT(event_type) AS cnt
    FROM events
    GROUP BY 1
)
, CTE2 AS (
    SELECT 
        event_type, 
        -- latest = ORDER BY time DESC
        value - LEAD(value) OVER(PARTITION BY event_type ORDER BY time DESC) AS value,
        ROW_NUMBER() OVER(PARTITION BY event_type ORDER BY time DESC) AS row_num
    FROM events
    WHERE 
        event_type IN ( 
            SELECT event_type 
            FROM CTE1
            WHERE cnt >=2
        )
)
SELECT event_type, value
FROM CTE2
WHERE row_num = 1
ORDER BY 1
```
## _SqlWorldCup : Given a list of matches in a group stage of the soccer World Cup, compute the number of points each team currently has._
```sql

-- Compute the total number of points each team has scored after all the matches
WITH HOST AS (
    SELECT host_team AS team_id,
        SUM(CASE WHEN host_goals > guest_goals THEN 3 
            WHEN host_goals = guest_goals THEN 1
            ELSE 0 
        END) AS num_points 
    FROM matches 
    GROUP BY 1
)
, GUEST AS (
    SELECT guest_team AS team_id,
        SUM(CASE WHEN (host_goals < guest_goals) THEN 3 
            WHEN host_goals = guest_goals THEN 1
            ELSE 0
        END) AS num_points
    FROM matches 
    GROUP BY 1
)
, CTE AS (
    SELECT * FROM HOST
    UNION ALL -- 중복허용
    SELECT * FROM GUEST
)
-- team_id | team_name | num_points
SELECT 
    t.team_id,
    t.team_name,
    -- IF NULL : 0 
    COALESCE(SUM(num_points),0) AS num_points 
FROM teams  t 
-- LEFT OUTER JOIN 
LEFT OUTER JOIN CTE c ON c.team_id = t.team_id
GROUP BY 1,2
-- ordered by num_points(in decreasing), team_id (in increasing)
ORDER BY 3 DESC, 1
```
