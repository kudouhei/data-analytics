## String

### Methods

- `s.explode()`: Returns a new series with each element on its own line

```python
s = Series(['a', 'b', 'c', 'd'])
s.explode()
# output:
# 0    a
# 1    b
# 2    c
# 3    d
# dtype: object

s = pd.Series([
    ["apple", "banana"],
    ["watermelon"],
    ["grape", "orange", "pear"]
])
s.explode()
# output:
# 0    apple
# 1    banana
# 2    watermelon
# 3    grape
# 4    orange
# 5    pear
# dtype: object
```

- `s.str.contains('a')`: Returns a boolean series indicating whether each element contains the substring 'a'

```python
s = pd.Series(['apple', 'banana', 'melon'])
s.str.contains('a')
# output:
# 0     True
# 1    True
# 2    False
# dtype: bool
```

- `str.get_dummies`: Returns a data frame containing 1s and 0s based on a categorical series

```python
data = {
    'country': [
        'USA',
        'UK;Germany',
        'France',
        'USA;UK',
        'Japan'
    ]
}
s = pd.Series(data['country'])

dummies = s.str.get_dummies(sep=';') # 执行后，会生成一个 DataFrame，其中包含每个国家的列，以及每个国家对应的 1 或 0
print(dummies)

   France  Germany  Japan  UK  USA
0       0        0      0   0    1  # USA
1       0        1      0   1    0  # UK;Germany
2       1        0      0   0    0  # France
3       0        0      0   1    1  # USA;UK
4       0        0      1   0    0  # Japan
```

- `s.isin(['a', 'b'])`: Returns a boolean series indicating whether each element is in the list

```python
s = pd.Series(['apple', 'banana', 'orange', 'grape'])

# 检查哪些水果是 'apple' 或 'banana'
result = s.isin(['apple', 'banana'])
print(result)
# output:
# 0     True
# 1     True
# 2    False
# 3    False
# dtype: bool
```

