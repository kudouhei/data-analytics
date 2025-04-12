# Grouping, joining, and sorting

### Methods for grouping data

- `df.sort_index` Reorder the rows of a data frame based on the values in its index, in ascending order

- `df.sort_values` Reorder the rows of a data frame based on the values in one or more specified columns

```python
df = df.sort_values('distance')
```

- `df.transpose() or df.T` Returns a new data frame with the same values as df but with the columns and index exchanged

```python
df = df.transpose()
```

- `df.diff()` For a given data frame, indicates the difference between each cell and the corresponding cell in the previous row

```python
df = df.diff()
```

- `df.groupby()` Allows us to invoke on or more aggregate methods for each value in a particular column.

```python
df = df.groupby('column_name')
```

- `df.assign` Adds one or more columns to a data frame
  
```python
df.assign(a=df['x']*3)
```


