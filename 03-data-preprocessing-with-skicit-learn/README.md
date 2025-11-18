# Introduction

An overview of the main models used in scikit-learn.

In this chapter, you will continue to use scikit-learn, creating a variety of models for linear regression and classifying data. You'll also learn how to perform hyperparameter tuning and model evaluation through cross-validation.

## A. Creating models for data

The main job of a data scientist is analyzing data and creating models for obtaining results 
from the data. Oftentimes, data scientists will use simple statistical models for their data, rather than machine learning models like neural networks. This is because data scientists tend to work with smaller datasets than machine learning engineers, so they can quickly extract good results using statistical models.

The scikit-learn library provides many statistical models for [linear regression](https://en.wikipedia.org/wiki/Linear_regression). It also provides a few good models for classifying data, which will be introduced in later chapters.

When creating these models, data scientists need to figure out the optimal [hyperparameters](https://en.wikipedia.org/wiki/Hyperparameter) to use. Hyperparameters are values that we set when creating a model, e.g. certain constant coefficients used in the model's calculations. We'll talk more about hyperparameter tuning, the process of finding the optimal hyperparameter settings, in later chapters.

### **1. Linear Regression**

[Linear Regression](./04-data-modeling-w-skicit-learn/02-Linear-Regression.md)

- **What it is:** A basic regression model that fits a straight line to minimize squared errors.
- **What you do:** Use `LinearRegression` to model relationships between input features and a continuous target.

---

### **2. Ridge Regression**

[Ridge Regression](./04-data-modeling-w-skicit-learn/03-Ridge-Regression.md)

- **What it is:** Linear regression with L2 regularization to reduce overfitting.
- **What you do:** Apply `Ridge(alpha=...)` when you want a more stable model that shrinks large coefficients.

---

### **3. LASSO Regression**

[LASSO Regression](./04-data-modeling-w-skicit-learn/04-LASSO-Regression.md)

- **What it is:** Linear regression with L1 regularization that can set coefficients to zero.
- **What you do:** Use `Lasso(alpha=...)` for feature selection and sparsity.

---

### **4. Bayesian Regression**

[Bayesian Regression](./04-data-modeling-w-skicit-learn/05- Bayesian-Regression.md)

- **What it is:** Regression that treats model parameters as probability distributions.
- **What you do:** Use `BayesianRidge()` when you want uncertainty estimates and smoother predictions.

---

### **5. Logistic Regression**

[Logistic Regression](./04-data-modeling-w-skicit-learn/06-Logistic-Regression.md)

- **What it is:** A linear classifier that predicts probabilities using the logistic function.
- **What you do:** Use `LogisticRegression()` for binary or multiclass classification tasks.

---

### **6. Decision Trees**

[Decision Trees](./04-data-modeling-w-skicit-learn/07- Decision-Trees.md)

- **What it is:** A model that splits data into branches based on feature thresholds.
- **What you do:** Use `DecisionTreeClassifier` or `DecisionTreeRegressor` for interpretable, rule-based models.

---

### **7. Training and Testing**

[Training and Testing](./04-data-modeling-w-skicit-learn/08-Training-Testing.md)

- **What it is:** Splitting data into training and test sets to measure generalization.
- **What you do:** Use `train_test_split` to train on one portion of data and evaluate on the other.

---

### **8. Cross-Validation**

[Cross-Validation](./04-data-modeling-w-skicit-learn/09-Cross-Validation.md)

- **What it is:** Repeated training/testing on different subsets for more reliable evaluation.
- **What you do:** Use `cross_val_score` or `KFold` to validate models across multiple folds.

---

### **9. Applying CV to Decision Trees**

[Applying CV to Decision Trees](./04-data-modeling-w-skicit-learn/10-Applying-CV-to-Decision-Trees.md)

- **What it is:** Using cross-validation to tune tree hyperparameters like `max_depth`.
- **What you do:** Try multiple depth values and pick the one with the best cross-validated performance.

---

### **10. Evaluating Model**

[Evaluating Model](./04-data-modeling-w-skicit-learn/11-Evaluating-Models.md)


- **What it is:** Measuring model performance using metrics like accuracy, R2, MSE, and MAE.
- **What you do:** Use `metrics` functions (e.g., `accuracy_score`, `r2_score`, `mean_squared_error`) on predictions.

---

### **11. Exhaustive Tuning (Grid Search)**

[Exhaustive Tuning](./04-data-modeling-w-skicit-learn/12-Exhaustive-Tuning.md)

- **What it is:** Trying every possible combination of hyperparameters using cross-validation.
- **What you do:** Use `GridSearchCV` to brute-force the best hyperparameter settings on small datasets.
