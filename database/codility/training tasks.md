# [_Training tasks_](https://app.codility.com/programmers/trainings/6/)
`PostgreSQL 9.4`
## _SqlSum : Calculate sum of elements._
```sql
-- return the sum of the numbers in column v.

SELECT sum(v)
FROM elements
```

## _SqlEventsDelta : Compute the difference between the latest and the second latest value for each event type._
```
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
