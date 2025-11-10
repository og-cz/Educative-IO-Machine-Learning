# Filtering

In this section, we’ll learn how to filter rows in a pandas DataFrame using **conditional logic** - a skill that lets you isolate only the data that meets specific criteria.

---

## **Chapter Goals**

* Understand how to filter a DataFrame based on specific conditions
* Learn to use relational operations and pandas filtering functions
* Practice filtering real MLB statistics

---

## **A. Creating Filter Conditions**

In NumPy, we used **relational operations** (`>`, `<`, `==`, etc.) to create **boolean arrays** that marked which elements passed a test.
Pandas works the same way - but now, we apply these comparisons to **DataFrame columns**.

Each comparison returns a **boolean Series**, where `True` means the row passes the condition.

```python
df = pd.DataFrame({
  'playerID': ['bettsmo01', 'canoro01', 'cruzne02', 'ortizda01', 'cruzne02'],
  'yearID': [2016, 2016, 2016, 2016, 2017],
  'teamID': ['BOS', 'SEA', 'SEA', 'BOS', 'SEA'],
  'HR': [31, 39, 43, 38, 39]
})

print(df, '\n')

cruzne02 = df['playerID'] == 'cruzne02'
hr40 = df['HR'] > 40
notbos = df['teamID'] != 'BOS'

print(cruzne02, '\n')
print(hr40, '\n')
print(notbos)
```

**Explanation:**

* `df['playerID'] == 'cruzne02'` → True only for rows where `playerID` is `"cruzne02"`
* `df['HR'] > 40` → True only for rows with more than 40 home runs
* `df['teamID'] != 'BOS'` → True for players not on the BOS team

These booleans become the “filters” we can use later to select rows.

---

## **B. Filters from String Functions**

Pandas provides helpful **string methods** to create filter conditions - such as:

* `.str.startswith('text')`
* `.str.endswith('text')`
* `.str.contains('text')`

These work just like Python string methods, but operate across the entire Series.

```python
str_f1 = df['playerID'].str.startswith('c')
str_f2 = df['teamID'].str.endswith('S')
str_f3 = ~df['playerID'].str.contains('o')  # negate condition with ~

print(str_f1, '\n')
print(str_f2, '\n')
print(str_f3)
```

**Explanation:**

* `str.startswith('c')` → player IDs beginning with “c”
* `str.endswith('S')` → team names ending in “S”
* `~df['playerID'].str.contains('o')` → player IDs **not containing** “o” (`~` negates the condition)

---

## **C. Checking for Set Membership with `isin()`**

Use `isin()` to check if values belong to a list (or any iterable).
This is great for filtering specific names, IDs, or years.

```python
isin_f1 = df['playerID'].isin(['cruzne02', 'ortizda01'])
isin_f2 = df['yearID'].isin([2015, 2017])

print(isin_f1, '\n')
print(isin_f2)
```

**Explanation:**

* `isin()` returns `True` if the cell’s value appears in the given list.

---

## **D. Filtering for Missing Values (`NaN`)**

Missing data in pandas is represented by `NaN`, just like NumPy’s `np.nan`.
To test for missing values, we use:

* `.isna()` → True for missing values
* `.notna()` → True for present values

```python
df = pd.DataFrame({
  'playerID': ['bettsmo01', 'canoro01', 'doejo01'],
  'yearID': [2016, 2016, 2017],
  'teamID': ['BOS', 'SEA', np.nan],
  'HR': [31, 39, 99]
})

print(df, '\n')

isna = df['teamID'].isna()
notna = df['teamID'].notna()

print(isna, '\n')
print(notna)
```

**Explanation:**
`.isna()` identifies the missing values (True for NaN),
while `.notna()` does the opposite.

---

## **E. Applying Filter Conditions**

Once you have a filter condition, apply it directly inside **square brackets** to return only rows that meet the condition.

```python
hr40_df = df[df['HR'] > 40]
not_hr30_df = df[~(df['HR'] > 30)]
str_df = df[df['teamID'].str.startswith('B')]

print(hr40_df, '\n')
print(not_hr30_df, '\n')
print(str_df)
```

**Explanation:**

* `df[df['HR'] > 40]` → rows where HR > 40
* `df[~(df['HR'] > 30)]` → rows where HR ≤ 30
* `df[df['teamID'].str.startswith('B')]` → rows where team starts with “B”

---

## **🧩 Time to Code! Practice Section**

Let’s apply what we learned to the MLB dataset.

### 1. Filter for the top hitters

Filter rows where batting average (`'BA'`) is above 0.300.

```python
top_hitters = mlb_df[mlb_df['BA'] > 0.300]
print(top_hitters)
```

---

### 2. Filter players whose IDs **do not** start with “a”

Use negation (`~`) with `.str.startswith()`.

```python
exclude_a = mlb_df[~mlb_df['playerID'].str.startswith('a')]
print(exclude_a)
```

---

### 3. Filter for two specific players

Use `isin()` to include `'bondsba01'` and `'troutmi01'`.

```python
two_ids = ['bondsba01', 'troutmi01']
two_players = mlb_df[mlb_df['playerID'].isin(two_ids)]
print(two_players)
```

