# Indexing in DataFrames

## **Chapter Goals**

* Learn how to index a DataFrame to retrieve rows and columns
* Write code for indexing a DataFrame

---

## **A. Direct Indexing**

When indexing a DataFrame, you can treat it like a dictionary of **Series** objects - each column is a Series, and column labels act as dictionary keys.

### **Code:**

```python
df = pd.DataFrame({'c1': [1, 2], 'c2': [3, 4],
                   'c3': [5, 6]}, index=['r1', 'r2'])

col1 = df['c1']
print('{}\n'.format(col1))

col1_df = df[['c1']]
print('{}\n'.format(col1_df))

col23 = df[['c2', 'c3']]
print('{}\n'.format(col23))
```

### **Explanation:**

* `df['c1']` returns a **Series** (single column).
* `df[['c1']]` returns a **DataFrame** (subset of one column).
* Passing multiple columns returns a DataFrame with those columns.

---

### **Code (Row Indexing):**

```python
df = pd.DataFrame({'c1': [1, 2, 3], 'c2': [4, 5, 6],
                   'c3': [7, 8, 9]}, index=['r1', 'r2', 'r3'])

print(df[0:2])       # integer slice
print(df['r2':'r3']) # label slice
```

### **Explanation:**

* Integer slicing (`0:2`) is **exclusive** of the end index.
* Label slicing (`'r2':'r3'`) is **inclusive** of the end label.
* Retrieving a single row via `df['r1']` raises a **KeyError**, since `df[]` looks for **columns**, not rows.

---

## **B. Using `iloc`**

The `.iloc` property retrieves rows by **integer position**.

### **Code:**

```python
df = pd.DataFrame({'c1': [1, 2, 3], 'c2': [4, 5, 6],
                   'c3': [7, 8, 9]}, index=['r1', 'r2', 'r3'])

print(df.iloc[1])           # single row as Series
print(df.iloc[[0, 2]])      # multiple rows
print(df.iloc[[False, True, True]])  # boolean mask
```

### **Explanation:**

* `iloc[1]` → returns **Series** (row 2).
* `iloc[[0,2]]` → returns **DataFrame** with rows 1 & 3.
* Boolean mask allows filtering rows.

---

## **C. Using `loc`**

The `.loc` property retrieves data by **label** (index names).

### **Code:**

```python
df = pd.DataFrame({'c1': [1, 2, 3], 'c2': [4, 5, 6],
                   'c3': [7, 8, 9]}, index=['r1', 'r2', 'r3'])

print(df.loc['r2'])                        # Single row
print(df.loc[['r1', 'r3'], 'c2'])          # Specific rows and column
df.loc[['r1', 'r3'], 'c2'] = 0             # Modify values
print(df)
```

### **Explanation:**

* `.loc` allows **row and column** access together.
* `.loc[row_labels, column_labels]` works like 2D indexing in NumPy.
* Can **read or assign** data.

---

# 🧩 **Time to Code!**

### **1. Direct Indexing**

**Question:**
Get the first column and the first two rows of `df`.

**Answer:**

```python
col_1 = df['c1']
row_12 = df[0:2]
```

**Output:**

```
r1     1
r2    18
r3    19
r4    20
Name: c1, dtype: int64

    c1  c2  c3
r1   1  -9   1
r2  18   0   2
```

---

### **2. Integer Indexing with `iloc`**

**Question:**
Retrieve the **first** and **third** rows of `df`.

**Answer:**

```python
row_13 = df.iloc[[0, 2]]
```

**Output:**

```
    c1  c2  c3
r1   1  -9   1
r3  19   0   7
```

---

### **3. Label Indexing with `loc`**

**Question:**
Set the **second column (`c2`)** of the **third and fourth rows (`r3`, `r4`)** to `12`.

**Answer:**

```python
df.loc[['r3','r4'], 'c2'] = 12
```

**Output:**

```
12, 12
```

