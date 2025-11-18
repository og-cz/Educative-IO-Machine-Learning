# **Applying CV to Decision Trees**

Apply **K-Fold Cross-Validation** to tune the maximum depth of a Decision Tree.

---

## **Chapter Goals**

* Use K-Fold cross-validation to tune a Decision Tree’s `max_depth`.

---

## **A. Decision Tree Depth**

Just like how we tuned the α value for regularized regression, we can tune a decision tree hyperparameter — specifically, its **maximum depth**.

The hyperparameter **`max_depth`** determines how “deep” the tree can grow.
A deeper tree = more complex model = higher risk of overfitting.

K-Fold CV lets us **evaluate multiple depths** and pick the one with the best cross-validated performance.

Below is an example of using a function you will implement (`cv_decision_tree`) to measure accuracy at different depths:

```python
is_clf = True  # for classification

for depth in range(3, 8):
  # Predefined data and labels
  scores = cv_decision_tree(
    is_clf, data, labels, depth, 5)  # k = 5

  mean = scores.mean()        # Mean acc across 5 folds
  std_2 = 2 * scores.std()    # 95% CI = mean ± 2*std

  print('95% C.I. for depth {}: {} +/- {:.2f}\n'.format(
    depth, mean, std_2))

# Output
95% C.I. for depth 3: 0.9133333333333333 +/- 0.02

95% C.I. for depth 4: 0.9199999999999999 +/- 0.04

95% C.I. for depth 5: 0.9333333333333333 +/- 0.04

95% C.I. for depth 6: 0.9166666666666666 +/- 0.05

95% C.I. for depth 7: 0.8933333333333333 +/- 0.05
```

We tested tree depths **3 → 7**, measuring 5-Fold CV accuracy for each.
From the confidence intervals, **depth = 4** performs the best.

If deeper values (5–7) kept improving, we would continue testing higher depths.

---

## **Time to Code!**

In this exercise, you’ll implement the `cv_decision_tree` function.

### ✔ Requirements

1. If `is_clf == True`:
   use `tree.DecisionTreeClassifier(max_depth=max_depth)`
2. Otherwise:
   use `tree.DecisionTreeRegressor(max_depth=max_depth)`
3. Use `cross_val_score` to compute the CV scores
4. Return the resulting `scores` array.

### **Starter Code**

```python
def cv_decision_tree(is_clf, data, labels,
                     max_depth, cv):
  # CODE HERE
  pass
```

