# Python Crash Course NITK - Day 6 Notes

---

## **1. `round()` Function**  

### **Overview**  
`round()` is used to round a number to a specified number of decimal places.  

---

### **Syntax**  
```python
round(number, ndigits)
```
- **number**: The number to round.  
- **ndigits**: (Optional) Number of decimal places to round to.  

---

### **Examples**  

1. **Basic Rounding**  
   ```python
   print(round(3.14159, 2))  # Output: 3.14
   print(round(7.5))        # Output: 8 (rounds to nearest even number)
   ```

2. **Negative Decimal Places**  
   ```python
   print(round(4567, -2))   # Output: 4600
   ```


### What `-2` Means:
- A negative value for the `digits` argument indicates rounding to the nearest hundred in this case.  
- The function rounds to the left of the decimal point by the number of places specified by the negative value.

### Calculation:
- `4567` rounded to the nearest hundred is `4600`.  
- This is because:
  - The hundreds digit is `5`.
  - The next digit (`6`, in the tens place) is `>= 5`, so the hundreds digit is increased by 1, making it `4600`.

### Final Result:
**4600**


---

### **Tricky Edge Cases**  

- **Banker’s Rounding (Round Half to Even)**  
  ```python
  print(round(2.5))  # Output: 2 (rounds down)
  print(round(3.5))  # Output: 4 (rounds up)
  ```

The behavior is due to **Banker's Rounding** (also known as **Round Half to Even**) in Python. This rounding method is used to minimize cumulative rounding errors in numerical calculations.

### How It Works:
- When a number is exactly halfway between two integers (e.g., `2.5`, `3.5`), Python rounds **toward the nearest even number**.

### Why Use Banker's Rounding?
- This method reduces rounding bias in datasets with many numbers by balancing rounding up and down.

### Examples Explained:
```python
print(round(2.5))  # Output: 2
```
- `2.5` is halfway between `2` and `3`.
- The nearest even number is `2`, so it rounds down.

```python
print(round(3.5))  # Output: 4
```
- `3.5` is halfway between `3` and `4`.
- The nearest even number is `4`, so it rounds up.

### Summary:
- If the number is halfway between two integers, round to the **even** integer.
- This avoids bias in statistical and financial calculations where rounding repeatedly in the same direction could cause inaccuracies.

---

### Rounding Floats with Precision Errors  
```python
print(round(2.675, 2))  # Output: 2.67 (due to floating-point precision)
```

#### Why This Happens:
- Floating-point numbers are represented approximately in binary, causing precision issues.
- `2.675` cannot be represented exactly in binary, so it becomes something like `2.674999999...` internally.
- When rounded to two decimal places, Python sees `2.674999...` and rounds it **down** to `2.67`.  

#### How to Handle:
- Use the `Decimal` module for precise decimal arithmetic if exact rounding is critical:
  ```python
  from decimal import Decimal
  print(round(Decimal('2.675'), 2))  # Output: 2.68
  ```

---

## **2. List Comprehension**  

### **Overview**  
List comprehension provides a concise way to create lists using a single line of code.

---

### **Syntax**  
```python
[expression for item in iterable if condition]
```

---

### **Examples**  

1. **Basic Example**  
   ```python
   squares = [x**2 for x in range(5)]
   print(squares)  # Output: [0, 1, 4, 9, 16]
   ```

2. **With Condition**  
   ```python
   evens = [x for x in range(10) if x % 2 == 0]
   print(evens)  # Output: [0, 2, 4, 6, 8]
   ```

3. **Nested Comprehension**  
   ```python
   matrix = [[j for j in range(3)] for i in range(3)]
   print(matrix)  
   # Output: [[0, 1, 2], [0, 1, 2], [0, 1, 2]]
   ```

---

### **Tricky Edge Cases**  

- **Conditional Expressions**  
  ```python
  result = ["Even" if x % 2 == 0 else "Odd" for x in range(5)]
  print(result)  # Output: ['Even', 'Odd', 'Even', 'Odd', 'Even']
  ```

- **Avoiding Side Effects**  
  ```python
  data = [1, 2, 3]
  [data.append(x) for x in range(4, 6)]
  print(data)  # Avoid this pattern
  ```

---

## **3. Tuples**  

### **Overview**  
A tuple is an immutable, ordered collection of elements.

---

### **Tuple Methods**  

1. **`count()`**: Returns occurrences of a value.  
   ```python
   tup = (1, 2, 2, 3)
   print(tup.count(2))  # Output: 2
   ```

2. **`index()`**: Returns the first occurrence of a value.  
   ```python
   print(tup.index(3))  # Output: 3
   ```

---

### **Tricky Edge Cases**  

- **Single-Element Tuple**  
  ```python
  single = (5,)  # Must include a comma
  print(type(single))  # Output: <class 'tuple'>
  ```

- **Tuple Packing & Unpacking**  
  ```python
  a, b, *c = (1, 2, 3, 4)
  print(a, b, c)  # Output: 1 2 [3, 4]
  ```

---

## **4. Sets**  

### **Overview**  
A set is an unordered collection of unique items.

