# **Bayesian Regression**

Bayesian Regression is like normal linear regression — **but instead of giving one single “best” answer, it gives a *distribution* of possible answers and how confident it is.**

### **Ordinary Regression**

* “Here is the best line.”

### **Bayesian Regression**

* “Here is the most *probable* line…
  and here’s how *uncertain* I am.”

You use this when you want **predictions + confidence estimates**.

---

# **Chapter Goals**

* Understand Bayesian regression
* Learn how priors affect learning
* Use `BayesianRidge` in scikit-learn
* Tune hyperparameters α and λ

---

# A. **Bayesian Techniques**

Earlier, you learned hyperparameter tuning using cross-validation.
Bayesian regression takes a different path:

### **Bayes Logic**

1. **Prior** — what you believe before seeing data
   *“Pizzas are usually ₱150.”*
2. **Data** — what you observe
   *“These pizzas today cost ₱200.”*
3. **Posterior** — updated belief
   *“Okay, the true average might be higher.”*

It follows:

> **New belief = Prior × Evidence (normalized)**

### How it applies to regression

Instead of giving single weight values, Bayesian regression gives a **distribution** over weights, meaning we also get **uncertainty** estimates.

---

# B. **Hyperparameter Priors**

Bayesian Ridge Regression has two hyperparameters:

* **α (alpha)** → same role as in ridge regression: controls regularization strength
* **λ (lambda)** → precision of weights (inverse of variance)

### **Both α and λ are assumed to follow Gamma distributions**

A Gamma distribution is controlled by:

* **shape** parameter
* **scale** parameter

You don’t need full math details — only that scikit-learn assumes:

```
α ~ Gamma(α1, α2)
λ ~ Gamma(λ1, λ2)
```

Defaults:
`α1 = α2 = λ1 = λ2 = 1e-6`

---

# C. **Tuning the Model**

`BayesianRidge` automatically:

✔ fits regression weights
✔ adjusts α and λ using evidence from data
✔ provides coefficients *and* uncertainty

### **Example Code**

```python
print('Data shape: {}\n'.format(data.shape))
print('Labels shape: {}\n'.format(labels.shape))

from sklearn import linear_model

reg = linear_model.BayesianRidge()
reg.fit(data, labels)

print('Coefficients: {}\n'.format(repr(reg.coef_)))
print('Intercept: {}\n'.format(reg.intercept_))
print('R2: {}\n'.format(reg.score(data, labels)))
print('Alpha: {}\n'.format(reg.alpha_))
print('Lambda: {}\n'.format(reg.lambda_))
```

### Example Output

```
Data shape: (150, 4)
Labels shape: (150,)

Coefficients: array([-0.1136, -0.0352, 0.2446, 0.5730])
Intercept: 0.1650
R2: 0.9303
Alpha: 20.9757
Lambda: 9.5335
```

### Customizing priors

You can manually set them:

```python
BayesianRidge(alpha_1=1e-3, alpha_2=1e-3, lambda_1=1e-3, lambda_2=1e-3)
```

---

# **Time to Code!**

Implement a function that:

1. Creates a `BayesianRidge` model
2. Fits it to the input data
3. Returns the trained model

```python
def bayes_ridge(data, labels):
    reg = linear_model.BayesianRidge()
    reg.fit(data, labels)
    return reg
```

### Example Output

```
array([-0.1014, 0.0497, -0.0438, 1.8948, -2.1419,
        3.6740, -0.0106, -1.2452, 0.2802, -0.0140,
       -0.7972, 0.0100, -0.5618 ])

27.55185485790286
0.043047452914199
0.48369920524561943
```


