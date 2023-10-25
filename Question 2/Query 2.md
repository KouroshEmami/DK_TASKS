Answer to question 2:

```
SELECT 
  name,
  salary,
  AVG(salary) OVER (PARTITION BY department) AS avg_department_salary,
  CASE 
    WHEN salary > AVG(salary) OVER (PARTITION BY department) 
    THEN TRUE
    ELSE FALSE
  END AS higher_than_avg,
  CASE 
    WHEN salary > AVG(salary) OVER (PARTITION BY department)
    THEN ROUND(((salary - AVG(salary) OVER (PARTITION BY department)) / AVG(salary) OVER (PARTITION BY department)) * 100, 2)
    ELSE -1
  END AS salary_exceeds_percentage
FROM employees
ORDER BY department, salary DESC;
```
