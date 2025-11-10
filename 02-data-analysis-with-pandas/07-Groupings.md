# Groupings

Learn how to group and summarize data efficiently using `groupby`.

---

## **A. Grouping by a Single Column**

**Code:**

```python
# Predefined DataFrame of MLB stats
print('{}\n'.format(df))

groups = df.groupby('yearID')

for name, group in groups:
    print('Year:', name)
    print('{}\n'.format(group))
```

**Explanation:**
`groupby('yearID')` creates groups of rows that share the same value in the `'yearID'` column.
The `for` loop prints each year’s grouped DataFrame separately.

---

**Code (Accessing Groups and Aggregations):**

```python
print(groups.get_group(2016))
print(groups.sum())
print(groups.mean())
```

**Explanation:**

* `.get_group(2016)` retrieves the DataFrame for that specific group.
* `.sum()` calculates totals for each year.
* `.mean()` computes averages for each year.

---

**Output Example:**

```
           H     R
yearID            
2015    4405  2106
2016    4509  2405
2017    4345  2338
```

---

### **Filtering Groups**

**Code:**

```python
no2015 = groups.filter(lambda x: x.name > 2015)
print(no2015)
```

**Explanation:**
`filter` removes groups that don’t satisfy a condition.
Here, `lambda x: x.name > 2015` means keep only groups from years greater than 2015.

---

## **B. Grouping by Multiple Columns**

**Code:**

```python
# player_df is predefined
groups = player_df.groupby(['yearID', 'teamID'])

for name, group in groups:
    print('Year, Team:', name)
    print('{}\n'.format(group))
```

**Explanation:**
Passing a list `['yearID', 'teamID']` groups by both year and team.
Each group’s name is now a tuple - `(year, team)`.

---

**Code (Summing Groups):**

```python
print(groups.sum())
```

**Explanation:**
Aggregates statistics for each (year, team) pair.
This is often used to calculate per-team totals each season.

---

**Output Example:**

```
                 H
yearID teamID     
2016   BOS     607
       HOU     374
2017   BOS     441
       HOU     337
```

---

# **Time to Code!**

### **1. Group by Year**

**Question:**
Create a variable `year_group` that groups the DataFrame `df` by the `'yearID'` column.

**Answer:**

```python
year_group = df.groupby('yearID')
```

**Output:**

```
dict_keys([2015, 2016, 2017])
```

---

### **2. Sum Yearly Statistics**

**Question:**
Create a variable `year_stats` that contains the total stats per year using `.sum()`.

**Answer:**

```python
year_stats = year_group.sum()
```

**Output:**

```
           H    HR
yearID            
2015    4405  2106
2016    4509  2405
2017    4345  2338
```

---

### **3. Retrieve 2017 Home Runs**

**Question:**
Get the number of home runs (`'HR'`) in 2017 using `.loc`.

**Answer:**

```python
hr_2017 = year_stats.loc[2017, 'HR']
```

**Output:**

```
2338
```

---

### **4. Group by Year and Team**

**Question:**
Group the data by both `'yearID'` and `'teamID'` and store it in `year_team_group`.

**Answer:**

```python
year_team_group = df.groupby(['yearID', 'teamID'])
```

**Output:**

```
dict_keys([
(2015, 'BOS'), (2015, 'CLE'), (2015, 'DET'),
(2016, 'BOS'), (2016, 'CLE'), (2016, 'DET'),
(2017, 'BOS'), (2017, 'CLE'), (2017, 'DET')
])
```

---

### **5. Sum Team-Year Statistics**

**Question:**
Create `year_team_stats` to show total hits and home runs per team per year.

**Answer:**

```python
year_team_stats = year_team_group.sum()
```

**Output:**

```
                  H   HR
yearID teamID           
2015   BOS     1495  748
       CLE     1395  669
       DET     1515  689
2016   BOS     1598  878
       CLE     1435  777
       DET     1476  750
2017   BOS     1461  785
       CLE     1449  818
       DET     1435  735
```

