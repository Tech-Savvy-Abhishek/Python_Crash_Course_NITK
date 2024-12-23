# Python Crash Course NITK - Day 13 Notes

---

## **1. Introduction to Matplotlib**  
Matplotlib is a powerful library for creating static, interactive, and animated visualizations in Python. It offers two main interfaces:  
1. **Pyplot Interface:** Simplified, state-based interface (`plt` module).  
2. **Object-Oriented Interface:** Greater control for advanced customizations.  


### **Installation:**  
```bash
pip install matplotlib
```

---


# **2. Basic Plotting with `plot()`**  
The `plot()` function is used to draw line plots.  


### **Syntax:**  
```python
plt.plot(x, y, linestyle, color, marker)
```


### **Example:**  
```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [2, 4, 6, 8, 10]

plt.plot(x, y, linestyle='--', color='blue', marker='o')
plt.xlabel("X-axis")
plt.ylabel("Y-axis")
plt.title("Basic Plot")
plt.show()
```

---

# **3. Customizing the Plot**  


### **3.1. Adding Labels and Title**  
- **`xlabel` and `ylabel`:** Add labels to axes.  
- **`title`:** Set the title of the plot.  

```python
plt.xlabel("X-axis Label")
plt.ylabel("Y-axis Label")
plt.title("Title of the Plot")
```


### **3.2. Setting Axis Limits**  
- **`xlim` and `ylim`:** Define the range for axes.  

```python
plt.xlim(0, 6)
plt.ylim(0, 12)
```


### **3.3. Adding a Legend**  
- **`legend`:** Display a legend for multiple plots.  

```python
plt.plot(x, y, label="Line 1")
plt.legend(loc='upper left')
```

**Tip:** Use `loc` for placement:  
- `'upper left'`, `'lower right'`, etc.


### **3.4. Adding Text to Canvas**  
- **`text(x, y, s)`:** Add text at a specific position.  

```python
plt.text(3, 6, "Point (3,6)")
```


### **3.5. Figure Customization**  
- **`figure()`:** Create or modify a figure.  

```python
plt.figure(figsize=(8, 6), dpi=100)
```


---

# **4. Styling and Line Properties**  



### **4.1. Linestyles (`linestyle`)**  
- `'-'` → Solid Line (default)  
- `'--'` → Dashed Line  
- `':'` → Dotted Line  
- `'-.'` → Dash-Dot Line  


### **4.2. Colors (`color`)**  
- Named Colors: `'red'`, `'blue'`, `'green'`, etc.  
- Hexadecimal Codes: `'#FF5733'`  


### **4.3. Markers (`marker`)**  
- `'o'` → Circle  
- `'s'` → Square  
- `'x'` → X  
- `'D'` → Diamond  


### **4.4. Using `plt.style`**  
Matplotlib provides predefined styles for plots.

```python
plt.style.use('ggplot')
```

Other popular styles include:
- `'seaborn'`  
- `'fivethirtyeight'`  
- `'bmh'`  

---


# **5. Subplots**  

Subplots allow multiple plots in one figure.


### **Using `subplot()`**  
```python
plt.subplot(nrows, ncols, index)
```

**Example:**
```python
plt.subplot(2, 1, 1)  # First subplot (2 rows, 1 column, index 1)
plt.plot(x, y)

plt.subplot(2, 1, 2)  # Second subplot (index 2)
plt.plot(x, [i**2 for i in x])
```


### **Using `subplots()` (OO Interface)**  
```python
fig, axes = plt.subplots(2, 1)
axes[0].plot(x, y)
axes[1].plot(x, [i**2 for i in x])
```


---

# **6. Object-Oriented Interface vs. Pyplot Interface**  



### **Object-Oriented Interface:**  
Provides more control.  

**Example:**
```python
fig, ax = plt.subplots()
ax.plot(x, y)
ax.set_xlabel("X-axis")
ax.set_ylabel("Y-axis")
```


### **Pyplot Interface:**  
Quick and easy but less customizable.  

**Example:**
```python
plt.plot(x, y)
plt.xlabel("X-axis")
plt.ylabel("Y-axis")
```


**Key Difference:**  
- **OO Interface:** Use `ax` objects for methods.  
- **Pyplot:** Use `plt` functions.


---

# **7. Tricky Concepts and Edge Cases**  


### **1. Legend Overlap:**  
Legends can overlap with data. Use `bbox_to_anchor`.  
```python
plt.legend(loc='upper right', bbox_to_anchor=(1.2, 1))
```


### **2. Dynamic Limits:**  
Avoid hardcoding limits:  
```python
plt.ylim(min(y) - 1, max(y) + 1)
```



### **3. Subplot Sharing:**  
Share axes between subplots for consistency.  
```python
fig, axes = plt.subplots(2, 1, sharex=True, sharey=True)
```


### **4. Combining Styles:**  
```python
plt.plot(x, y, linestyle='--', color='blue', marker='o')
```


### **5. Saving Figures:**  
Save a plot as an image using `savefig`.  
```python
plt.savefig("plot.png", dpi=300)
```

---

### End of Day 13 Notes 🎉
