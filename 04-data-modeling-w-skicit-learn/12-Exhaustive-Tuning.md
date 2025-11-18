# **Exhaustive Tuning**

**Exhaustive tuning = trying *every possible* combination of hyperparameter values to find the best one.**
It is called *exhaustive* because it **checks all options** without skipping.

Use **grid search** to perform full hyperparameter exploration.

---

## **Chapter Goals**

* Understand how to use **GridSearchCV** for exhaustive hyperparameter tuning
* Learn how cross-validation is applied during grid search

---

## **A. Grid-Search Cross-Validation**

**Think of GridSearchCV as a smart brute-force machine that tries every hyperparameter combination — but with cross-validation to score each one.**

When the dataset is small enough and we need the *best possible* hyperparameters, we use **exhaustive grid search**:

1. Provide lists of possible hyperparameter values
2. GridSearchCV builds a model for each possible combination
3. Each model is evaluated using K-Fold cross-validation
4. The best hyperparameter set is returned

We use the `GridSearchCV` object from `sklearn.model_selection`.

**GridSearchCV = tests all hyperparameter combinations + uses CV + picks the best model.**

---

### **Example: Grid Search for Bayesian Ridge Regression**

```python
reg = linear_model.BayesianRidge()
params = {
  'alpha_1': [0.1, 0.2, 0.3],
  'alpha_2': [0.1, 0.2, 0.3]
}

reg_cv = GridSearchCV(reg, params, cv=5)
# predefined train and test sets
reg_cv.fit(train_data, train_labels)
print(reg_cv.best_params_)

# Output
{'alpha_1': 0.3, 'alpha_2': 0.1}
```

In this example:

* We search through every combination of `alpha_1` and `alpha_2`
* Cross-validation (5-fold) evaluates each pair
* The best pair is returned via `.best_params_`

For any scikit-learn model, you can check its documentation page to see the list of hyperparameters you can include in the `params` dictionary.

---

### **Why Not Always Use Exhaustive Grid Search?**

Because it can be **very slow**.

For each hyperparameter combination:
→ Run K-Fold CV
→ Fit multiple models
→ Evaluate all of them

Grid search is great when:

* The dataset is **small enough**
* You really need the **best** hyperparameter combination

For larger datasets, other techniques (like randomized search) are usually preferred.

