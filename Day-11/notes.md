# Python Crash Course NITK - Day 11 Notes

---

# **1. SciPy Overview**  
SciPy is a scientific computing library that builds on NumPy, providing advanced mathematical functions like linear algebra, optimization, and signal processing.



### **Installation:**  
```bash
pip install scipy
```

### **Importing:**  
```python
import numpy as np
from scipy import linalg, optimize
```

---

# **2. Solving a System of Linear Equations**  

### **Standard Form:**  
\[ Ax = B \]  

Where:  
- \( A \): Coefficient matrix  
- \( x \): Unknown variable matrix  
- \( B \): Constant matrix  

---

### **2.1. Using `linalg.solve()`**  

```python
A = np.array([[3, 2], [1, 4]])
B = np.array([7, 10])
x = linalg.solve(A, B)
print(x)  # Solution for x and y
```

**Edge Case:**  
- Throws `LinAlgError` if matrix A is singular (non-invertible).  

---

### **2.2. Checking the Result:**  

```python
# Verify if Ax = B
print(np.dot(A, x))  # Should return [7, 10]
```

---


# **3. Matrix Operations in SciPy**  



### **3.1. Matrix Inverse - `linalg.inv()`**  

```python
A = np.array([[1, 2], [3, 4]])
A_inv = linalg.inv(A)
print(A_inv)
```

**Tricky Points:**  
- Matrix must be square.  
- If determinant is 0, the matrix is singular (non-invertible).  

---

### **3.2. Determinant - `linalg.det()`**  

```python
det_A = linalg.det(A)
print(det_A)  # Output: -2.0
```

---

### **3.3. Matrix Multiplication - `@` Operator**  

```python
B = np.array([[2, 0], [1, 3]])
result = A @ B
print(result)
```

---


# **4. Optimization Using SciPy**  



### **4.1. Finding Roots - `optimize.root()`**  

---

#### **Example 1:** Solving a Non-Linear Equation  
Solve the equation: \( x^2 - 4 = 0 \)

```python
from scipy.optimize import root

def func(x):
    return x**2 - 4

solution = root(func, 0)  # Initial guess is 0
print(solution.x)  # Output: [2.]
```

---

### **4.2. Minimization - `optimize.minimize()`**  

---

#### **Example 2:** Minimize a Quadratic Function  
Minimize the function \( f(x) = x^2 + 3x + 2 \)

```python
def f(x):
    return x**2 + 3*x + 2

result = optimize.minimize(f, x0=0)  # Initial guess is 0
print(result.x)  # Minimum point
```

---


# **5. Meshgrid for 3D Plotting**  

### **Meshgrid Concept:**  
- `np.meshgrid()` creates a grid for plotting 2D functions.  

```python
import matplotlib.pyplot as plt

x = np.linspace(-5, 5, 10)
y = np.linspace(-5, 5, 10)

X, Y = np.meshgrid(x, y)
Z = X**2 + Y**2

plt.contourf(X, Y, Z)
plt.colorbar()
plt.show()
```

---


# **6. Curve Fitting**  

### **6.1. Linear Function Fitting**  

---

#### **Use Case:** Fitting a linear model: \( y = mx + c \)

```python
from scipy.optimize import curve_fit

# Define a linear function
def linear(x, m, c):
    return m * x + c

# Data points
x_data = np.array([1, 2, 3, 4, 5])
y_data = np.array([2.2, 2.8, 3.6, 4.5, 5.1])

# Perform curve fitting
params, _ = curve_fit(linear, x_data, y_data)
m, c = params

print(f"Slope: {m}, Intercept: {c}")
```

---

### **6.2. Polynomial Function Fitting**  

---

#### **Use Case:** Fit a polynomial function \( y = ax^2 + bx + c \)

```python
def polynomial(x, a, b, c):
    return a * x**2 + b * x + c

params, _ = curve_fit(polynomial, x_data, y_data)
a, b, c = params

print(f"Coefficients: a={a}, b={b}, c={c}")
```

---


# **Tricky and Confusing Points**  


1. **Singular Matrix Error:**  
   - If the matrix determinant is zero, `linalg.inv()` and `linalg.solve()` will fail.  

2. **Initial Guess in Root Finding:**  
   - A bad initial guess can lead to incorrect results or non-convergence.  

3. **Curve Fitting Assumptions:**  
   - Data points must closely follow the expected function model, or fitting will be inaccurate.

4. **Meshgrid Memory Use:**  
   - Large grids can cause memory overflow. Use small intervals when testing.  

---


### End of Day 11 Notes 🎉