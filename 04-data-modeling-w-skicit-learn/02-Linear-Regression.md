# **Linear Regression**

**Linear regression finds the best straight line that describes the relationship between inputs (X) and an output (y).**

## **Chapter Goals**

* Create a basic linear regression model based on input data and labels.

---

# **A. What is Linear Regression?**

In data science and machine learning, one major goal is to **find an equation that fits a dataset**. This is called **data modeling** — using independent variables (*features*) to predict a dependent variable (*label*), while minimizing error.

Because real-world data contains *noise*, we rarely find a perfect model.
Instead, we find a **good approximation**, and one of the most common approximations is a **linear model**.

A **linear regression model** predicts a value using a linear combination of features:

[
y = a \cdot x_1 + b \cdot x_2 + c \cdot x_3 + d
]

* (x_1, x_2, x_3) → independent variables
* (a, b, c) → coefficients
* (d) → intercept
* (y) → predicted output

This equation forms a **hyperplane** that tries to best fit your dataset.

---

# **B. Basic Linear Regression**

The most common form is **Least Squares Regression**, which finds a line (or hyperplane) that **minimizes the total squared error** between predictions and true values.

In scikit-learn, this is implemented with:

```python
from sklearn.linear_model import LinearRegression
```

The model is trained using:

```python
reg.fit(features, labels)
```

### **Example: Pizza Data (Calories, Weight → Price)**

```python
# predefined pizza data and prices
print('{}\n'.format(repr(pizza_data)))
print('{}\n'.format(repr(pizza_prices)))

from sklearn import linear_model
reg = linear_model.LinearRegression()
reg.fit(pizza_data, pizza_prices)
```

**Output**

```
array([[2100,  800],
       [2500,  850],
       [1800,  760],
       [2000,  800],
       [2300,  810]])

array([10.99, 12.5 ,  9.99, 10.99, 11.99])
```

### **Making Predictions**

```python
new_pizzas = np.array([[2000,  820],
                       [2200,  830]])

price_predicts = reg.predict(new_pizzas)
print(price_predicts)
```

**Output**

```
array([10.86599206, 11.55111111])
```

---

# **C. Coefficients, Intercept, and R²**

You can inspect the learned model:

```python
print('Coefficients:', reg.coef_)
print('Intercept:', reg.intercept_)
r2 = reg.score(pizza_data, pizza_prices)
print('R2:', r2)
```

**Output**

```
Coefficients: array([0.00330913, 0.00232937])
Intercept: 2.3376587301587346
R2: 0.9758349388652625
```

---

# **D. Explanation of Results**

### **1. Intercept**

* Baseline prediction when all features = 0
* Example: `Intercept = 2.34` → model starts at ~$2.34 before adding feature effects

### **2. Coefficient**

* Change in prediction for every +1 unit in a feature
* Example:

  * Calories coefficient ≈ 0.0033
  * Weight coefficient ≈ 0.0023
    → both slightly increase the pizza price

### **3. R² Score**

* Measures how well the model fits the data
* Ranges from **–∞ to 1** in scikit-learn
* **1.0 = perfect fit**, **0 = no relationship**

Example:
**R² = 0.975 → model explains ~97.5% of price variation → excellent fit**

---

# **Time to Code!**

Complete the function using `LinearRegression` to fit a model and return it.

```python
def linear_reg(data, labels):
    from sklearn import linear_model
    reg = linear_model.LinearRegression()
    reg.fit(data, labels)
    return reg
```

**Example Output of a Trained Model**

```
Coefficient: [-1.08011358e-01  4.64204584e-02  2.05586264e-02  2.68673382e+00
 -1.77666112e+01  3.80986521e+00  6.92224640e-04 -1.47556685e+00
  3.06049479e-01 -1.23345939e-02 -9.52747232e-01  9.31168327e-03
 -5.24758378e-01]
Intercept: 36.459488385090125
```



