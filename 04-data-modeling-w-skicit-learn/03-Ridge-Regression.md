# **Ridge Regression**

**Ridge regression is linear regression with a penalty that keeps coefficients small, preventing overfitting and instability.**

## **Chapter Goals**

* Learn why regularization is needed
* Understand how ridge regression stabilizes linear models
* Use cross-validation to choose the best α
* Implement a cross-validated ridge regression model in scikit-learn

---

# **A. Why Regularization Is Needed**

Ordinary Least Squares (OLS) works well only when **features are independent (uncorrelated)**.
But real datasets often contain:

* noise
* redundant features
* correlated variables (e.g., prices in USD, EUR, JPY)

This makes OLS:

* unstable
* extremely sensitive to noise
* prone to huge, fluctuating coefficients

**Simpler Explanation**
OLS fits a line by minimizing squared error (SSE), but if features are correlated or noisy, OLS becomes unstable.
Regularization fixes this by shrinking coefficients to prevent wild behavior.

---

# **B. What Ridge Regression Does**

OLS minimizes:

[
\text{SSE} = \sum (y_i - \hat{y}_i)^2
]

Ridge regression adds a **penalty term** that punishes large coefficients:

[
\text{Ridge Loss} = \text{SSE} + \alpha \sum w^2
]

* The new term is the **penalty**
* **Larger α → stronger shrinking → smaller coefficients**
* Smaller coefficients → less sensitive to noise → more stable model

### **Visual Effect**

* OLS lines vary wildly when noise is added
* Ridge regression lines stay grouped and stable
* Ridge reduces *variance* without increasing *bias* too much

---

# **C. Implementing Ridge Regression in scikit-learn**

Just like linear regression, but using:

```python
from sklearn.linear_model import Ridge
```

### **Example: Pizza Dataset**

```python
from sklearn import linear_model
reg = linear_model.Ridge(alpha=0.1)
reg.fit(pizza_data, pizza_prices)

print('Coefficients:', reg.coef_)
print('Intercept:', reg.intercept_)
print('R2:', reg.score(pizza_data, pizza_prices))
```

**Output**

```
Coefficients: array([0.00330919, 0.0023288 ])
Intercept: 2.337978289647138
R2: 0.9758349388362842
```

Because the dataset is simple, ridge regression produces similar results to OLS — but on noisier data, ridge would be far more stable.

---

# **D. Choosing the Best α (Cross-Validation)**

α controls how much the coefficients shrink.

* **Small α → behaves like linear regression**
* **Large α → coefficients shrink a lot → model becomes simpler**

Rather than guessing α, we use **cross-validation** to choose the best one automatically.

### **RidgeCV: Ridge Regression + Cross-Validation**

```python
from sklearn import linear_model

alphas = [0.1, 0.2, 0.3]
reg = linear_model.RidgeCV(alphas=alphas)

reg.fit(pizza_data, pizza_prices)

print('Coefficients:', reg.coef_)
print('Intercept:', reg.intercept_)
print('Chosen alpha:', reg.alpha_)
```

**Output**

```
Coefficients: array([0.00330932, 0.00232767])
Intercept: 2.338616853432976
Chosen alpha: 0.3
```

---

# **E. What Is Overfitting?**

**Overfitting = the model learns the noise instead of the pattern.**

The model becomes:

* too complex
* too sensitive
* too specific to the training data
* poor at generalizing

Ridge regression reduces overfitting by keeping coefficients small and stable.

---

# **Time to Code!**

Complete the cross-validated ridge regression function.

```python
def cv_ridge_reg(data, labels, alphas):
    from sklearn import linear_model
    reg = linear_model.RidgeCV(alphas=alphas)
    reg.fit(data, labels)
    return reg
```

**Example Output**

```
array([-1.07473720e-01,  4.65716368e-02,  1.59989980e-02,  2.67001859e+00,
       -1.66846452e+01,  3.81823322e+00, -2.69060955e-04, -1.45962557e+00,
        3.03515266e-01, -1.24205938e-02, -9.40758541e-01,  9.36807528e-03,
       -5.25966203e-01])

35.69365461796402

0.1
```



