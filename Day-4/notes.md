# Python Crash Course NITK - Day 4 Notes

---

# **1. `range()` Function**  

## **Overview**  
`range()` generates a sequence of numbers, primarily used in loops.

### **Syntax**  
```python
range(start, stop, step)
```  
- **start** (optional): Starting number (default = 0).  
- **stop** (required): Ending number (exclusive).  
- **step** (optional): Increment or decrement (default = 1).  

---

### **Examples**  

1. **Basic Usage**  
   ```python
   for i in range(5):  
       print(i)  # Output: 0 1 2 3 4
   ```

2. **Custom Start & Step**  
   ```python
   for i in range(2, 10, 2):  
       print(i)  # Output: 2 4 6 8
   ```

3. **Negative Step**  
   ```python
   for i in range(10, 0, -2):  
       print(i)  # Output: 10 8 6 4 2
   ```

4. **Edge Cases**  
   ```python
   range(1, 5, 0)  # ValueError: step must not be zero
   ```

---

# **2. `len()` Function**  

## **Overview**  
`len()` returns the number of elements in objects like strings, lists, tuples, dictionaries, and sets.  

### **Syntax**  
```python
len(obj)
```  

---

### **Examples**  

1. **Strings**  
   ```python
   s = "Python"
   print(len(s))  # Output: 6
   ```

2. **Lists**  
   ```python
   lst = [1, 2, 3, 4]
   print(len(lst))  # Output: 4
   ```

3. **Dictionaries**  
   ```python
   d = {'a': 1, 'b': 2}
   print(len(d))  # Output: 2
   ```

4. **Edge Cases**  
   ```python
   print(len(""))    # Output: 0 (empty string)
   print(len([]))    # Output: 0 (empty list)
   print(len({}))    # Output: 0 (empty dictionary)
   ```

---

# **3. Strings in Python**  

Python strings are **immutable** sequences of characters.

---

## **String Operations**  

### **a) Membership Operators `in`, `not in`**  

Check if a substring exists.  

```python
s = "hello world"

print("world" in s)    # True
print("WORLD" in s)    # False (case-sensitive)
print("world" not in s)  # False
```

---

### **b) String Methods**  

#### **1. `index()`**  
Returns the first occurrence of a substring or raises `ValueError`.  

```python
s = "programming"
print(s.index("g"))  # Output: 3
```

#### **Edge Case**  
```python
s.index("z")  # ValueError: substring not found
```

---

#### **2. `count()`**  
Counts occurrences of a substring.  

```python
s = "mississippi"
print(s.count("s"))   # Output: 4
print(s.count("ss"))  # Output: 2 (overlapping considered)
```

---

#### **3. `find()`**  
Similar to `index()`, but returns `-1` if the substring is not found.  

```python
print(s.find("g"))   # Output: 3
print(s.find("z"))   # Output: -1
```

---

#### **4. `replace()`**  
Replaces occurrences of a substring with another.  

```python
s = "hello world"
print(s.replace("world", "Python"))  # Output: hello Python
```

---

#### **5. `startswith()` & `endswith()`**  
Check if a string starts or ends with a specific substring.  

```python
print(s.startswith("hello"))  # True
print(s.endswith("Python"))   # False
```

---

#### **6. `strip()`, `lstrip()`, `rstrip()`**  
Remove whitespace from strings.  

```python
s = "  hello world  "
print(s.strip())   # Output: "hello world"
print(s.lstrip())  # Output: "hello world  "
print(s.rstrip())  # Output: "  hello world"
```

---

### **Character Functions**  

#### **1. `ord()`**  
Returns the ASCII/Unicode code of a character.  

```python
print(ord("A"))   # Output: 65
print(ord("a"))   # Output: 97
print(ord(" "))   # Output: 32
```

#### **2. `chr()`**  
Returns the character for a given ASCII/Unicode code.  

```python
print(chr(65))   # Output: A
print(chr(97))   # Output: a
```

---

#### **3. `min()` & `max()`**  
Finds the minimum and maximum character based on Unicode values.  

```python
s = "hello"
print(min(s))  # Output: 'e'
print(max(s))  # Output: 'o'
```

---

### **String Comparisons**  

Python compares strings lexicographically based on Unicode values.  

```python
print("apple" < "banana")  # True
print("Zebra" < "apple")   # True
```

---

# **4. String Slicing**  

## **Overview**  
Extract portions of a string using `s[start:stop:step]`.  

---

### **Examples**  

1. **Basic Slicing**  
   ```python
   s = "Python"
   print(s[1:4])   # Output: "yth"
   ```

2. **Skipping Characters**  
   ```python
   print(s[0:6:2])  # Output: "Pto"
   ```

3. **Negative Indexing**  
   ```python
   print(s[-1])     # Output: "n"
   print(s[-3:-1])  # Output: "ho"
   ```

4. **Reversing a String**  
   ```python
   print(s[::-1])  # Output: "nohtyP"
   ```

---

### **Edge Cases & Gotchas**  

- **Start >= Stop** returns an empty string:  
  ```python
  print(s[4:2])  # Output: ""
  ```

- **Step = 0** raises an error:  
  ```python
  print(s[::0])  # ValueError: slice step cannot be zero
  ```

---

# **Recap**  

1. **`range()` Negative Steps**: Be careful with start/stop values.  
2. **`len()` on Empty Objects**: Returns 0, not an error.  
3. **String Operations**: Many methods are case-sensitive (`in`, `count`, `index`).  
4. **Slicing Bounds**: Out-of-range indices don’t throw an error but adjust to limits.  
5. **Comparisons & Unicode Values**: Use `ord()` and `chr()` to understand custom sorting.  
6. **Find vs Index**: `find()` returns `-1`, while `index()` raises an error.  

---
### End of Day 4 Notes 🎉