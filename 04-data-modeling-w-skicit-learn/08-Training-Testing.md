# **Training and Testing**

In this section, you’ll learn **why datasets must be split** and how to separate them into **training** and **testing** sets using **scikit-learn**.

---

## **A. Training vs Testing**

When building a machine learning model, you should **never evaluate it on the same data you trained it on**.
Why?

Because the model has already “seen” that data — it can memorize patterns instead of learning generalizable rules.

### **Two Dataset Roles**

**1. Training Set**
Used to **fit** the model — this is where learning happens.

**2. Testing Set**
Used to **evaluate** how well the model performs on *unseen* data.

---

### **Typical Split Ratio**

Most common:

* **70–90%** → training
* **10–30%** → testing

Larger training sets improve learning.
Larger testing sets improve evaluation reliability.

---

## **B. Splitting the Dataset**

scikit-learn provides a convenient utility:

```python
from sklearn.model_selection import train_test_split
```

This function:

* **shuffles** the data (important!)
* splits it into training and testing sets
* returns 4 items:

  1. training data
  2. testing data
  3. training labels
  4. testing labels

---

### **Example: Splitting a Small Dataset**

```python
data = np.array([
  [10.2 ,  0.5 ],
  [ 8.7 ,  0.9 ],
  [ 9.3 ,  0.8 ],
  [10.1 ,  0.4 ],
  [ 9.5 ,  0.77],
  [ 9.1 ,  0.68],
  [ 7.7 ,  0.9 ],
  [ 8.3 ,  0.8 ]])

labels = np.array(
  [1.4, 1.2, 1.6, 1.5, 1.6, 1.3, 1.1, 1.2])

from sklearn.model_selection import train_test_split
split_dataset = train_test_split(data, labels)
train_data = split_dataset[0]
test_data = split_dataset[1]
train_labels = split_dataset[2]
test_labels = split_dataset[3]

print(train_data)
print(train_labels)
print(test_data)
print(test_labels)
```

### **Output**

```
array([[ 9.1 ,  0.68],
       [ 9.3 ,  0.8 ],
       [ 7.7 ,  0.9 ],
       [ 8.7 ,  0.9 ],
       [10.1 ,  0.4 ],
       [ 8.3 ,  0.8 ]])

array([1.3, 1.6, 1.1, 1.2, 1.5, 1.2])

array([[ 9.5 ,  0.77],
       [10.2 ,  0.5 ]])

array([1.6, 1.4])
```

Notice:

* The data is **shuffled** before splitting.
* The default test size is **25%** of the dataset.

---

### **Using a Custom Test Size**

```python
split_dataset = train_test_split(data, labels, test_size=0.375)
```

This gives a **37.5%** test set and **62.5%** training set.

---

## **Why Split?**

Testing on the training set gives a **false sense of performance**.

A model that performs well on the training set but poorly on the testing set is said to be:

> **Overfitting** — it memorized instead of learning.

A proper train/test split prevents this.

---

# **Time to Code!**

Write a function that takes a dataset + labels and returns:

* **train_set** → `(train_data, train_labels)`
* **test_set** → `(test_data, test_labels)`

### ✔️ **Expected Implementation**

```python
def dataset_splitter(data, labels, test_size=0.25):
  split_dataset = train_test_split(data, labels, test_size=test_size)
  train_set = (split_dataset[0], split_dataset[2])
  test_set = (split_dataset[1], split_dataset[3])
  return train_set, test_set
```


