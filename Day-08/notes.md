# Python Crash Course NITK - Day 8 Notes

---

## **1. Nested Lists in Python**  

### **What Are Nested Lists?**  
- A list that contains other lists as its elements.  
- Used for creating matrices, tables, and complex data structures.  



### **Creating a Nested List**  
```python
nested_list = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
```


### **Accessing Elements in Nested Lists**  
```python
# Accessing element 5
print(nested_list[1][1])  # Output: 5
```


### **Modifying Elements**  
```python
nested_list[2][1] = 88
print(nested_list)  # Output: [[1, 2, 3], [4, 5, 6], [7, 88, 9]]
```


### **Tricky Edge Cases:**  
1. **IndexError in Nested Lists:**  
   ```python
   print(nested_list[3][0])  # IndexError: list index out of range
   ```

2. **Negative Indexing in Nested Lists:**  
   ```python
   print(nested_list[-1][-1])  # Output: 9
   ```

---

## **2. Nested Lists with List Comprehension**  

### **Syntax:**  
```python
[[expression for item in outer_list] for item in inner_list]
```



### **Example:** Creating a 3x3 Matrix  
```python
matrix = [[j for j in range(3)] for i in range(3)]
print(matrix)  # Output: [[0, 1, 2], [0, 1, 2], [0, 1, 2]]
```


### **More Examples:**  

1. **Multiplication Table:**  
   ```python
   table = [[i * j for j in range(1, 6)] for i in range(1, 6)]
   print(table)
   ```

2. **Flatten a Nested List:**  
   ```python
   flat_list = [num for sublist in nested_list for num in sublist]
   print(flat_list)  # Output: [1, 2, 3, 4, 5, 6, 7, 88, 9]
   ```

---


## **3. `dir()` Function**  

### **What It Does:**  
- Returns a list of all attributes and methods of an object.



### **Example:**  
```python
print(dir(list))  # Shows all list methods
```



### **Tricky Points:**  
1. **Using `dir()` on Custom Objects:**  
   ```python
   class MyClass:
       def my_method(self):
           pass
   
   obj = MyClass()
   print(dir(obj))
   ```

2. **Hidden Attributes Start with `__`:**  
   ```python
   print(dir(obj))  # Shows __init__, __str__, etc.
   ```


---

## **4. Handling JSON in Python**  

### **Importing JSON Module**  
```python
import json
```


### **4.1. `json.dump()` Method**  

- **Purpose:** Write JSON data to a file.  



**Syntax:**  
```python
json.dump(data, file_object, indent=4)
```


**Example:**  
```python
data = {"name": "Alice", "age": 25, "city": "Wonderland"}
with open("data.json", "w") as file:
    json.dump(data, file, indent=4)
```


### **4.2. `json.load()` Method**  

- **Purpose:** Load JSON data from a file.  


**Example:**  
```python
with open("data.json", "r") as file:
    loaded_data = json.load(file)
    print(loaded_data)  # Output: {'name': 'Alice', 'age': 25, 'city': 'Wonderland'}
```


### **Tricky Points:**  
1. **Handling Invalid JSON:**  
   ```python
   try:
       json.loads('{"key": value}')  # Missing quotes around value
   except json.JSONDecodeError:
       print("Invalid JSON!")
   ```

2. **Data Type Conversion:**  
   ```python
   json_string = '{"name": "Bob", "age": 30}'
   python_dict = json.loads(json_string)
   print(type(python_dict))  # Output: <class 'dict'>
   ```



---

## **5. Pandas Library in Python**  

### **Importing Pandas**  
```python
import pandas as pd
```


### **5.1. `read_csv()` Method**  

- **Purpose:** Reads data from a CSV file into a DataFrame.



**Syntax:**  
```python
df = pd.read_csv("data.csv")
```


**Example:**  
```python
df = pd.read_csv("data.csv")
print(df.head())  # Displays the first 5 rows
```


### **Tricky Points:**  
1. **Handling Missing Files:**  
   ```python
   try:
       df = pd.read_csv("non_existent_file.csv")
   except FileNotFoundError:
       print("File not found!")
   ```

2. **Custom Delimiters:**  
   ```python
   df = pd.read_csv("data.csv", delimiter=';')
   ```



### **5.2. DataFrame Methods**  

#### **1. `info()`**  

- **Purpose:** Shows summary of the DataFrame.  


**Example:**  
```python
print(df.info())
```


#### **2. `describe()`**  

- **Purpose:** Generates summary statistics for numerical columns.  


**Example:**  
```python
print(df.describe())
```


#### **3. `head()` and `tail()`**  

- **Purpose:** Displays the first or last few rows.  


**Example:**  
```python
print(df.head())   # First 5 rows
print(df.tail(3))  # Last 3 rows
```


#### **4. Accessing Data Using `loc[]`**  


**Example:**  
```python
# Access rows by label
print(df.loc[0])  # First row

# Access a specific column
print(df.loc[:, "column_name"])

# Access specific rows and columns
print(df.loc[0:2, ["column_1", "column_2"]])
```


### **Tricky Points:**  

1. **Indexing Error:**  
   ```python
   print(df.loc[100])  # KeyError if 100 doesn't exist
   ```

2. **Setting a New Index:**  
   ```python
   df.set_index("column_name", inplace=True)
   print(df.head())
   ```


---

### **End of Day 8 Notes 🎉**

