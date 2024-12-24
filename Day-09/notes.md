# Python Crash Course NITK - Day 9 Notes

---

# **1. NumPy Overview**  

- NumPy (Numerical Python) is a powerful library for numerical computing.  
- It supports large, multi-dimensional arrays and matrices with mathematical operations.  

---

### **Importing NumPy:**  
```python
import numpy as np
```

---

---

# **2. Creating Arrays in NumPy**  

---

### **2.1. `np.array()` - Creating a NumPy Array**  

```python
arr = np.array([1, 2, 3, 4])
print(arr)        # Output: [1 2 3]
print(type(arr))  # Output: <class 'numpy.ndarray'>
```

---

### **2.2. Creating Special Arrays:**  

---

#### **1. `np.zeros(shape)` - Array of Zeros**  
```python
zeros_arr = np.zeros((2, 3))
print(zeros_arr)
```
**Output:**  
```
[[0. 0. 0.]
 [0. 0. 0.]]
```

---

#### **2. `np.ones(shape)` - Array of Ones**  
```python
ones_arr = np.ones((3, 2))
print(ones_arr)
```

---

#### **3. `np.full(shape, value)` - Constant Array**  
```python
full_arr = np.full((2, 2), 7)
print(full_arr)
```

---

#### **4. `np.empty(shape)` - Uninitialized Array**  
```python
empty_arr = np.empty((2, 3))
print(empty_arr)
```
*Note:* Values will be random and depend on memory allocation.

---

#### **5. Identity Matrix:**  
```python
identity_matrix = np.eye(4)
print(identity_matrix)
```

---

---

# **3. Generating Ranges and Sequences**  

---

#### **1. `np.arange(start, stop, step)`**  

```python
range_arr = np.arange(1, 10, 2)
print(range_arr)  # Output: [1 3 5 7 9]
```

---

#### **2. `np.linspace(start, stop, num)`**  

```python
linear_space = np.linspace(0, 1, 5)
print(linear_space)  # Output: [0.   0.25 0.5  0.75 1. ]
```

---

---

# **4. Array Attributes**  

---

#### **1. `shape` - Array Dimensions**  
```python
arr = np.array([[1, 2, 3], [4, 5, 6]])
print(arr.shape)  # Output: (2, 3)
```

---

#### **2. `ndim` - Number of Dimensions**  
```python
print(arr.ndim)  # Output: 2
```

---

#### **3. `size` - Total Number of Elements**  
```python
print(arr.size)  # Output: 6
```

---

#### **4. `dtype` - Data Type of Elements**  
```python
print(arr.dtype)  # Output: int64 (may vary)
```

---

---

# **5. Array Indexing and Slicing**  

---

### **1. Indexing Elements:**  

```python
arr = np.array([[10, 20, 30], [40, 50, 60]])
print(arr[0, 1])  # Output: 20
```

---

### **2. Slicing Arrays:**  

```python
print(arr[0, :])   # Output: [10 20 30] (Entire Row)
print(arr[:, 1])   # Output: [20 50] (Entire Column)
```

---

### **Tricky Slicing Cases:**  
```python
# Reverse Rows
print(arr[::-1, :])  # Output: [[40 50 60], [10 20 30]]

# Reverse Columns
print(arr[:, ::-1])  # Output: [[30 20 10], [60 50 40]]
```

---

---

# **6. Reshaping Arrays**  

---

```python
arr = np.arange(1, 10)
reshaped = arr.reshape(3, 3)
print(reshaped)
```

---

### **Tricky Points:**  
- Reshape must preserve the number of elements:  
  ```python
  arr.reshape(2, 5)  # Error: Cannot reshape if dimensions don't match
  ```

---

---

# **7. Concatenation and Stacking**  

---

### **1. `np.concatenate()` - Joining Arrays**  
```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
concat_arr = np.concatenate((a, b))
print(concat_arr)  # Output: [1 2 3 4 5 6]
```

---

### **2. `np.vstack()` - Vertical Stack**  
```python
vstack_arr = np.vstack((a, b))
print(vstack_arr)
```

---

### **3. `np.hstack()` - Horizontal Stack**  
```python
hstack_arr = np.hstack((a, b))
print(hstack_arr)  # Output: [1 2 3 4 5 6]
```

---

---

# **8. Copying Arrays**  

---

### **1. Shallow Copy (`view`)**  
```python
arr = np.array([1, 2, 3])
view_arr = arr.view()
view_arr[0] = 100
print(arr)  # Output: [1 2 3] (Unchanged)
```

---

### **2. Deep Copy (`copy`)**  
```python
copy_arr = arr.copy()
copy_arr[0] = 500
print(arr)      # Output: [1 2 3] (Original)
print(copy_arr) # Output: [500 2 3]
```

---

---

# **9. Random Functions in NumPy**  

---

### **1. `np.random.rand()` - Random Float (0-1)**  
```python
random_float = np.random.rand(3, 3)
print(random_float)
```

---

### **2. `np.random.randint()` - Random Integers**  
```python
random_int = np.random.randint(1, 10, (2, 3))
print(random_int)
```

---

### **3. `np.random.randn()` - Random Values (Standard Normal)**  
```python
random_normal = np.random.randn(4, 4)
print(random_normal)
```

---

### **4. `np.random.choice()` - Random Sampling**  
```python
sample = np.random.choice([10, 20, 30, 40], 3)
print(sample)
```

---

---

# **Tricky Edge Cases and Confusing Concepts**  

1. **Reshaping Errors:**  
   ```python
   np.arange(10).reshape(3, 3)  # ValueError: Mismatched dimensions
   ```

2. **Copy vs View Confusion:**  
   ```python
   arr = np.array([1, 2, 3])
   b = arr.view()   # Shallow copy
   c = arr.copy()   # Deep copy
   b[0] = 100
   print(arr)  # Changed
   c[0] = 200
   print(arr)  # Unchanged
   ```

3. **Slicing in Multidimensional Arrays:**  
   ```python
   arr = np.arange(16).reshape(4, 4)
   print(arr[:, 1:3])  # Extracts sub-matrix
   ```

4. **Random Number Seed Fixation:**  
   ```python
   np.random.seed(42)
   print(np.random.rand())  # Fixed output every run
   ```

---

### **End of Day 9 Notes 🎉**

