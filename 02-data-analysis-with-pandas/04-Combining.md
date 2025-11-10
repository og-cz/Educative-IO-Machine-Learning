# Combining

### **Chapter Goals**

* Understand different methods for combining DataFrame objects
* Write code for concatenating and merging DataFrames

---

## **A. Concatenation**

To combine multiple DataFrames either **by rows** or **by columns**, we use [`pd.concat()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.concat.html).
It works similarly to `np.concatenate()` in NumPy but is more flexible and DataFrame-aware.

---

**Code:**

```python
import pandas as pd

df1 = pd.DataFrame({'c1': [1, 2], 'c2': [3, 4]},
                   index=['r1', 'r2'])
df2 = pd.DataFrame({'c1': [5, 6], 'c2': [7, 8]},
                   index=['r1', 'r2'])
df3 = pd.DataFrame({'c1': [5, 6], 'c2': [7, 8]})

concat = pd.concat([df1, df2], axis=1)
print('{}\n'.format(concat))

concat = pd.concat([df2, df1, df3])
print('{}\n'.format(concat))

concat = pd.concat([df1, df3], axis=1)
print('{}\n'.format(concat))
```

**Output:**

```
    c1  c2  c1  c2
r1   1   3   5   7
r2   2   4   6   8

    c1  c2
r1   5   7
r2   6   8
r1   1   3
r2   2   4
0    5   7
1    6   8

     c1   c2   c1   c2
r1  1.0  3.0  NaN  NaN
r2  2.0  4.0  NaN  NaN
0   NaN  NaN  5.0  7.0
1   NaN  NaN  6.0  8.0
```

---

**Explanation:**

* `pd.concat([df1, df2])` stacks the DataFrames vertically (row-wise) by default.
* `axis=1` combines them side-by-side (column-wise).
* Mismatched **row indices** create missing values (`NaN`) where data doesn’t align.
* When combining, you can use options like:

  * `ignore_index=True` → reset row indices
  * `keys=['df1', 'df2']` → add hierarchical index labels

---

## **B. Merging**

Besides concatenation, you can **merge** DataFrames using [`pd.merge()`](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.merge.html).
This works similarly to SQL joins — combining rows based on **common columns** or **keys**.

---

**Code:**

```python
mlb_df1 = pd.DataFrame({
    'name': ['john doe', 'al smith', 'sam black', 'john doe'],
    'pos': ['1B', 'C', 'P', '2B'],
    'year': [2000, 2004, 2008, 2003]
})

mlb_df2 = pd.DataFrame({
    'name': ['john doe', 'al smith', 'jack lee'],
    'year': [2000, 2004, 2012],
    'rbi': [80, 100, 12]
})

print('{}\n'.format(mlb_df1))
print('{}\n'.format(mlb_df2))

mlb_merged = pd.merge(mlb_df1, mlb_df2)
print('{}\n'.format(mlb_merged))
```

**Output:**

```
        name pos  year
0   john doe  1B  2000
1   al smith   C  2004
2  sam black   P  2008
3   john doe  2B  2003

        name   year  rbi
0   john doe   2000   80
1   al smith   2004  100
2   jack lee   2012   12

       name pos  year  rbi
0  john doe  1B  2000   80
1  al smith   C  2004  100
```

---

**Explanation:**

* `pd.merge(df1, df2)` merges rows using **all common columns** (default behavior).
* Only rows with matching values in those common columns are merged.
* In the example, both DataFrames share `'name'` and `'year'`, so:

  * `'john doe'` (2000) and `'al smith'` (2004) appear in both → merged.
  * Other rows without matches are **excluded** by default (inner join).

You can control join behavior using the `how` argument:

```python
pd.merge(df1, df2, how='left')
pd.merge(df1, df2, how='right')
pd.merge(df1, df2, how='outer')
pd.merge(df1, df2, how='inner')  # default
```

---

# 🧩 **Time to Code!**

### **1. Concatenate Rows**

**Question:**
Write a function `concat_rows(df1, df2)` that concatenates two DataFrames vertically (by rows).

**Answer:**

```python
def concat_rows(df1, df2):
    row_concat = pd.concat([df1, df2])
    return row_concat
```

**Output:**

```
   0  1   2
0  1  5   3
1 -9  0   1
2  7  5  -8
0  9  2   3
1 -1  1  -2
2  0  0  19
```

---

### **2. Concatenate Columns**

**Question:**
Write a function `concat_cols(df1, df2)` that concatenates two DataFrames horizontally (by columns).

**Answer:**

```python
def concat_cols(df1, df2):
    col_concat = pd.concat([df1, df2], axis=1)
    return col_concat
```

**Output:**

```
   0  1  2  0  1   2
0  1  5  3  9  2   3
1 -9  0  1 -1  1  -2
2  7  5 -8  0  0  19
```

---

### **3. Merge Two DataFrames**

**Question:**
Write a function `merge_dfs(df1, df2)` that merges two DataFrames based on common columns.

**Answer:**

```python
def merge_dfs(df1, df2):
    merged_df = pd.merge(df1, df2)
    return merged_df
```

**Output:**

```
       name pos  year  rbi
0  john doe  1B  2000   80
1  al smith   C  2004  100
```


