# Series 

In this section, you’ll learn about the **pandas Series object**, which represents **1-dimensional labeled data**.
You’ll create and explore Series objects, understand their indexing, and see how to construct them using lists, arrays, and dictionaries.

---

### **A. Creating Series**

**Code:**

```python
import pandas as pd
import numpy as np

# Creating an empty Series (avoid DeprecationWarning by specifying dtype)
series = pd.Series(dtype='float64')
print('{}\n'.format(series))

series = pd.Series(5)
print('{}\n'.format(series))

series = pd.Series([1, 2, 3])
print('{}\n'.format(series))

series = pd.Series([1, 2.2])  # upcasting
print('{}\n'.format(series))

arr = np.array([1, 2])
series = pd.Series(arr, dtype=np.float32)
print('{}\n'.format(series))

series = pd.Series([[1, 2], [3, 4]])
print('{}\n'.format(series))
```

**Explanation:**
A **Series** is a 1-D array-like structure that can store any data type (integers, floats, objects, etc.).
It is created using the `pd.Series()` constructor.

* The `data` argument specifies the Series values.
* The `dtype` argument sets the data type manually (similar to NumPy).
* Series automatically display **index labels** on the left and **values** on the right.

**Output:**

```
Series([], dtype: float64)

0    5
dtype: int64

0    1
1    2
2    3
dtype: int64

0    1.0
1    2.2
dtype: float64

0    1.0
1    2.0
dtype: float32

0    [1, 2]
1    [3, 4]
dtype: object
```

**Note:**
Series are always 1-D. When you pass lists inside, each list becomes a single element - not a 2-D matrix.

---

### **B. Index**

**Code:**

```python
series = pd.Series([1, 2, 3], index=['a', 'b', 'c'])
print('{}\n'.format(series))

series = pd.Series([1, 2, 3], index=['a', 8, 0.3])
print('{}\n'.format(series))
```

**Explanation:**
Every Series has an **index**, which labels each element.

* By default, pandas assigns a numeric index (0, 1, 2, …).
* You can set a custom index using the `index` keyword argument.
* The index must have the same length as the data.
* Index labels can be strings, integers, or floats - as long as they’re hashable.

**Output:**

```
a    1
b    2
c    3
dtype: int64

a      1
8      2
0.3    3
dtype: int64
```

---

### **C. Dictionary Input**

**Code:**

```python
series = pd.Series({'a': 1, 'b': 2, 'c': 3})
print('{}\n'.format(series))

series = pd.Series({'b': 2, 'a': 1, 'c': 3})
print('{}\n'.format(series))
```

**Explanation:**
When you pass a **dictionary** to `pd.Series`,

* The **keys** become index labels.
* The **values** become Series elements.
  The order of keys in the dictionary determines the output order (unless the dictionary is unordered, as in older Python versions).

**Output:**

```
a    1
b    2
c    3
dtype: int64

b    2
a    1
c    3
dtype: int64
```

---

# **Time to Code!**

### **1. Create a basic Series**

**Question:**
Create a Series `s1` from the list `[1, 3, 5.2]`.

**Answer:**

```python
s1 = pd.Series([1, 3, 5.2])
print(s1)
```

**Output:**

```
0    1.0
1    3.0
2    5.2
dtype: float64
```

---

### **2. Perform element-wise multiplication**

**Question:**
Create a new Series `s2` by multiplying `s1` by `[0.1, 0.2, 0.3]`.

**Answer:**

```python
s2 = s1 * [0.1, 0.2, 0.3]
print(s2)
```

**Output:**

```
0    0.10
1    0.60
2    1.56
dtype: float64
```

---

### **3. Create a Series with custom index**

**Question:**
Create a Series `s3` from `[1, 3, 8, np.nan]` with index `['a', 'b', 'c', 'd']`.

**Answer:**

```python
s3 = pd.Series([1, 3, 8, np.nan], index=['a', 'b', 'c', 'd'])
print(s3)
```

**Output:**

```
a    1.0
b    3.0
c    8.0
d    NaN
dtype: float64
```

---

### **4. Create a Series from a dictionary**

**Question:**
Create a Series `s4` using a dictionary `{'a': 0, 'b': 1, 'c': 2}`.

**Answer:**

```python
s4 = pd.Series({'a': 0, 'b': 1, 'c': 2})
print(s4)
```

**Output:**

```
a    0
b    1
c    2
dtype: int64
```

