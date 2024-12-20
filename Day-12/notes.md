# Python Crash Course NITK - Day 12 Notes

---

# **1. Introduction to Scikit-Learn**  
Scikit-learn is a popular Python library for machine learning. It provides tools for data preprocessing, model training, evaluation, and serialization.


### **Installation:**  
```bash
pip install scikit-learn
```

### **Importing the Library:**  
```python
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.neighbors import KNeighborsClassifier
from sklearn import metrics
from sklearn.svm import SVC
import pickle
```


---

# **2. Loading Datasets - `sklearn.datasets`**  

Scikit-learn includes several built-in datasets like the Iris dataset, useful for classification tasks.


### **Loading the Iris Dataset:**  
```python
from sklearn.datasets import load_iris

# Load the dataset
iris = load_iris()

# Features and target
X = iris.data   # Features
y = iris.target  # Target labels
```


### **Checking the Dataset:**  
```python
# View first 5 samples
print(X[:5])
print(y[:5])

# Dataset info
print(iris.feature_names)
print(iris.target_names)
```

---

# **3. Splitting the Dataset - `train_test_split()`**  


### **Why Split?**  
To avoid overfitting, we split the dataset into:  
- **Training Set:** For model training  
- **Testing Set:** For model evaluation  


### **Train-Test Split Example:**  
```python
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.3, random_state=42)
```

**Key Parameters:**  
- `test_size=0.3` → 30% for testing, 70% for training  
- `random_state=42` → Reproducibility  

---


# **4. K-Nearest Neighbors (KNN) Classifier**  


### **4.1. Model Training:**  
```python
# Initialize the KNN model
knn = KNeighborsClassifier(n_neighbors=3)

# Train the model
knn.fit(X_train, y_train)
```


### **4.2. Model Prediction:**  
```python
# Predict on the test set
y_pred = knn.predict(X_test)
```


### **4.3. Accuracy Score:**  
```python
# Calculate accuracy
accuracy = metrics.accuracy_score(y_test, y_pred)
print(f"Accuracy: {accuracy:.2f}")
```



### **Tricky Points:**  
- **Choosing `n_neighbors`:**  
  - Larger values smooth decision boundaries but can underfit.  
  - Smaller values can overfit the data.  

- **Distance Metric:**  
  - KNN uses Euclidean distance by default but supports other metrics using the `metric` parameter.  

---


# **5. Support Vector Machine (SVM)**  


### **5.1. Model Initialization:**  
```python
# Initialize the SVM model
svc = SVC(kernel='poly', C=10, gamma='scale')
```


### **Key Parameters:**  
- `kernel='poly'` → Polynomial kernel  
- `C=10` → Regularization strength (higher means less regularization)  
- `gamma='scale'` → Automatic kernel coefficient calculation  


### **5.2. Model Training:**  
```python
svc.fit(X_train, y_train)
```


### **5.3. Model Prediction:**  
```python
y_pred_svc = svc.predict(X_test)
```


### **5.4. Accuracy Score:**  
```python
accuracy_svc = metrics.accuracy_score(y_test, y_pred_svc)
print(f"SVM Accuracy: {accuracy_svc:.2f}")
```

---


# **6. Model Serialization Using Pickle**  



### **Why Serialize Models?**  
- Save trained models for later use.  
- Avoid retraining models every time.


### **6.1. Save the Model:**  
```python
# Save using Pickle
with open("knn_model.pkl", "wb") as f:
    pickle.dump(knn, f)
```

### **6.2. Load the Model:**  
```python
# Load the saved model
with open("knn_model.pkl", "rb") as f:
    loaded_model = pickle.load(f)

# Test the loaded model
loaded_pred = loaded_model.predict(X_test)
print("Loaded Model Accuracy:", metrics.accuracy_score(y_test, loaded_pred))
```

---


# **Tricky and Confusing Concepts**  



### **1. `train_test_split()` Shuffling**  
- If `random_state` is not set, the split is random every time.  
- Fix `random_state` for reproducibility.  



### **2. KNN Edge Cases:**  
- **Outliers:**  
  - Sensitive to outliers due to distance-based calculations.  
- **Feature Scaling:**  
  - KNN requires feature scaling using `StandardScaler()` or `MinMaxScaler()`.  


### **3. SVM Edge Cases:**  
- **Choosing C and Gamma:**  
  - **Low `C`:** Allows more margin violations → Underfitting  
  - **High `C`:** Reduces violations → Overfitting  
  - **Low `gamma`:** Broad influence of data points → Underfitting  
  - **High `gamma`:** Tight influence → Overfitting  


### **4. Pickle Pitfalls:**  
- Pickle files are not portable across different Python versions.  
- Do not load pickle files from untrusted sources due to security risks.  

---

### End of Day 12 Notes 🎉