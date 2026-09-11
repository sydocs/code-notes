## Sql Basic
### Create Table

```sql
    CREATE TABLE table_name (
    column1 datatype constraints,
    column2 datatype constraints
    );
```

<br>

```sql
    CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    salary DECIMAL(10,2),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
    );
```

### Data Types

- `INT`: whole numbers
- `DECIMAL` (p,s) (total digitals, decimal digitals): Money, Precise Values
- `VARCHAR(n)`: Text
- `TEXT`: Long text
- `DATE`: Date
- `TIMESTAMP`: Date + Time
- `BOOLEAN`: True, False

> Constraints

- `PRIMARY KEY`: Unique ID
- `NOT NULL`: Required field
- `UNIQUE`: No duplicates
- `FOREIGN KEY`: Link tables
- `DEFAULT`: Preset value
- `REFERENCES`: Link between tables

### Comments

```sql
    -- Add sql comment
```

### Drop Table

```sql
    DROP TABLE table_name;
```

### Insert

> Insert data into one row

```sql
    INSERT INTO table_name (column1, column2)
    VALUES ('value1', 'value2');
```

> Insert data into multiple rows

```sql
    INSERT INTO table_name (column1, column2)
    VALUES 
    ('value1', 'value2'),
    ('value3', 'value4');
```

### Update

```sql
    UPDATE table_name
    SET column1 = 'new_value'
    WHERE condition;
```

### Delete

> Delete all

```sql
    DELETE FROM table_name;
```

> Filter and delete

```sql
    DELETE FROM table_name
    WHERE condition;
```

### Alias

> Rename column & table

```sql
    SELECT column1 AS new_name
    FROM table_name AS t;
```

### Alter Table

> Modify an existing table and add a new column1

```sql
      ALTER TABLE table_name
      ADD column1 TEXT;
```

### Select

> Select all columns

```sql 
    SELECT *
    FROM table_name;
```

> Select more than one columns

```sql  
    SELECT column1, column2
    FROM table_name;
```

### Where

- `WHERE`: Filters rows before grouping.

> Filter one condition

```sql
    SELECT column1, column2
    FROM table_name
    WHERE condition;
```

> Filter multiple conditions (AND)

```sql
    SELECT column1
    FROM table_name
    WHERE condition1 AND condition2;
```

> Filter multiple conditions (OR)

```sql
    SELECT column1
    FROM table_name
    WHERE condition1 OR condition2;
```

> Filter multiple conditions (NOT)

```sql
    SELECT column1
    FROM table_name
    WHERE NOT condition;
```

### Order By

> Sort by ASC

```sql
    SELECT column1, column2
    FROM table_name
    ORDER BY column1 ASC;
```

> Sort by DESC

```sql
    SELECT column1, column2
    FROM table_name
    ORDER BY column1 DESC;
```

> Sort by multiple columns

```sql
    SELECT column1, column2
    FROM table_name
    ORDER BY column1 ASC, column2 DESC;
```

### Select, Where, Order by

```sql
    SELECT column1, column2
    FROM table_name
    WHERE condition
    ORDER BY column1;
```

### Limit

- `LIMIT`: How many rows to return

```sql
      SELECT column1
      FROM table_name
      LIMIT 5;
```

### Offset

- `OFFSET`: How many rows to skip

```sql
      SELECT column1
      FROM table_name
      LIMIT 5 OFFSET 10;
```

### Distinct

- `DISTINCT`: Shows only unique values (remove duplicates)

> Select one column

```sql
    SELECT DISTINCT column1
    FROM table_name;
```

> Select multiple columns

```sql
    SELECT DISTINCT column1, column2
    FROM table_name;
```

### Aggregation

- `COUNT(*)`: Counts the number of rows in each group.

> Counts all rows

```sql
    SELECT COUNT(*) 
    FROM table_name;
```

> Counts only rows where column1 is not NULL

```sql
    SELECT COUNT(column1)
    FROM table_name;
```

> Sum

```sql
    SELECT SUM(column1)
    FROM table_name;
```

> Average

```sql
    SELECT AVG(column1)
    FROM table_name;
```

> Minimun & Maximun

```sql
    SELECT MIN(column1), MAX(column1)
    FROM table_name;
```