---

### **Set Methods**  

1. **`add()`**: Adds a single element.  
   ```python
   s = {1, 2, 3}
   s.add(4)
   print(s)  # Output: {1, 2, 3, 4}
   ```

2. **`update()`**: Adds multiple elements.  
   ```python
   s.update([5, 6])
   print(s)  # Output: {1, 2, 3, 4, 5, 6}
   ```

3. **`remove()` / `discard()`**: Removes an element.  
   ```python
   s.remove(2)  # Raises KeyError if not found
   s.discard(7)  # No error if not found
   ```

4. **`pop()`**: Removes and returns a random element.  
   ```python
   s.pop()
   print(s)
   ```

---

### **Tricky Edge Cases**  

- **Duplicate Removal**  
  ```python
  s = {1, 2, 2, 3}
  print(s)  # Output: {1, 2, 3}
  ```

- **Frozenset (Immutable Set)**  
  ```python
  fs = frozenset([1, 2, 3])
  # fs.add(4)  # Raises AttributeError
  ```

---

## **5. Dictionaries**  

### **Overview**  
A dictionary is a collection of key-value pairs, where keys are unique and immutable.

---

### **Dictionary Methods**  

1. **`get()`**: Retrieves a value.  
   ```python
   d = {'a': 1, 'b': 2}
   print(d.get('a'))  # Output: 1
   print(d.get('c', "Not Found"))  # Output: Not Found
   ```

2. **`keys()` / `values()` / `items()`**  
   ```python
   print(d.keys())    # Output: dict_keys(['a', 'b'])
   print(d.values())  # Output: dict_values([1, 2])
   print(d.items())   # Output: dict_items([('a', 1), ('b', 2)])
   ```

3. **`update()`**: Merges dictionaries.  
   ```python
   d.update({'c': 3})
   print(d)  # Output: {'a': 1, 'b': 2, 'c': 3}
   ```

4. **`pop()` / `popitem()`**  
   ```python
   d.pop('a')  # Removes key 'a'
   print(d)

   d.popitem()  # Removes last key-value pair
   ```

5. **`setdefault()`**: Sets default value if the key doesn’t exist.  
   ```python
   d.setdefault('d', 4)
   print(d)  # Output: {'b': 2, 'd': 4}
   ```

---
### **`zip()` Function in Python**
The `zip()` function combines elements from two or more iterables (like lists, tuples) into pairs or tuples. It stops when the shortest iterable is exhausted.

---

### **Creating a Dictionary Using `zip()`**
You can use `zip()` with lists to create a dictionary using the `dict()` constructor.

#### **Example 1: Basic Usage**
```python
keys = ['name', 'age', 'city']
values = ['Alice', 25, 'New York']

# Create a dictionary
result = dict(zip(keys, values))
print(result)
```
**Output:**
```python
{'name': 'Alice', 'age': 25, 'city': 'New York'}
```

---

### **How It Works:**
- `zip(keys, values)` pairs corresponding elements from `keys` and `values`.
- `dict()` converts these pairs into key-value pairs in a dictionary.

---

### **Key Concepts Related to `zip()`:**

#### 1. **Unequal Lengths**
If the lists have different lengths, `zip()` stops at the shortest list.
```python
keys = ['name', 'age']
values = ['Alice', 25, 'New York']

result = dict(zip(keys, values))
print(result)
```
**Output:**
```python
{'name': 'Alice', 'age': 25}
```

---

#### 2. **Unzipping with `zip()`**
You can reverse the process using the unpacking operator `*`.
```python
pairs = [('name', 'Alice'), ('age', 25), ('city', 'New York')]
keys, values = zip(*pairs)
print(keys)    # ('name', 'age', 'city')
print(values)  # ('Alice', 25, 'New York')
```

---

#### 3. **Multiple Lists with `zip()`**
You can combine multiple lists:
```python
list1 = [1, 2, 3]
list2 = ['a', 'b', 'c']
list3 = [True, False, True]

result = list(zip(list1, list2, list3))
print(result)
```
**Output:**
```python
[(1, 'a', True), (2, 'b', False), (3, 'c', True)]
```

---

#### 4. **Using Loops with `zip()`**
You can iterate through multiple lists using `zip()`:
```python
keys = ['name', 'age', 'city']
values = ['Alice', 25, 'New York']

for key, value in zip(keys, values):
    print(f'{key}: {value}')
```
**Output:**
```python
name: Alice
age: 25
city: New York
```
---

### **Summary:**
- Use `zip()` to combine lists into tuples or dictionaries.
- Stops when the shortest iterable is exhausted.
- Use `dict()` to create dictionaries and `*` to unpack zipped pairs.
- Works well in loops for paired iteration.

---


### **Tricky Edge Cases**  

- **Mutable Keys Not Allowed**  
  ```python
  # d = {[1, 2]: "invalid"}  # Raises TypeError
  ```

- **Dictionary Comprehension**  
  ```python
  squares = {x: x**2 for x in range(5)}
  print(squares)  # Output: {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
  ```

---

### End of Day 6 Notes 🎉