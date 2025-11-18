# **Introduction**

An overview of the main models used in scikit-learn.

In this chapter, you will continue using scikit-learn to create **regression models**, **classification models**, and learn essential tools like **hyperparameter tuning** and **cross-validation**.

---

## **A. Creating Models for Data**

### **What Data Scientists Actually Do**

Data scientists spend most of their time:

* Analyzing data
* Cleaning / preprocessing
* Building simple, reliable models
* Extracting meaningful insights

Unlike ML engineers, they often work with **smaller datasets**, so traditional statistical models are **fast, interpretable, and accurate enough**.

---

## **Linear Regression Models**

scikit-learn provides multiple regression tools to model relationships between features and a target value.

Examples include:

* **Linear Regression**
* **Ridge Regression**
* **Lasso Regression**
* **ElasticNet**

They are easy to train, fast, and commonly used for numeric prediction tasks.

---

## **Classification Models**

scikit-learn also includes several classic algorithms for labeling or categorizing data:

* **Logistic Regression**
* **k-Nearest Neighbors (kNN)**
* **Decision Trees**
* **Support Vector Machines (SVM)**

These will be covered in later chapters.

---

## **Hyperparameters**

These are **settings you choose before training the model**, such as:

* number of neighbors in kNN
* strength of regularization in Ridge
* depth of a decision tree
* learning rate (for some algorithms)

They are **not learned** from data — YOU choose them.

Good hyperparameters = better model performance.

---

## **Hyperparameter Tuning (Later Chapters)**

Since different settings lead to different results, data scientists use tools like:

* grid search
* randomized search
* cross-validation

to find the **best combination** of hyperparameters.



