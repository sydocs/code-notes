## Sql Intermediate

### Group By

- `GROUP BY`: Group similar rows and summarise each group.

```sql
      SELECT column1, COUNT(column2)
      FROM table_name
      GROUP BY column1;
```

### Having

- `HAVING`: Filters groups after grouping.

```sql
      SELECT column1, COUNT(*) AS alias_name
      FROM table_name
      GROUP BY column1
      HAVING COUNT(*) > N;
```

<br>

```sql
      SELECT column1, COUNT(column2)
      FROM table_name
      GROUP BY column1
      HAVING COUNT(column2) > 5;
```

### Null

- `IS NULL`: Checks if a column has no value.
- `IS NOT NULL`: Checks if a column has a value.

> IS NULL

```sql
      SELECT column1
      FROM table_name
      WHERE column2 IS NULL;
```

> IS NOT NULL

```sql
      SELECT column1
      FROM table_name
      WHERE column2 IS NOT NULL;
```

> Check NULL

```sql
    SELECT *
    FROM table_name
    WHERE column1 IS NULL;
```

> Replace NULL

```sql
     SELECT COALESCE(column2, 0)
     FROM table_name;
```

### Join

- `JOIN`: Matches rows with the same value in common column.

> Join one column

```sql
    SELECT a.column1, a.column2, b.column3
    FROM table1 a
    JOIN table2 b
    ON a.common_column = b.common_column;
```

> Join multiple columns

```sql
    SELECT a.column1, b.column2
    FROM table1 a
    JOIN table2 b
    ON a.column1 = b.column1 AND a.column2 = b.column2;
```

> Join different operators

```sql
    SELECT a.column1, b.column2
    FROM table1 a
    JOIN table2 b
    ON a.date_column < b.date_column;
```

> Join with aliases

```sql
    SELECT t1.name, t2.salary
    FROM employees t1
    JOIN payroll t2
    ON t1.emp_id = t2.emp_id;
```

> Join with functions

```sql
    SELECT a.column1, b.column2
    FROM table1 a
    JOIN table2 b
    ON YEAR(a.date) = YEAR(b.date);
```

> Join multiple tables

```sql
    SELECT a.col1, b.col2, c.col3
    FROM table1 a
    JOIN table2 b
    ON a.id = b.id
    JOIN table3 c
    ON b.id = c.id;
```

> Join with WHERE

```sql
    SELECT a.col1, b.col2
    FROM table1 a
    JOIN table2 b
    ON a.id = b.id
    WHERE b.status = 'Active';
```

- `INNER JOIN`: Only matching rows from both tables.
- `LEFT JOIN`: All rows from left table; matching rows from right table; NULL if no match.
- `RIGHT JOIN`: All rows from right table; matching rows from left table; NULL if no match.
- `FULL OUTER JOIN`: All rows from both tables; NULL where there’s no match.
- `CROSS JOIN`: Cartesian product of both tables (all combinations).
- `SELF JOIN`: Join a table to itself using aliases.

> Inner Join

```sql
    SELECT column1, column2
    FROM table1
    INNER JOIN table2
    ON table1.column1 = table2.column1;
```

> Left Join

```sql
    SELECT column1, column2
    FROM table1
    LEFT JOIN table2
    ON table1.column1 = table2.column1;
```

> Right Join

```sql
    SELECT column1, column2
    FROM table1
    RIGHT JOIN table2
    ON table1.column1 = table2.column1;
```

> Full Outer Join

```sql
    SELECT table1.column1, table2.column2
    FROM table1
    FULL OUTER JOIN table2
    ON table1.common_column = table2.common_column;
```

> Cross Join

```sql
    SELECT table1.column1, table2.column2
    FROM table1
    CROSS JOIN table2;
```

> Self Join

```sql
    SELECT a.column1, b.column2
    FROM table1 a
    INNER JOIN table1 b
    ON a.common_column = b.common_column;
```

### Case When

- `CASE`: IF...ELSE

```sql
      SELECT column1,
      CASE 
          WHEN condition THEN 'result1'
          WHEN condition THEN 'result2'
          ELSE 'other'
      END AS new_column
      FROM table_name;
```

### Subquery (Where)

```sql
    SELECT column1
    FROM table_name
    WHERE column2 IN (
       SELECT column2
       FROM table_name2
       WHERE condition
    );
```

### Correlated Subquery

```sql 
    SELECT column1
    FROM table_name t1
    WHERE column2 > (
        SELECT AVG(column2)
        FROM table_name t2
        WHERE t1.column1 = t2.column1
    );
```

### Exists

```sql
    SELECT column1
    FROM table_name t1
    WHERE EXISTS (
        SELECT 1
        FROM table_name2 t2
        WHERE t1.column1 = t2.column1
    );
```

### Window Functions (Over)

> ROW_NUMBER

```sql
    SELECT column1,
           ROW_NUMBER() OVER (PARTITION BY column1 ORDER BY column2 DESC) AS rn
    FROM table_name;
```

> RANK

```sql
    SELECT column1,
       RANK() OVER (ORDER BY column2 DESC) AS rank_value
    FROM table_name;
```

### Partition + Aggregation

```sql
    SELECT column1,
           SUM(column2) OVER (PARTITION BY column1) AS total_value
    FROM table_name;
```

### Common Table Expressions

```sql
    WITH temp_table AS (
         SELECT column1, column2
         FROM table_name
         WHERE condition
    )
    SELECT *
    FROM temp_table
    WHERE column2 > 100;
```

<br>

```sql
    SELECT column1 FROM table_name
    UNION ALL
    SELECT column1 FROM table_name2;
```

### Date Functions

```sql
    SELECT DATE(column1) 
    FROM table_name;
```

<br>

```sql
    SELECT strftime('%Y-%m', column1) 
    FROM table_name;
```

### String Functions

```sql
    SELECT UPPER(column1), LOWER(column1)
    FROM table_name;
```

<br>

```sql
    SELECT LENGTH(column1)
    FROM table_name;
```

<br>

```sql
    SELECT SUBSTR(column1, 1, 5)
    FROM table_name;
```