# **Evaluating Models**

Learn how to evaluate **classification** and **regression** models using standard metrics.

---

## **Chapter Goals**

* Understand how to make predictions with trained models
* Learn common evaluation metrics for regression and classification

---

## **A. Making Predictions**

Every model we’ve used includes a `.predict()` function.
This generates predictions for **new, unseen data** (data not used for training).

Example: making predictions with a **Decision Tree Regressor**:

```python
reg = tree.DecisionTreeRegressor()
# predefined train and test sets
reg.fit(train_data, train_labels)
predictions = reg.predict(test_data)
```

---

## **B. Evaluation Metrics**

### **Classification**

For classification models, we typically evaluate performance using:

* **Accuracy** — proportion of correct predictions on the test set

### **Regression**

Common regression metrics:

* **Mean Absolute Error (MAE)**

  * Most natural measure of error
  * Represents the average absolute difference between predictions and true values
* **Mean Squared Error (MSE)**

  * Squares errors → penalizes large mistakes more
* **R2 Score**

  * Measures how well the regression model fits the data
  * 1.0 = perfect fit, 0.0 = no better than baseline

All metrics come from scikit-learn’s `metrics` module.
Each function receives:

1. **actual test labels**
2. **model predictions**

---

### **Example: Evaluating a Regression Model**

```python
reg = tree.DecisionTreeRegressor()
# predefined train and test sets
reg.fit(train_data, train_labels)
predictions = reg.predict(test_data)

from sklearn import metrics

r2 = metrics.r2_score(test_labels, predictions)
print('R2: {}\n'.format(r2))

mse = metrics.mean_squared_error(
  test_labels, predictions)
print('MSE: {}\n'.format(mse))

mae = metrics.mean_absolute_error(
  test_labels, predictions)
print('MAE: {}\n'.format(mae))

# output
R2: 0.7911279948293561

MSE: 17.61393700787402

MAE: 2.704724409448819
```

---

### **Example: Evaluating a Classification Model**

```python
clf = tree.DecisionTreeClassifier()
# predefined train and test sets
clf.fit(train_data, train_labels)
predictions = clf.predict(test_data)

from sklearn import metrics

acc = metrics.accuracy_score(test_labels, predictions)
print('Accuracy: {}\n'.format(acc))

# output
Accuracy: 0.9440559440559441
```
