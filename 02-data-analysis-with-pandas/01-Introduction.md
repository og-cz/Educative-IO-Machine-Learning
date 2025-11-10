# **An Overview of Data Analysis with pandas**

In this chapter, we’ll use **pandas** to explore and analyze **Major League Baseball (MLB)** data from [Sean Lahman’s baseball database](http://www.seanlahman.com/baseball-archive/statistics/).
You’ll learn the fundamentals of data analysis - inspecting data, finding patterns, and preparing it for further use (like visualization or machine learning).

---

### **A. What Is Data Analysis?**

**Code (Concept illustration):**

```python
# Example: inspecting basic data structure
import pandas as pd

data = pd.DataFrame({
    'player': ['John', 'Mike', 'Sara', 'Ana'],
    'batting_avg': [0.315, 0.288, 0.301, 0.274],
    'home_runs': [24, 17, 19, 22]
})

print(data.head())
```

**Explanation:**
Before performing any operations, we first **analyze and understand the dataset**.
This helps us identify:

* Outliers or missing values
* Relationships between columns
* Which features are most relevant for our analysis

Data analysis ensures we’re working with **clean, meaningful data** before applying machine learning or visualization tools.

---

### **B. Introduction to pandas**

**Code:**

```python
import pandas as pd

df = pd.read_csv("Lahman/Teams.csv")
print(df.info())
print(df.describe())
```

**Explanation:**
**pandas** is a Python library designed for **data manipulation and analysis**.
It allows us to:

* Load datasets from multiple formats (CSV, Excel, SQL)
* Inspect and clean data quickly
* Convert data to **NumPy arrays** for mathematical operations

Most ML frameworks (like TensorFlow and scikit-learn) integrate smoothly with pandas, making it the **core toolkit** for data handling in Python.

---

### **C. Data Visualization with Matplotlib and Pyplot**

**Code:**

```python
import matplotlib.pyplot as plt

plt.plot(data['player'], data['home_runs'], marker='o')
plt.title("Home Runs by Player")
plt.xlabel("Player")
plt.ylabel("Home Runs")
plt.show()
```

**Explanation:**
Visualization is a **key part of data analysis** - it helps uncover trends and patterns that numbers alone can’t show.

We use:

* **Matplotlib** → the main plotting library in Python
* **Pyplot API** → a simple interface for creating charts (line plots, boxplots, histograms, etc.)

A clear visualization can reveal correlations, trends, or outliers instantly - “a picture is worth a thousand rows.”

---

### **Practice Exercises**

**1. Load and Inspect a Dataset**

**Question:**
Load `Teams.csv` from the Lahman Baseball Database and show its first 5 rows.

**Answer:**

```python
import pandas as pd

df = pd.read_csv("Lahman/Teams.csv")
print(df.head())
```

---

**2. View Summary Statistics**

**Question:**
Display column statistics (mean, min, max, etc.) for numerical data.

**Answer:**

```python
print(df.describe())
```

---

**3. Create a Simple Plot**

**Question:**
Plot team wins vs. losses using Matplotlib.

**Answer:**

```python
import matplotlib.pyplot as plt

plt.scatter(df['W'], df['L'])
plt.title("Wins vs. Losses (MLB Teams)")
plt.xlabel("Wins")
plt.ylabel("Losses")
plt.show()
```

---

### **Summary**

* **pandas** helps load, clean, and manipulate real-world datasets.
* **Data analysis** is the foundation before visualization or modeling.
* **Matplotlib (Pyplot)** lets us visualize trends clearly and quickly.

Together, pandas and Matplotlib make Python a **complete data analysis environment**.


