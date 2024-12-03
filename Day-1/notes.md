# Python Crash Course NITK - Day 1 Notes

## 1. Operators in Python

### Arithmetic Operators
Python provides various arithmetic operators to perform mathematical operations.

| Operator | Description          | Example           | Output  |
|----------|----------------------|-------------------|---------|
| `+`      | Addition             | `5 + 3`           | `8`     |
| `-`      | Subtraction          | `10 - 4`          | `6`     |
| `*`      | Multiplication       | `7 * 2`           | `14`    |
| `/`      | Division (float)     | `9 / 2`           | `4.5`   |
| `%`      | Modulus (remainder)  | `10 % 3`          | `1`     |
| `//`     | Floor Division       | `10 // 3`         | `3`     |
| `**`     | Exponentiation       | `2 ** 3`          | `8`     |

### Tricky Concepts and Examples
1. **Integer Division vs Float Division:**
   ```python
   print(7 // 2)  # Output: 3 (integer floor division)
   print(7 / 2)   # Output: 3.5 (float division)
   ```

2. **Negative Modulus:**
   ```python
   print(-10 % 3)  # Output: 2
   # Formula: a = (a // b) * b + (a % b)
   # For -10 % 3: (-10 = (-4)*3 + 2)
   ```

3. **Chained Exponentiation:**
   ```python
   print(2 ** 3 ** 2)  # Output: 512
   # Exponentiation is evaluated right-to-left: 2 ** (3 ** 2) = 2 ** 9 = 512
   ```

4. **Operator Precedence:**
   ```python
   print(5 + 2 * 3 ** 2)  # Output: 23
   # Order: Exponentiation (**), Multiplication (*), Addition (+).
   ```

---

## 2. Types of Errors in Python

| Error Type       | Description                                                                 | Example                                   |
|------------------|-----------------------------------------------------------------------------|-------------------------------------------|
| `NameError`      | Occurs when referencing a variable that hasn't been defined.               | `print(x)` where `x` is undefined.       |
| `SyntaxError`    | Happens when Python cannot parse your code due to invalid syntax.          | `if True print("Hello")` (missing `:`).  |
| `TypeError`      | Raised when an operation is performed on an incompatible type.             | `3 + "3"` (int + string).                |
| `ValueError`     | Raised when a function receives an argument of correct type but invalid value. | `int("abc")`.                           |
| `IndexError`     | Raised when trying to access an index that is out of range in a list.      | `[1, 2][3]`                              |

### Tricky Scenarios
1. **Using Undefined Variables:**
   ```python
   def foo():
       print(x)  # NameError if x is not defined globally
   foo()
   ```

2. **Implied Tuple in SyntaxError:**
   ```python
   x = 10, 20  # This is valid (tuple assignment)
   x = (10 20)  # SyntaxError (missing comma).
   ```

---

## 3. Data Types

### Core Data Types
1. **Numeric Types:**
   - `int`, `float`, `complex`
   ```python
   x = 10      # int
   y = 3.14    # float
   z = 3 + 4j  # complex
   ```

2. **Sequence Types:**
   - `str`, `list`, `tuple`
   ```python
   name = "Alice"       # str
   fruits = ["apple", "banana"]  # list (mutable)
   point = (1, 2)       # tuple (immutable)
   ```

3. **Mapping Type:**
   - `dict`
   ```python
   d = {"name": "Alice", "age": 25}  # Key-value pairs
   ```

4. **Set Types:**
   - `set`, `frozenset`
   ```python
   unique_numbers = {1, 2, 3}  # set (mutable)
   frozen = frozenset({1, 2})  # frozenset (immutable)
   ```

5. **Boolean Type:**
   - `bool`
   ```python
   is_active = True
   is_logged_in = False
   ```

6. **None Type:**
   - Represents absence of value.
   ```python
   x = None
   ```

### Tricky Questions
1. **Type Conversion Pitfalls:**
   ```python
   print(int(3.9))  # Output: 3 (truncates, not rounds)
   print(float("3.14"))  # Output: 3.14
   ```

2. **Mutable vs Immutable:**
   ```python
   x = [1, 2, 3]  # Mutable
   x[0] = 0       # Allowed

   y = (1, 2, 3)  # Immutable
   y[0] = 0       # TypeError
   ```

---

## 4. Key Built-in Functions

### `type()`
- **Usage:** Determines the data type of an object.
```python
print(type(10))  # Output: <class 'int'>
print(type([1, 2, 3]))  # Output: <class 'list'>
```

#### Tricky Scenario:
```python
print(type(10) == int)  # Output: True
print(type(10.0) == float)  # Output: True
# Comparison works as expected, but type inheritance (like isinstance) is preferred.
```

### `print()`
- **Usage:** Displays output to the console.
```python
print("Hello, World!")  # Output: Hello, World!
```

#### Tricky Scenario:
1. **Separator (`sep`) and End (`end`) Parameters:**
   ```python
   print("Python", "Crash", "Course", sep="-")  # Output: Python-Crash-Course
   print("Hello", end="!")                      # Output: Hello!
   ```

2. **Printing to a File:**
   ```python
   with open("output.txt", "w") as f:
       print("Saving to file", file=f)
   ```

### `int()` and `float()`
- **Usage:** Convert values to integers or floating-point numbers.
```python
print(int(3.9))  # Output: 3
print(float(3))  # Output: 3.0
```

#### Tricky Scenario:
1. **String Conversion:**
   ```python
   print(int("42"))     # Output: 42
   print(float("3.14")) # Output: 3.14
   print(int("3.14"))   # Raises ValueError
   ```

2. **Binary Conversion:**
   ```python
   print(int("101", 2))  # Output: 5 (binary to decimal)
   ```

---

## 5. Functions

### Defining and Using Functions
Functions in Python are reusable blocks of code.
```python
def greet(name):
    return f"Hello, {name}!"

print(greet("Alice"))  # Output: Hello, Alice!
```

### Tricky Concepts
1. **Default Arguments:**
   ```python
   def add(x, y=5):
       return x + y

   print(add(3))      # Output: 8 (uses default value of y)
   print(add(3, 7))   # Output: 10
   ```

2. **Mutable Default Arguments Pitfall:**
   ```python
   def append_to_list(value, my_list=[]):
       my_list.append(value)
       return my_list

   print(append_to_list(1))  # Output: [1]
   print(append_to_list(2))  # Output: [1, 2] (shares same list!)
   ```
   - **Fix:**
     ```python
     def append_to_list(value, my_list=None):
         if my_list is None:
             my_list = []
         my_list.append(value)
         return my_list
     ```

3. **Lambda Functions:**
   - Anonymous functions created using `lambda`.
   ```python
   square = lambda x: x ** 2
   print(square(4))  # Output: 16
   ```

4. **Using Functions in Sorting:**
   ```python
   names = ["Alice", "Bob", "Eve"]
   names.sort(key=lambda x: len(x))
   print(names)  # Output: ['Bob', 'Eve', 'Alice']
   ```

---

### End of Day 1 Notes 🎉
