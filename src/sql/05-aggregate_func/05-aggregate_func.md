## Aggregate Functions

The most frequently used aggregate functions include `SUM()`, `AVG()`, `MIN()`, `MAX()`, `COUNT()`, `CORR()`, and `STDDEV()`.

- The GROUP BY statements usually have the following structure:

```sql
SELECT
  {KEY},
  {AGGFUNC(column1)}
FROM
  {table1}
GROUP BY
  {KEY}
```

- The aggregates can also be ordered using `ORDER BY` clause.

```sql
SELECT state, COUNT(*)
FROMcustomers
GROUP BY state
ORDER BY COUNT(*);
```

### Multiple-column GROUP BY

The `GROUP BY` clause can also include multiple columns.

**Grouping Sets**
a SQL feature that allows you to perform multiple grouping operations in a single query. It is a way to group data by different combinations of columns and perform aggregate functions on the grouped data.

Task:
For instance, say you wanted to count the total number of customers you have in each state, while simultaneously, you also wanted the total number of male and female customers you have in each state. 

- UNION ALL: 快，不检查重复，直接合并

```sql
(
  SELECT state, NULL as gender, COUNT(*)
  FROM customers
  GROUP BY 1
  ORDER BY 1
)
UNION ALL 
(
  SELECT state, gender, COUNT(*)
  FROM customers
  GROUP BY 1, 2
  ORDER BY 1, 2
)
ORDER BY 1, 2;
```

- GROUPING SETS: 

```sql
-- 同时统计：按产品分类的销售额、按地区的销售额、总计销售额
SELECT 
    product_category, 
    region, 
    SUM(sales) AS total_sales
FROM sales_data
GROUP BY GROUPING SETS (
    (product_category),  -- 按产品分类统计
    (region),           -- 按地区统计
    ()                  -- 总计, 空括号表示总计(不分组)
);
```

```sql
SELECT state, gender, COUNT(*)
FROM customers
GROUP BY GROUPING SETS (
    (state), 
    (state, gender)
);
ORDER BY 1, 2;
```

- To use the **filter on aggregate functions**, you need to use a new clause: `HAVING`. The `HAVING` clause is similar to the `WHERE` clause, except it is specifically designed for `GROUP BY` queries. It applies the filter condition on the aggregated groups instead of the original dataset. 

```sql
SELECT 列名, 聚合函数(列名)
FROM 表名
GROUP BY 列名
HAVING 条件;
```

```sql
SELECT state, gender, COUNT(*)
FROM customers
GROUP BY GROUPING SETS (
    (state), 
    (state, gender)
)
HAVING COUNT(*) > 10;
```



