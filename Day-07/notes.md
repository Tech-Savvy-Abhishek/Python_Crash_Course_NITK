# Python Crash Course NITK - Day 7 Notes

---

## **1. Dictionary Methods: `.keys()`, `.values()`, `.items()`**  

### **1.1. `dict.keys()`**  
- **Returns**: A view object containing all keys in the dictionary.
- **Dynamic Nature**: Reflects changes in the dictionary.

**Example:**
```python
# Example usage of dict.keys()
d = {'a': 1, 'b': 2, 'c': 3}
keys = d.keys()
print(keys)  # Output: dict_keys(['a', 'b', 'c'])

d['d'] = 4
print(keys)  # Output: dict_keys(['a', 'b', 'c', 'd'])
```

### **1.2. `dict.values()`**  
- **Returns**: A view object containing all values in the dictionary.

**Example:**
```python
# Example usage of dict.values()
values = d.values()
print(values)  # Output: dict_values([1, 2, 3, 4])

d['a'] = 10
print(values)  # Output: dict_values([10, 2, 3, 4])
```

### **1.3. `dict.items()`**  
- **Returns**: A view object containing key-value pairs as tuples.

**Example:**
```python
# Example usage of dict.items()
items = d.items()
print(items)  # Output: dict_items([('a', 10), ('b', 2), ('c', 3), ('d', 4)])
```

### **Tricky Edge Cases:**
- **Type Conversion:**
  ```python
  print(list(d.keys()))    # Converts to list: ['a', 'b', 'c', 'd']
  print(tuple(d.values()))  # Converts to tuple: (10, 2, 3, 4)
  ```
- **Avoiding Key Errors:**
  ```python
  print(d.get('z', "Not Found"))  # Safe lookup, Output: Not Found
  ```

---

## **2. `dict.update()` Method**

- **Purpose**: Merges another dictionary or iterable into the dictionary.
- **Behavior**: Overwrites existing keys but keeps non-matching keys.

**Example:**
```python
# Example usage of dict.update()
d.update({'b': 20, 'e': 5})
print(d)  # Output: {'a': 10, 'b': 20, 'c': 3, 'd': 4, 'e': 5}
```

### **Tricky Edge Cases:**
- **Updating with an Iterable of Tuples:**
  ```python
  d.update([('f', 6), ('g', 7)])
  print(d)  # Output: {'a': 10, 'b': 20, 'c': 3, 'd': 4, 'e': 5, 'f': 6, 'g': 7}
  ```
- **Using `update()` on Empty Dictionaries:**
  ```python
  empty_dict = {}
  empty_dict.update(a=1, b=2)
  print(empty_dict)  # Output: {'a': 1, 'b': 2}
  ```

---

## **3. File Handling in Python**

### **File Modes:**
| Mode  | Description                  |
|-------|------------------------------|
| `r`   | Read-only (default)          |
| `w`   | Write (overwrite)            |
| `a`   | Append to the file           |
| `x`   | Create file, error if exists |
| `b`   | Binary mode                  |
| `t`   | Text mode (default)          |
| `+`   | Read/Write mode              |

---

### **Opening a File:**
```python
file = open("example.txt", "r")  # Opens in read mode
```
---

### **Reading a File:**

1. **`.read()` Method:**
   - Reads the entire file content as a string.

```python
file = open("example.txt", "r")
content = file.read()
print(content)
file.close()
```

2. **Read Line by Line:**
```python
file = open("example.txt", "r")
for line in file:
    print(line.strip())  # Removes trailing newlines
file.close()
```

3. **`.readline()` Method:**
   - Reads one line at a time.
```python
file = open("example.txt", "r")
print(file.readline())  # Reads the first line
print(file.readline())  # Reads the second line
file.close()
```

4. **`.readlines()` Method:**
   - Returns all lines as a list.
