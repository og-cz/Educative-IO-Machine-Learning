# DataFrame

### **Chapter Goals**

* Understand what the pandas `DataFrame` object is and how to use it
* Learn to create, manipulate, and modify DataFrames

---

## **A. Introduction to 2-D Data**

A **DataFrame** is the core data structure in **pandas** for working with **tabular (2-D)** data - similar to a spreadsheet or SQL table.

It consists of **rows** and **columns**, where:

* Each **column** is a `Series` (1-D)
* Together they form a **DataFrame** (2-D)

We use the `pd.DataFrame()` constructor to create one.

---

**Code:**

```python
import pandas as pd

df = pd.DataFrame()
print('{}\n'.format(df))

df = pd.DataFrame([5, 6])
print('{}\n'.format(df))

df = pd.DataFrame([[5, 6]])
print('{}\n'.format(df))

df = pd.DataFrame([[5, 6], [1, 3]],
                  index=['r1', 'r2'],
                  columns=['c1', 'c2'])
print('{}\n'.format(df))

df = pd.DataFrame({'c1': [1, 2], 'c2': [3, 4]},
                  index=['r1', 'r2'])
print('{}\n'.format(df))
```

**Output:**

```
Empty DataFrame
Columns: []
Index: []

   0
0  5
1  6

   0  1
0  5  6

    c1  c2
r1   5   6
r2   1   3

    c1  c2
r1   1   3
r2   2   4
```

---

**Explanation:**

* When passing a list of lists, each **inner list** becomes a **row**.
* When using a **dictionary**, keys become **column labels**, and their values (lists) become the **column data**.
* The `index` argument names the rows.
* The `columns` argument names the columns.

---

### **Series vs DataFrame**

* **Series (1D):** like one column of data
* **DataFrame (2D):** a *frame* that holds multiple Series side by side

---

## **B. Upcasting**

When a DataFrame contains mixed types (e.g., integers and floats), **upcasting** occurs automatically *per column*.

**Code:**

```python
upcast = pd.DataFrame([[5, 6], [1.2, 3]])
print('{}\n'.format(upcast))
print(upcast.dtypes)
```

**Output:**

```
     0  1
0  5.0  6
1  1.2  3

0    float64
1      int64
dtype: object
```

**Explanation:**

* The first column is upcast to `float64` because it contains both integers and floats.
* The second column remains `int64` since it contains only integers.
* Upcasting ensures all data in a column share a single compatible data type.

---

## **C. Appending Rows**

To add new rows, we use `pd.concat()` - a flexible function that merges DataFrames or Series.

**Code:**

```python
df = pd.DataFrame([[5, 6], [1.2, 3]])
ser = pd.Series([0, 0], name='r3', index=[0, 1])

print("--- Original DataFrame ---")
print(df)
print("\n--- Original Series ---")
print(ser)

df_appended_series = pd.concat([df, ser.to_frame().T], ignore_index=True)
print("\n--- Appending a Series as a new row ---")
print(df_appended_series)

df2 = pd.DataFrame([[0, 0], [9, 9]])
df_appended_df = pd.concat([df, df2], ignore_index=True)
print("\n--- Appending another DataFrame ---")
print(df_appended_df)
```

**Explanation:**

* `pd.concat([df, ser.to_frame().T])` converts the Series into a one-row DataFrame for proper alignment.
* `ignore_index=True` resets the index to default integers.
* You can concatenate multiple DataFrames or Series at once.

---

## **D. Dropping Data**

You can remove rows or columns with the `.drop()` method.

**Code:**

```python
df = pd.DataFrame({'c1': [1, 2], 'c2': [3, 4], 'c3': [5, 6]}, index=['r1', 'r2'])

# Drop row 'r1'
df_drop = df.drop(labels='r1')
print('{}\n'.format(df_drop))

# Drop columns 'c1' and 'c3'
df_drop = df.drop(labels=['c1', 'c3'], axis=1)
print('{}\n'.format(df_drop))

# Drop using index/columns keywords
df_drop = df.drop(index='r2')
print('{}\n'.format(df_drop))

df_drop = df.drop(columns='c2')
print('{}\n'.format(df_drop))

df_drop = df.drop(index='r2', columns='c2')
print('{}\n'.format(df_drop))
```

**Explanation:**

* `axis=0` (default) → drop rows
* `axis=1` → drop columns
* You can also use `index=` or `columns=` instead of `labels` + `axis`
* Each `.drop()` returns a *new* DataFrame (does not modify in place unless `inplace=True`)

---

# **🧩 Time to Code!**

### **1. Create a DataFrame from a Dictionary**

**Question:**
Create a DataFrame `df` with:

* Columns: `'c1': [0, 1, 2, 3]`, `'c2': [5, 6, 7, 8]`
* Index: `['r1', 'r2', 'r3', 'r4']`

**Answer:**

```python
df = pd.DataFrame({'c1': [0, 1, 2, 3], 'c2': [5, 6, 7, 8]}, index=['r1', 'r2', 'r3', 'r4'])
```

**Output:**

```
    c1  c2
r1   0   5
r2   1   6
r3   2   7
r4   3   8
```

---

### **2. Create a Single-Row DataFrame**

**Question:**
Create `row_df` with one row `[[9, 9]]`, columns `['c1', 'c2']`, and index `['r5']`.

**Answer:**

```python
row_df = pd.DataFrame([[9, 9]], columns=['c1', 'c2'], index=['r5'])
```

**Output:**

```
    c1  c2
r5   9   9
```

---

### **3. Append and Drop Rows**

**Question:**
Append `row_df` to `df`, then drop row `'r2'`.

**Answer:**

```python
df_app = pd.concat([df, row_df])
df_drop = df_app.drop(labels='r2')
```

**Output:**

```
    c1  c2
r1   0   5
r2   1   6
r3   2   7
r4   3   8
r5   9   9

    c1  c2
r1   0   5
r3   2   7
r4   3   8
r5   9   9
```

