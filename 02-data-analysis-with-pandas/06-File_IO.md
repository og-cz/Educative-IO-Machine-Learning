# File I/O

## **Chapter Goals**

* Learn how to handle file input/output using pandas
* Write code to process and save data files

---

## **A. Reading Data**

pandas can read and write from a wide range of file formats - including **CSV**, **Excel (XLSX)**, and **JSON**.
Each format has its own convenient function for loading data:

| File Type | Function          |
| --------- | ----------------- |
| CSV       | `pd.read_csv()`   |
| Excel     | `pd.read_excel()` |
| JSON      | `pd.read_json()`  |

Each of these functions takes the **file path** as a required argument.
We can also pass optional keyword arguments such as `index_col`, `sheet_name`, or `orient`.

---

### **1. Reading CSV Files**

A **CSV file** stores tabular data as comma-separated text.
By default, pandas assigns integer row labels and uses the first line as column headers.
We can customize this behavior using the `index_col` argument.

#### **Code:**

```python
# data.csv contains baseball data
df = pd.read_csv('data.csv')
print(df, '\n')

df = pd.read_csv('data.csv', index_col=0)
print(df, '\n')

df = pd.read_csv('data.csv', index_col=1)
print(df)
```

#### **Explanation:**

* `index_col=0` → Uses the **first column** as row labels.
* `index_col=1` → Uses the **second column** as row labels.
* Default → pandas automatically assigns row numbers (0, 1, 2...).

---

### **2. Reading Excel Files**

Excel files may contain **multiple sheets** (spreadsheets).
We can specify which sheet(s) to read using the `sheet_name` argument.

#### **Code:**

```python
df = pd.read_excel('data.xlsx')
print(df, '\n')

# Read by sheet index (0-indexed)
df = pd.read_excel('data.xlsx', sheet_name=1)
print(df, '\n')

# Read by sheet name
df = pd.read_excel('data.xlsx', sheet_name='MIL')
print(df, '\n')

# Read multiple sheets into a dict
df_dict = pd.read_excel('data.xlsx', sheet_name=[0, 1])
print(df_dict[1], '\n')

# Read all sheets
df_dict = pd.read_excel('data.xlsx', sheet_name=None)
print(df_dict.keys())
```

#### **Explanation:**

* `sheet_name=1` → Reads the **second sheet**.
* `sheet_name='MIL'` → Reads sheet by **name**.
* `sheet_name=[0,1]` → Returns an **ordered dictionary** of sheets.
* `sheet_name=None` → Loads **all sheets**.

---

### **3. Reading JSON Files**

A **JSON file** is similar to a nested Python dictionary.
The function `pd.read_json()` can interpret the JSON structure in multiple orientations.

#### **Code:**

```python
print(data, '\n')

df1 = pd.read_json('data.json')
print(df1, '\n')

df2 = pd.read_json('data.json', orient='index')
print(df2)
```

#### **Explanation:**

* Default orientation (`orient='columns'`) treats **outer keys as column labels**.
* `orient='index'` treats **outer keys as row labels**.

---

## **B. Writing to Files**

pandas also supports exporting DataFrames to CSV, Excel, and JSON formats using:

* `DataFrame.to_csv()`
* `DataFrame.to_excel()`
* `DataFrame.to_json()`

Each supports optional arguments like `index`, `sheet_name`, and `orient`.

---

### **1. Writing CSV Files**

#### **Code:**

```python
print(mlb_df, '\n')

# Keep the index
mlb_df.to_csv('data.csv')
df = pd.read_csv('data.csv')
print(df, '\n')

# Do not keep the index
mlb_df.to_csv('data.csv', index=False)
df = pd.read_csv('data.csv')
print(df)
```

#### **Explanation:**

* By default, `to_csv()` writes the **index** as the first column.
* Setting `index=False` omits it from the output file.

---

### **2. Writing Excel Files**

To write multiple DataFrames into a single Excel workbook, use **`pd.ExcelWriter`**.

#### **Code:**

```python
print(mlb_df1, '\n')
print(mlb_df2, '\n')

with pd.ExcelWriter('data.xlsx') as writer:
    mlb_df1.to_excel(writer, index=False, sheet_name='NYY')
    mlb_df2.to_excel(writer, index=False, sheet_name='BOS')

df_dict = pd.read_excel('data.xlsx', sheet_name=None)
print(df_dict.keys())
print(df_dict['BOS'])
```

#### **Explanation:**

* Each call to `to_excel()` writes one sheet.
* Use `ExcelWriter` to save multiple sheets in the same file.
* Default sheet name is `'Sheet1'` if not specified.

---

### **3. Writing JSON Files**

JSON exports can also be customized using the `orient` argument.

#### **Code:**

```python
print(df, '\n')

df.to_json('data.json')
df2 = pd.read_json('data.json')
print(df2, '\n')

df.to_json('data.json', orient='index')
df2 = pd.read_json('data.json', orient='index')
print(df2)
```

#### **Explanation:**

* Default → columns as outer keys.
* `orient='index'` → row labels as outer keys.
* Useful for structured, nested data interchange.

---

# 🧩 **Time to Code!**

### **1. Read CSV Files**

**Question:**
Read the files `'stats.csv'` and `'salary.csv'` into DataFrames.

**Answer:**

```python
stats_df = pd.read_csv('stats.csv')
salary_df = pd.read_csv('salary.csv')
```

**Output:**

```
            name  rbi  hr
0   jose sanchez   19   1
1  julio ricardo  100   5
2      matt baum  112  10

            name  salary
0   jose sanchez   19000
1  julio ricardo   10000
2      matt baum   11002
```

---

### **2. Merge DataFrames**

**Question:**
Merge `stats_df` and `salary_df` into a single DataFrame.

**Answer:**

```python
df = pd.merge(stats_df, salary_df)
```

**Output:**

```
            name  rbi  hr  salary
0   jose sanchez   19   1   19000
1  julio ricardo  100   5   10000
2      matt baum  112  10   11002
```

---

### **3. Write to CSV**

**Question:**
Write the merged DataFrame `df` into a CSV file named `'out.csv'` without the index.

**Answer:**

```python
df.to_csv('out.csv', index=False)
```

**Output File:**

```
name,rbi,hr,salary
jose sanchez,19,1,19000
julio ricardo,100,5,10000
matt baum,112,10,11002
```