```python
file = open("example.txt", "r")
lines = file.readlines()
print(lines)  # Output: ['Line 1\n', 'Line 2\n', 'Line 3\n']
file.close()
```
---

### **Using `with open()` for Safe File Handling:**
```python
with open("example.txt", "r") as file:
    content = file.read()
    print(content)
```

- The file closes automatically when the block ends.

### **Why Use `with open()`?**
- **Automatic Resource Management:** No need to manually call `close()`.
- **Cleaner Code:** Simplifies file operations.



In Python, when you use the `with open(path) as fp` construct, you are creating a **context-managed block** that ensures the file is properly opened and closed. Here's how the scope behaves:


### **Scope of the Block:**
- The variable `fp` exists **only inside** the `with` block.
- After the `with` block ends, `fp` is automatically closed, and its scope is **terminated** unless it was defined outside the block.



### **Example 1: Access Within the Block**
```python
path = "example.txt"
with open(path, "r") as fp:
    content = fp.read()
    print(content)  # Works inside the block
```


### **What Happens Outside?**
```python
# Trying to access fp outside the block
print(fp)
```
**Output:** 
```python
NameError: name 'fp' is not defined
```
- `fp` is only defined within the `with` block and cannot be accessed outside.

---

### **Example 2: Storing Content for Use Outside**
```python
path = "example.txt"
with open(path, "r") as fp:
    content = fp.read()

# Access content outside the block
print(content)
```
**Output:**  
```python
# Prints file content
```
- Since `content` is defined outside the block, it can be accessed even after the file is closed.

---


### **Key Takeaways:**
- Variables created **inside** the `with` block (like `fp`) are **local** to the block.
- Variables **assigned** from the block (like `content`) can be accessed **outside** if declared outside the block.
- The file **closes automatically** when the block ends.

---

`content` is technically created **inside** the `with` block in this example:  

```python
path = "example.txt"
with open(path, "r") as fp:
    content = fp.read()  # Defined inside the block

# Access content outside the block
print(content)
```

---

### **Why Is `content` Accessible Outside the Block?**
- **Scope in Python:**  
  In Python, variables created inside a block like `with`, `for`, or `if` are still part of the **local function or global scope**, depending on where the code is executed.

- Since `content` is **assigned** inside the block but **not bound to the block**, its scope extends to the **entire function** or **global scope** if no function is defined.  

---

### **What Is Block-Limited in `with`?**
- **`fp` (the file pointer)** exists **only within** the `with` block because it is context-managed.
- Once the block ends, the file is **closed**, and the file pointer `fp` is **deleted**.

---

### **Clarification Example:**
```python
# Example without 'with'
fp = open("example.txt", "r")
content = fp.read()
fp.close()

# Both fp and content exist after the file is closed
print(fp)       # Still defined, but closed
print(content)  # Accessible
```

---

### **Summary:**
- Variables like `content` are accessible **outside** the `with` block because Python does not restrict their scope to the block itself.
- The **context manager** (`with open() as fp`) only manages the file's lifecycle and the variable `fp`, which becomes **undefined** after the block ends.

---

### **Writing to a File:**

1. **`.write()` Method:**
   - Writes a string to the file (overwrites existing content if in `w` mode).
```python
file = open("output.txt", "w")
file.write("This is a new file.\n")
file.write("File handling in Python is easy!\n")
file.close()
```

2. **`.writelines()` Method:**
   - Writes multiple lines at once using a list of strings.
```python
file = open("output.txt", "w")
lines = ["First line\n", "Second line\n", "Third line\n"]
file.writelines(lines)
file.close()
```
---

### **Best Practices:**
1. Use `with open()` to avoid manual closure:
```python
with open("example.txt", "r") as file:
    content = file.read()
    print(content)
```

2. Use Exception Handling for Robust Code:
```python
try:
    with open("example.txt", "r") as file:
        print(file.read())
except FileNotFoundError:
    print("File not found!")
```

---

### **End of Day 7 Notes 🎉**

