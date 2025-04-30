
### Using LIKE and ILIKE with WHERE

**Percent sign (%)**: A wildcard matching `one or more characters`
**Underscore (_)**: A wildcard matching just `one character`

```sql
LIKE 'b%' # Starts with b
LIKE '%ak%' # Contains ak
LIKE '_aker' # 5 characters long, 3rd character is a
LIKE 'ba_er' # 5 characters long, 2nd and 5th characters are a and r
```

### COPY command

The `COPY` command in PostgreSQL is a powerful utility for efficiently transferring data between database tables and the filesystem.

Example:

- Basic Import/Export
```sql
-- Export table data to CSV
COPY employees TO '/path/to/employees.csv' WITH CSV HEADER;

-- Import data from CSV
COPY employees FROM '/path/to/employees.csv' WITH CSV HEADER;
```

- Column-Specific Operations

```sql
-- Export specific columns
COPY (SELECT id, name FROM employees) TO '/path/to/employees_subset.csv' WITH CSV HEADER;

-- Import specific columns
COPY employees (id, name) FROM '/path/to/employees_subset.csv' WITH CSV HEADER;
```

- Export Query Results

```sql
-- Export query results to CSV
COPY (SELECT * FROM employees WHERE department = 'Sales') TO '/path/to/sales_employees.csv' WITH CSV HEADER;
```

### INTERSECT and EXCEPT

- `INTERSECT`: Returns rows that are in both queries
- `EXCEPT`: Returns rows that are in one query but not in the other

```sql
-- 找出VIP客户中最近有消费但未使用优惠券的客户
(SELECT 客户ID FROM VIP客户表
 INTERSECT
 SELECT 客户ID FROM 最近消费表)
EXCEPT
SELECT 客户ID FROM 优惠券使用表;
```


