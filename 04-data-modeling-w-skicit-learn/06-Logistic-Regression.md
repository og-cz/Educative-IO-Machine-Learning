# **Logistic Regression**

Logistic Regression predicts whether something belongs to **class 0 or class 1** by converting inputs into a probability between **0 and 1** using the **sigmoid function**.

### Key idea:

* ❌ *Not* used for predicting continuous numbers
* ✔ **Used for classification**
* ✔ Output: **0 or 1** (or multiple classes in the multiclass version)

---

# **Chapter Goals**

* Understand logistic regression for linearly separable data
* Use scikit-learn’s `LogisticRegression` for binary and multiclass classification
* Learn about solvers and cross-validated logistic regression

---

# A. **Classification**

You have used several linear regression models so far.
Despite the name, **Logistic Regression is not a regression model — it is a linear classifier.**

Why is it called “regression”?
Because it performs regression on the **logit**, which is then passed through a sigmoid to produce probabilities for classification.

We use the scikit-learn class:

```
sklearn.linear_model.LogisticRegression
```

Default mode: **binary classification** (predicts labels 0 or 1).

---

## **Binary Classification Example**

```python
print('Data shape: {}\n'.format(data.shape))
print('Labels:\n{}\n'.format(repr(labels)))

from sklearn import linear_model
reg = linear_model.LogisticRegression()
reg.fit(data, labels)

new_data = np.array([
  [ 0.3,  0.5, -1.2,  1.4],
  [-1.3,  1.8, -0.6, -8.2]])

print('Prediction classes: {}\n'.format(
  repr(reg.predict(new_data))))
```

### Output

```
Data shape: (569, 4)
Labels: array([...])
Prediction classes: array([1, 0])
```

The model predicts:

* First sample → **1**
* Second sample → **0**

---

# **Multiclass Classification**

When labels are more than two classes (e.g., 0, 1, 2), we set:

```python
multi_class='multinomial'
```

For this, we also need a compatible solver such as `'lbfgs'`.

### Example

```python
print('Data shape: {}\n'.format(data.shape))
print('Labels:\n{}\n'.format(repr(labels)))

from sklearn import linear_model
reg = linear_model.LogisticRegression(
    solver='lbfgs',
    multi_class='multinomial',
    max_iter=200
)
reg.fit(data, labels)

new_data = np.array([
    [1.8, -0.5, 6.2, 1.4],
    [3.3, 0.8, 0.1, 2.5]
])

print('Prediction classes: {}\n'.format(
  repr(reg.predict(new_data))))
```

### Output

```
Data shape: (150, 4)
Labels: array([...])
Prediction classes: array([2, 0])
```

### Why `max_iter`?

If you don’t increase iterations (default=100), you may get:

```
ConvergenceWarning: Solver failed to converge
```

So `max_iter=200` (or higher) is common.

---

# B. **Solvers**

A **solver** is the algorithm used to find the optimal weights during training.

Scikit-learn supports several solvers:

| Solver    | Handles L1 | Handles L2 | Multiclass? | Large dataset? |
| --------- | ---------- | ---------- | ----------- | -------------- |
| liblinear | ✔          | ✔          | One-vs-Rest | Small datasets |
| lbfgs     | ✖          | ✔          | Multinomial | Good general   |
| newton-cg | ✖          | ✔          | Multinomial | Good general   |
| sag       | ✖          | ✔          | Multinomial | Large datasets |
| saga      | ✔          | ✔          | Multinomial | Large datasets |

Default solver (may change in future): **liblinear**

To choose your own:

```python
from sklearn import linear_model
reg = linear_model.LogisticRegression(
    solver='lbfgs',
    max_iter=1000
)
```

---

# C. **Cross-validated Logistic Regression**

Just like RidgeCV and LassoCV, logistic regression has a cross-validated version:

```
sklearn.linear_model.LogisticRegressionCV
```

This automatically picks the best regularization strength using cross-validation.

Example:

```python
from sklearn import linear_model
reg = linear_model.LogisticRegressionCV(
    solver='multinomial',
    max_iter=1000
)
```

---

# **Time to Code!**

You will implement `multiclass_lr`, which:

1. Creates a logistic regression model
2. Uses solver `'lbfgs'`
3. Uses multiclass `'multinomial'`
4. Uses `max_iter` parameter
5. Fits the model and returns it

```python
def multiclass_lr(data, labels, max_iter):
    reg = linear_model.LogisticRegression(
        solver='lbfgs',
        max_iter=max_iter,
        multi_class='multinomial'
    )
    reg.fit(data, labels)
    return reg
```

### Example Output

```
max_iter: 1000, solver: lbfgs, multi_class: multinomial

array([[-0.42337807,  0.96721343, -2.51728182, -1.07954287],
       [ 0.53450128, -0.32140046, -0.20643473, -0.94412164],
       [-0.11112321, -0.64581297,  2.72371656,  2.02366451]])

array([  9.84987356,   2.23644935, -12.08632291])
```

