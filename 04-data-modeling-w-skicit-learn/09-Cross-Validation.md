# **Cross-Validation**

**Cross-validation repeatedly trains and tests a model on different splits of the dataset to measure performance more accurately.**

---

## **A. Why Do We Need Cross-Validation?**

A single testing set gives only **one measurement** of model quality.
But what if:

* that test set is unusually easy?
* or unusually hard?
* or not representative of the full dataset?

To evaluate a model **more reliably**, we need multiple evaluation sets.

### **Validation Sets**

If a dataset is large enough, we can split it into:

1. **Training set** → used to fit the model
2. **Validation set** → used to evaluate during training/tuning
3. **Testing set** → used only for final evaluation

But splitting into 3 sets means:

* training set becomes **smaller**
* model may perform **worse** due to less data

Cross-validation solves this by generating **synthetic validation sets** from the training data.

---

## **B. K-Fold Cross-Validation**

The most common method is **K-Fold cross-validation**.

### **How K-Fold Works**

1. Split the training data into **k equal folds**.
2. Repeat **k rounds**:

   * Pick **1 fold** → validation set
   * Combine the other **k – 1 folds** → training set
3. Train + evaluate the model in each round.
4. Collect all scores → final CV score array

This means the model is trained **k times**, each with a different validation set.

---

### **Why Use K-Fold CV?**

✔ Uses **all data** for training and evaluation
✔ Provides a **more stable** estimate of performance
✔ Helps detect overfitting and underfitting
✔ Avoids shrinking the training set too much

---

### **Visualization of 5-Fold Cross-Validation**

```
Round 1:  Train Train Train Train | Test
Round 2:  Train Train Train Test | Train
Round 3:  Train Train Test Train | Train
Round 4:  Train Test Train Train | Train
Round 5:  Test Train Train Train | Train
```

Each fold gets to be the test set exactly once.

---

## **C. Using cross_val_score in scikit-learn**

scikit-learn provides:

```python
from sklearn.model_selection import cross_val_score
```

This function:

* Runs the full K-Fold CV process
* Automatically fits the model each round
* Returns an **array of scores**, one per fold

You *do not* call `.fit()` beforehand — CV handles it internally.

---

### **Example: Classification (Accuracy Score)**

```python
from sklearn import linear_model
from sklearn.model_selection import cross_val_score

clf = linear_model.LogisticRegression(max_iter=3000)

# Predefined data and labels
cv_score = cross_val_score(clf, data, labels, cv=3)  # k = 3

print(repr(cv_score))
```

**Output**

```
array([0.94210526, 0.96315789, 0.94708995])
```

---

### **Example: Regression (R² Score)**

```python
from sklearn import linear_model
from sklearn.model_selection import cross_val_score

reg = linear_model.LinearRegression()

cv_score = cross_val_score(reg, data, labels, cv=4)  # k = 4

print(repr(cv_score))
```

**Output**

```
array([0.37548118, 0.49022643, 0.52061242, 0.54864085])
```

---

## **D. Stratified K-Fold (for Classification)**

For classification problems, scikit-learn automatically uses:

> **Stratified K-Fold**

This ensures **each fold** has roughly the same class proportions as the full dataset.

Example:
If the original data is 60% class 0 and 40% class 1 →
Each fold will also be close to 60/40.

This prevents biased folds.

---

## **E. When Not to Use Cross-Validation**

Cross-validation can be **slow**, especially with:

* very large datasets
* very complex models

In those cases, it's often better to use:

✔ A standard train/validation/test split
✔ A single evaluation pass


