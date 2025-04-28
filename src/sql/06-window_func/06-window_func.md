## Window Functions

The following is the basic syntax of a window function:

```sql
SELECT {columns},
{window_func} OVER (PARTITION BY {partition_key} ORDER BY {order_key})
FROM table1;
```

### NOTES

**What Is the PARTITION BY Clause in SQL?**

The SQL PARTITION BY expression is a subclause of the OVER clause, which is used in almost all invocations of window functions like `AVG()`, `MAX()`, and `RANK()`.

The first thing to focus on is the syntax. Here’s how to use the SQL `PARTITION BY` clause:

```sql
SELECT
    <column>,
    <window function> OVER(PARTITION BY <column> [ORDER BY <column>])
FROM table;
```

Example:


    | car_make | car_model | car_price | average_make |
    |----------|-----------|-----------|--------------|
    | Citroen  | Picasso   | 23400     | 21200        |
    | Citroen  | Cactus    | 19000     | 21200        |
    | Ford     | Galaxy    | 12400     | 13196        |
    | Ford     | Falcon    | 8990      | 13196        |
    | Ford     | Mondeo    | 18200     | 13196        |
    | Renault  | Megane    | 14300     | 15400        |
    | Renault  | Fuego     | 16500     | 15400        |


As an example, say we want to obtain the average price and the top price for each make. Use the following query:

```sql
SELECT
    car_make,
    AVG(car_price) AS average_price,
    MAX(car_price) AS max_price
FROM car_sales
GROUP BY car_make;

## output:
| car_make | average_price | max_price |
|----------|---------------|-----------|
| Citroen  | 21200         | 23400     |
| Ford     | 13196         | 18200     |
| Renault  | 15400         | 16500     |
```

You cannot do this by using GROUP BY, because the individual records of each model are collapsed due to the clause GROUP BY `car_make`.

```sql
SELECT
  car_make,
  car_model,
  car_price,
  AVG(car_price) OVER (PARTITION BY car_make) AS average_make
FROM car_list_prices;

## output:
| car_make | car_model | car_price | average_make |
|----------|-----------|-----------|--------------|
| Citroen  | Picasso   | 23400     | 21200        |
| Citroen  | Cactus    | 19000     | 21200        |
| Ford     | Galaxy    | 12400     | 13196        |
| Ford     | Falcon    | 8990      | 13196        |
| Ford     | Mondeo    | 18200     | 13196        |
| Renault  | Megane    | 14300     | 15400        |
| Renault  | Fuego     | 16500     | 15400        |

```

### Statistics with Window Functions

- `ROW_NUMBER()`: is one of the most useful window functions in SQL that assigns a unique sequential number to each row in your result set.
- 始终生成唯一序号(1,2,3...)，即使排序值相同也会分配不同序号

```sql
SELECT 
    column_name,
    ROW_NUMBER() OVER (
        [PARTITION BY group_column]  -- Optional: Restart numbering for each group
        ORDER BY sort_column         -- Required: How to order rows before numbering
    ) AS row_num_column
FROM table_name;
```

**Example** 1: Numbering Within Groups

```sql
-- 在每个部门内，按工资高低给员工编号
SELECT 
    department,
    employee_name,
    salary,
    ROW_NUMBER() OVER (
        PARTITION BY department
        ORDER BY salary DESC
    ) AS dept_salary_rank
FROM employees;

## output format:
| department | employee_name | salary | dept_salary_rank |
|------------|---------------|--------|------------------|
| Sales      | John          | 50000  | 1                |
| Sales      | Jane          | 45000  | 2                |  
| Sales      | Jim           | 40000  | 3                |
| Marketing  | John          | 55000  | 1                |
| Marketing  | Jane          | 50000  | 2                |

```

**Example** 2: Top N per Group

```sql
-- 找出每个部门工资前三的员工
SELECT * FROM (
    SELECT 
        department,
        employee_name,
        salary,
        ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS rn
    FROM employees
) t WHERE rn <= 2;

## output format:
| department | employee_name | salary | rn |
|------------|---------------|--------|----|
| Sales      | John          | 50000  | 1  |
| Sales      | Jane          | 45000  | 2  |
| Marketing  | John          | 55000  | 1  |
| Marketing  | Jane          | 50000  | 2  |

```

- `RANK()`: RANK() is a window function in SQL that assigns ranks to rows with special handling for tied values.
- 相同排名，跳过后续序号	不连续	1,2,2,4

```sql
SELECT 
    student_name,
    score,
    RANK() OVER (ORDER BY score DESC) AS score_rank
FROM exam_results;
```


