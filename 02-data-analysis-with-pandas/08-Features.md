# Features

Learn how to identify and work with different types of features in a dataset - both **quantitative** and **categorical** - and how to manipulate them in pandas.

---

## **Chapter Goals**

* Understand the difference between **quantitative** and **categorical** features
* Learn methods to manipulate and add features to a `DataFrame`
* Write code to calculate and add baseball statistics to a dataset

---

## **A. Quantitative vs. Categorical Features**

We often call the **columns** of a `DataFrame` the **features** of the dataset it represents.
Each feature can be either **quantitative** or **categorical**.

---

### **Quantitative Features**

A **quantitative feature** can be *measured numerically*.
Examples:

* Height
* Weight
* Age
  These features support mathematical operations such as `sum`, `mean`, or `average`.

---

### **Categorical Features**

A **categorical feature** describes *groups or categories* rather than numeric values.
Examples:

* Gender
* Team name
* City or birthplace

Categorical features are best used with functions like `groupby` to organize and summarize data.

---

### **Context Matters**

Some features can act as either:

* **Quantitative** → e.g., calculating average birth year
* **Categorical** → e.g., grouping by birth year

Quantitative and categorical data types represent **distinct kinds of information**:

* **Quantitative:** numeric, measurable quantities
* **Categorical:** labels or names that classify items

---

## **B. Quantitative Features in pandas**

In the previous chapter, you used `groupby()` to summarize **categorical** groups.
Now, we’ll focus on operations for **quantitative** features using built-in pandas functions.

Two important functions for numerical data are:

* [`sum()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sum.html)
* [`mean()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.mean.html)

---

### **Example: Summing and Averaging Across Rows and Columns**

```python
import pandas as pd

df = pd.DataFrame({
  'T1': [10, 15, 8],
  'T2': [25, 27, 25],
  'T3': [16, 15, 10]
})

print('{}\n'.format(df))

print(df.sum())        # Sum down each column (axis=0)
print(df.sum(axis=1))  # Sum across each row  (axis=1)
print(df.mean())       # Mean down each column
print(df.mean(axis=1)) # Mean across each row
```

**Output:**

```
   T1  T2  T3
0  10  25  16
1  15  27  15
2   8  25  10

T1    33
T2    77
T3    41
dtype: int64

0    51
1    57
2    43
dtype: int64
```

---

### **Axis Reminder**

| Axis     | Direction    | Meaning                  |
| -------- | ------------ | ------------------------ |
| `axis=0` | ↓ vertical   | Operate down each column |
| `axis=1` | → horizontal | Operate across each row  |

* `sum()` or `mean()` without specifying `axis` defaults to `axis=0` (columns).
* Use `axis=1` to summarize each row instead.

---

## **C. Weighted Features**

Sometimes you may want to **apply different weights** to features before aggregating them.
This is done using the [`multiply()`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.multiply.html) function.

---

### **Example: Applying Weights**

```python
df = pd.DataFrame({
  'T1': [0.1, 150.],
  'T2': [0.25, 240.],
  'T3': [0.16, 100.]
})

print('{}\n'.format(df))

print(df.multiply(2))                          # Multiply all values by 2
df_ms = df.multiply([1000, 1], axis=0)         # Multiply first row by 1000
print(df_ms)

df_w = df_ms.multiply([1, 0.5, 1])             # Apply column weights
print(df_w)
print(df_w.sum(axis=1))                        # Weighted sums
```

**Output:**

```
      T1      T2      T3
0    0.1    0.25    0.16
1  150.0  240.00  100.00

      T1     T2      T3
0    0.2    0.5    0.32
1  300.0  480.0  200.00

      T1     T2     T3
0  100.0  250.0  160.0
1  150.0  240.0  100.0

      T1     T2     T3
0  100.0  125.0  160.0
1  150.0  120.0  100.0

0    385.0
1    370.0
dtype: float64
```

---

### **Explanation**

* The first processor’s values were converted from seconds → milliseconds (`×1000`).
* Then column `T2` was halved (`×0.5`) because two processors ran that test.
* The final row sums give **weighted totals** for each processor.

---

## **Time to Code! ⚾**

We’ll now use these ideas to calculate **baseball statistics** from MLB data.

### **Helper Function**

```python
def col_list_sum(df, col_list, weights=None):
    col_df = df[col_list]
    if weights is not None:
        col_df = col_df.multiply(weights)
    return col_df.sum(axis=1)
```

* `df` → input DataFrame
* `col_list` → list of columns to sum
* `weights` → optional list of weight values

---

### **1️⃣ Calculate Batting Average**

**Task:**
Set `mlb_df['BA']` equal to hits (`'H'`) divided by at-bats (`'AB'`).

```python
mlb_df['BA'] = mlb_df['H'] / mlb_df['AB']
```

**Output:**

```
[0.4201, 0.3174, 0.3475, 0.2747, 0.4246, 0.4177, 0.3326, 0.3275, 0.2230]
```

---

### **2️⃣ Calculate Singles**

**Task:**

* Set `other_hits` = sum of doubles, triples, and home runs
* Set `mlb_df['1B']` = total hits - other hits

```python
other_hits = col_list_sum(mlb_df, ['2B', '3B', 'HR'])
mlb_df['1B'] = mlb_df['H'] - other_hits
```

**Output:**

```
[295, 388, 164, 248, 226, 304, 451, 306, 430]
```

---

### **3️⃣ Calculate Weighted Hits (for Slugging Percentage)**

**Task:**
Compute a weighted sum for singles, doubles, triples, and home runs.
Weights: `[1, 2, 3, 4]`.

```python
weighted_hits = col_list_sum(
    mlb_df, ['1B', '2B', '3B', 'HR'], weights=[1, 2, 3, 4]
)
```

**Output:**

```
[4357, 3909, 5066, 4449, 4476, 4297, 4183, 4371, 4045]
```

---

### **4️⃣ Calculate Slugging Percentage**

**Task:**
Set `mlb_df['SLG']` equal to `weighted_hits` divided by at-bats (`'AB'`).

```python
mlb_df['SLG'] = weighted_hits / mlb_df['AB']
```

**Output:**

```
[1.263, 0.889, 1.101, 0.806, 1.288, 1.251, 0.931, 0.980, 0.629]
```


