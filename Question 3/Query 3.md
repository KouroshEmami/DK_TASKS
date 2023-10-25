Answer to question 3
```
SELECT *,
       (ROW_NUMBER() OVER (ORDER BY nmv)) AS rank,
       (CASE
           WHEN (ROW_NUMBER() OVER (ORDER BY nmv)) > id THEN 
               (nmv +
                COALESCE((LAG(nmv, 3) OVER (ORDER BY id)), 0) +
                COALESCE((LAG(nmv, 2) OVER (ORDER BY id)), 0) +
                COALESCE((LAG(nmv, 1) OVER (ORDER BY id)), 0))
           ELSE nmv
       END) AS calculation
FROM customer
ORDER BY id;
```
