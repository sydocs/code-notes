## Advanced Sql

### Window Functions (Analytics)

> Row number (unique ranking)

```sql
    SELECT column1,
           ROW_NUMBER() OVER (PARTITION BY column2 ORDER BY column1 DESC) AS rn
    FROM table_name;
```

> Rank (with gaps)

```sql
    SELECT column1,
           RANK() OVER (ORDER BY column1 DESC) AS rnk
    FROM table_name;
```

> Dense rank (no gaps)

```sql
    SELECT column1,
           DENSE_RANK() OVER (ORDER BY column1 DESC) AS drnk
    FROM table_name;
```

> Running total

```sql
    SELECT column1,
           SUM(column2) OVER (ORDER BY column1) AS running_total
    FROM table_name;
```

> Moving average (last 3 rows)

```sql
    SELECT column1,
           AVG(column2) OVER (
               ORDER BY column1
               ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
           ) AS moving_avg
    FROM table_name;
```

### Common Table Expressions

> Basic CTE

```sql
    WITH cte_name AS (
        SELECT column1, column2
        FROM table_name
        WHERE condition
    )
    SELECT *
    FROM cte_name;
```

> Multiple CTEs

```sql
    WITH cte1 AS (
        SELECT column1 FROM table_name
    ),
    cte2 AS (
        SELECT column2 FROM table_name
    )
    SELECT *
    FROM cte1
    JOIN cte2 ON cte1.column1 = cte2.column2;
```

### Recursive Cte

```sql
    WITH RECURSIVE cte_name AS (
        SELECT column1, column2
        FROM table_name
        WHERE condition   -- base case

        UNION ALL

        SELECT t.column1, t.column2
        FROM table_name t
        JOIN cte_name c ON t.column1 = c.column2
    )
    SELECT *
    FROM cte_name;
```

### Subqueries (Advanced)

> Scalar subquery

```sql
    SELECT column1,
           (SELECT MAX(column2) FROM table_name) AS max_val
    FROM table_name;
```

> Correlated subquery

```sql
    SELECT column1
    FROM table_name t1
    WHERE column2 > (
        SELECT AVG(column2)
        FROM table_name t2
        WHERE t1.column1 = t2.column1
    );
```

> EXISTS

```sql
    SELECT column1
    FROM table_name t1
    WHERE EXISTS (
        SELECT 1
        FROM table_name t2
        WHERE t1.column1 = t2.column1
    );
```

### Advanced Joins

> Inner Join

```sql
    SELECT t1.column1, t2.column2
    FROM table_name t1
    JOIN table_name t2
    ON t1.column1 = t2.column2;
```

> Left Join

```sql
    SELECT *
    FROM table_name t1
    LEFT JOIN table_name t2
    ON t1.column1 = t2.column2;
```

> Self Join

```sql
    SELECT a.column1, b.column2
    FROM table_name a
    JOIN table_name b
    ON a.column1 = b.column2;
```

> Cross Join

```sql
    SELECT *
    FROM table_name t1
    CROSS JOIN table_name t2;
```

### Conditional Aggregations

```sql
    SELECT column1,
           SUM(CASE WHEN condition THEN column2 ELSE 0 END) AS conditional_sum,
           COUNT(CASE WHEN condition THEN 1 END) AS conditional_count
    FROM table_name
    GROUP BY column1;
```

### Pivoting (Manual)

```sql
    SELECT column1,
           SUM(CASE WHEN column2 = 'A' THEN column3 ELSE 0 END) AS A_total,
           SUM(CASE WHEN column2 = 'B' THEN column3 ELSE 0 END) AS B_total
    FROM table_name
    GROUP BY column1;
```

### De-Duplication

> Keep latest row per group

```sql
    WITH ranked AS (
        SELECT *,
               ROW_NUMBER() OVER (
                   PARTITION BY column1
                   ORDER BY column2 DESC
               ) AS rn
        FROM table_name
    )
    SELECT *
    FROM ranked
    WHERE rn = 1;
```

### Advanced Filtering

> BETWEEN

```sql
    SELECT *
    FROM table_name
    WHERE column1 BETWEEN value1 AND value2;
```

> IN

```sql
    SELECT *
    FROM table_name
    WHERE column1 IN (value1, value2);
```

> LIKE

```sql
    SELECT *
    FROM table_name
    WHERE column1 LIKE '%pattern%';
```

### Set Operations

> UNION (remove duplicates)

```sql
    SELECT column1 FROM table_name
    UNION
    SELECT column1 FROM table_name;
```

> UNION ALL (keep duplicates)

```sql
    SELECT column1 FROM table_name
    UNION ALL
    SELECT column1 FROM table_name;
```

> INTERSECT

```sql
    SELECT column1 FROM table_name
    INTERSECT
    SELECT column1 FROM table_name;
```

> EXCEPT

```sql
    SELECT column1 FROM table_name
    EXCEPT
    SELECT column1 FROM table_name;
```

### Performance Optimization

> Index

```sql
    CREATE INDEX idx_name
    ON table_name (column1);
```

> Explain query plan

```sql
    EXPLAIN QUERY PLAN
    SELECT *
    FROM table_name
    WHERE column1 = value;
```

### Advanced Date Handling

> Extract year

```sql
    SELECT strftime('%Y', column1) AS year
    FROM table_name;
```
> Date difference

```sql
    SELECT julianday('now') - julianday(column1) AS days_diff
    FROM table_name;
```