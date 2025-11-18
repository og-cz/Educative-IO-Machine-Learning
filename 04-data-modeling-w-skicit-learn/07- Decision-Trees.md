# Decision Trees (Super Easy Explanation)

Decision trees are **models that make decisions like a flowchart**:

* At each node, they check a **feature** (like "is age < 20?").
* Depending on the answer, you go **left or right**.
* When you reach a **leaf**, that's your prediction.

They work for:

* **Classification** (predict categories)
* **Regression** (predict numbers)

---

# Key Ideas

### How do they choose what feature to split on?

They choose the feature that **best separates the data**:

* For **classification** → minimize **Gini Impurity**
* For **regression** → minimize **MSE** or **MAE**

### ✔ Why limit tree depth?

Without limits, a tree will grow huge and **overfit**.

`max_depth=5` means:

* Tree can only have 5 levels
* More general
* Less overfitting

---

# Coding Exercise Solution (Exactly what they want)

You must:

1. Create a `DecisionTreeRegressor` with `max_depth=5`
2. Fit it on `data` and `labels`

### Final Code:

```python
from sklearn import tree

d_tree = tree.DecisionTreeRegressor(max_depth=5)
d_tree.fit(data, labels)
```

This returns a fitted model that can be used to make predictions.

---

# Simple Mental Model

* **Linear models** → draw straight lines / planes.
* **Decision trees** → chop the space into boxes.

Trees are **non-linear**, good for messy data, but can overfit if too deep.



