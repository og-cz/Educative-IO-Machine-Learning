# **LASSO Regression**

**LASSO regression is linear regression with L1 regularization, which can shrink some coefficients *all the way to zero* — effectively removing useless features.**

## **Chapter Goals**

* Understand sparse (L1) regularization
* Learn how LASSO performs feature selection
* Implement LASSO regression in scikit-learn

---

# **A. Sparse Regularization (L1 Penalty)**

Ridge regression uses an **L2 penalty**, which shrinks coefficients but rarely makes them zero.

**LASSO uses the L1 norm instead:**

[
\text{Loss} = \text{SSE} + \alpha \sum |w|
]

where:

* **SSE** = sum of squared errors
* **α** = regularization strength
* **L1 norm** = sum of absolute weight values

### **Key Effect of L1 Regularization**

LASSO naturally prefers **sparse models**, meaning:

* many coefficients become exactly **0**
* only the strongest features survive
* irrelevant or duplicate features are removed

This makes LASSO **both a regression model and a feature selection method**.

---

# **B. LASSO in scikit-learn**

Use:

```python
from sklearn.linear_model import Lasso
```

Just like Ridge regression, LASSO takes `alpha=` as its key hyperparameter.

### **Example Using a Dataset With 150 Samples × 4 Features**

```python
# predefined dataset
print('Data shape:', data.shape)
print('Labels shape:', labels.shape)

from sklearn import linear_model
reg = linear_model.Lasso(alpha=0.1)
reg.fit(data, labels)

print('Coefficients:', reg.coef_)
print('Intercept:', reg.intercept_)
print('R2:', reg.score(data, labels))
```

### **Output**

```
Data shape: (150, 4)
Labels shape: (150,)

Coefficients: array([ 0.        , -0.        ,  0.40811896,  0.        ])
Intercept: -0.5337110569441175
R2: 0.8958211202747038
```

Here, **3 out of 4 features were removed** — their coefficients were shrunk to zero.
This is the defining behavior of LASSO.

---

# **C. LASSO with Cross-Validation**

Just like RidgeCV, scikit-learn provides:

```python
from sklearn.linear_model import LassoCV
```

This automatically picks the best α via cross-validation.

---

# **Time to Code!**

Implement LASSO regression using the provided α value.

```python
def lasso_reg(data, labels, alpha):
    from sklearn import linear_model
    reg = linear_model.Lasso(alpha=alpha)
    reg.fit(data, labels)
    return reg
```

### **Example Output**

```
array([-0.09893538,  0.04882625, -0.04135539,  1.76163112, -1.04492925,
        3.83661798, -0.01185763, -1.20269042,  0.27103396, -0.01402828,
       -0.77320498,  0.01019297, -0.55392516])

25.30130244233386
```


