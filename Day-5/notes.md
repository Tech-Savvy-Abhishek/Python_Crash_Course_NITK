# Python Crash Course NITK - Day 5 Notes

---

# **1. `enumerate()` Function**  

## **Overview**  
`enumerate()` adds a counter to an iterable and returns an iterator of tuples containing the index and the value.

---

### **Syntax**  
```python
enumerate(iterable, start=0)
```  

- **iterable**: Any sequence (list, tuple, string).  
- **start**: Starting index (default = 0).  

---

### **Examples**  

1. **Basic Usage**  
   ```python
   fruits = ["apple", "banana", "cherry"]
   for index, fruit in enumerate(fruits):
       print(index, fruit)
   # Output:
   # 0 apple
   # 1 banana
   # 2 cherry
   ```

2. **Custom Start Index**  
   ```python
   for index, fruit in enumerate(fruits, start=1):
       print(index, fruit)
   # Output:
   # 1 apple
   # 2 banana
   # 3 cherry
   ```

---

### **Edge Cases & Tricks**  

- **Convert to List of Tuples**  
  ```python
  print(list(enumerate("hello")))
  # Output: [(0, 'h'), (1, 'e'), (2, 'l'), (3, 'l'), (4, 'o')]
  ```

- **Index Filtering**  
  ```python
  nums = [10, 20, 30, 40, 50]
  even_indices = [num for idx, num in enumerate(nums) if idx % 2 == 0]
  print(even_indices)  # Output: [10, 30, 50]
  ```

---

# **2. Lists in Python**  

## **Overview**  
A list is a mutable, ordered collection of items that can hold elements of different types.

---

### **List Creation**  

1. **Empty List**  
   ```python
   my_list = []
   ```

2. **With Elements**  
   ```python
   my_list = [1, "hello", 3.14, True]
   ```

---

### **Accessing Elements**  

1. **Indexing**  
   ```python
   print(my_list[1])  # Output: hello
   ```

2. **Negative Indexing**  
   ```python
   print(my_list[-1])  # Output: True
   ```

3. **Slicing**  
   ```python
   print(my_list[1:3])  # Output: ['hello', 3.14]
   ```

---

### **Modifying Elements**  

1. **Update**  
   ```python
   my_list[1] = "world"
   print(my_list)  # Output: [1, 'world', 3.14, True]
   ```

2. **Insert**  
   ```python
   my_list.insert(2, "Python")
   print(my_list)  # Output: [1, 'world', 'Python', 3.14, True]
   ```

3. **Delete**  
   ```python
   del my_list[0]
   print(my_list)  # Output: ['world', 'Python', 3.14, True]
   ```

---

# **3. List Methods**  

---

### **1. `append()`**  
Adds an element to the end of the list.  

```python
my_list.append("new")
print(my_list)  # Output: [1, 2, 3, 'new']
```

---

### **2. `extend()`**  
Extends the list by adding elements from another iterable.  

```python
my_list.extend([4, 5, 6])
print(my_list)  # Output: [1, 2, 3, 4, 5, 6]
```

---

### **3. `insert()`**  
Inserts an element at a specified position.  

```python
my_list.insert(1, "inserted")
print(my_list)  # Output: [1, 'inserted', 2, 3]
```

---

### **4. `remove()`**  
Removes the first occurrence of a value.  

```python
my_list.remove(2)
print(my_list)  # Output: [1, 'inserted', 3]
```

---

### **5. `pop()`**  
Removes and returns the last element or a specified index.  

```python
my_list.pop()     # Removes last element
my_list.pop(1)    # Removes element at index 1
```

---

### **6. `clear()`**  
Removes all elements from the list.  

```python
my_list.clear()
print(my_list)  # Output: []
```

---

### **7. `index()`**  
Returns the first occurrence of a value.  

```python
my_list = [1, 2, 3, 2, 4]
print(my_list.index(2))  # Output: 1
```

---

### **8. `count()`**  
Counts occurrences of a value.  

```python
print(my_list.count(2))  # Output: 2
```

---

### **9. `sort()`**  
Sorts the list in ascending order (modifies original list).  

```python
my_list.sort()
print(my_list)  # Output: [1, 2, 3, 4]
```

---

### **10. `sorted()`**  
Returns a sorted version without modifying the original list.  

```python
print(sorted(my_list, reverse=True))  # Output: [4, 3, 2, 1]
```

---

### **11. `reverse()`**  
Reverses the list.  

```python
my_list.reverse()
print(my_list)  # Output: [4, 3, 2, 1]
```

---

# **Tricky Edge Cases**  

1. **Out-of-Range Indexing**  
   ```python
   my_list = [1, 2, 3]
   # print(my_list[5])  # IndexError: list index out of range
   ```

2. **Duplicate Removal with `remove()`**  
   ```python
   my_list = [1, 2, 3, 2, 4]
   my_list.remove(2)
   print(my_list)  # Output: [1, 3, 2, 4] (removes first occurrence)
   ```

3. **Copy vs Reference**  
   ```python
   list1 = [1, 2, 3]
   list2 = list1  # Both refer to the same list
   list2.append(4)
   print(list1)  # Output: [1, 2, 3, 4] (both lists are updated)
   ```

4. **Copy Using `copy()`**  
   ```python
   list1 = [1, 2, 3]
   list2 = list1.copy()  # Creates a new list
   list2.append(4)
   print(list1)  # Output: [1, 2, 3]
   ```

5. **List Comprehension Trick**  
   ```python
   squares = [x ** 2 for x in range(5)]
   print(squares)  # Output: [0, 1, 4, 9, 16]
   ```

6. **Unpacking in Lists**  
   ```python
   a, *b, c = [1, 2, 3, 4, 5]
   print(a, b, c)  # Output: 1 [2, 3, 4] 5
   ```

---

### End of Day 5 Notes 🎉