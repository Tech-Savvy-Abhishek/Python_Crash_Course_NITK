# Python Crash Course NITK - Day 3 Notes

## **1. `random.randint()` Function**
The `random.randint(a, b)` function generates a random integer between two specified values **a** and **b**, **inclusive**.

### **Syntax**:
```python
import random
random.randint(a, b)
```

### **Key Points**:
- Both endpoints, **a** and **b**, are included in the range.
- Requires the `random` module.
- Returns a single integer.

### **Examples and Edge Cases**:
1. **Basic Usage**:
    ```python
    import random
    print(random.randint(1, 10))  # Output: Random number between 1 and 10
    ```

2. **Edge Case: `a == b`**  
   If `a` equals `b`, the function will always return that value:
    ```python
    print(random.randint(5, 5))  # Output: 5
    ```

3. **Edge Case: `a > b`**  
   Throws a `ValueError` because it’s logically invalid:
    ```python
    print(random.randint(10, 5))  # ValueError: empty range for randint()
    ```

4. **Tricky Logic**:  
   Generating random even numbers between 1 and 10:
    ```python
    print(random.randint(1, 5) * 2)  # Outputs only even numbers
    ```

5. **Performance Consideration**:
   - For large ranges (e.g., `random.randint(1, 10**6)`), the function remains efficient.
   - For biased randomness (e.g., custom probabilities), `random.choices()` is preferred.

---

## **2. Logical Operators**

### **Overview**:
Logical operators allow combining multiple conditions in a single expression. They work on Boolean values (`True` or `False`).

| Operator | Description                | Example               |
|----------|----------------------------|-----------------------|
| `and`    | True if **both** conditions are True. | `x > 5 and y < 10` |
| `or`     | True if **at least one** condition is True. | `x > 5 or y < 10` |
| `not`    | Inverts the Boolean value.   | `not(x > 5)`         |

### **Evaluation Order**:
- `and` is evaluated before `or`.  
- Use parentheses for clarity.

### **Examples**:
1. **Basic Usage**:
    ```python
    x, y = 3, 7
    print(x > 2 and y < 10)  # True
    print(x < 2 or y < 10)   # True
    print(not(x > 2))        # False
    ```

2. **Short-Circuiting**:
   - Logical operators stop evaluating as soon as the result is determined:
     ```python
     x = 5
     print(x > 2 or (10 / 0))  # True (division by 0 never happens)
     print(x < 2 and (10 / 0)) # False (division by 0 never happens)
     ```

3. **Edge Case with Truthy/Falsy Values**:
   - Python treats certain non-boolean values as `True` or `False`:
     ```python
     print(0 or 5)      # 5 (0 is falsy)
     print(not "hello") # False (non-empty strings are truthy)
     ```

4. **Non-Boolean Results**:
   Logical operators return the last evaluated value:
   ```python
   print(3 and 5)  # 5 (both are truthy, returns last truthy value)
   print(0 or 10)  # 10 (returns first truthy value)
   ```

---

## **3. Operator Precedence**

### **Precedence Order**:
From highest to lowest:
1. **Parentheses**: `()`
2. **Exponentiation**: `**`
3. **Unary Operators**: `+`, `-`, `not`
4. **Multiplication/Division**: `*`, `/`, `//`, `%`
5. **Addition/Subtraction**: `+`, `-`
6. **Relational Operators**: `<`, `<=`, `>`, `>=`, `==`, `!=`
7. **Logical Operators**: `and`, `or`

### **Examples**:
1. **Basic Precedence**:
    ```python
    result = 3 + 5 * 2 ** 2
    # Step 1: Exponentiation (2 ** 2 = 4)
    # Step 2: Multiplication (5 * 4 = 20)
    # Step 3: Addition (3 + 20 = 23)
    print(result)  # Output: 23
    ```

2. **Custom Precedence with Parentheses**:
    ```python
    result = (3 + 5) * 2 ** 2
    # Step 1: Parentheses (3 + 5 = 8)
    # Step 2: Exponentiation (2 ** 2 = 4)
    # Step 3: Multiplication (8 * 4 = 32)
    print(result)  # Output: 32
    ```

3. **Combining Logical Operators**:
    ```python
    result = True or False and False
    # Step 1: `and` is evaluated first (False and False = False)
    # Step 2: `or` is evaluated (True or False = True)
    print(result)  # Output: True
    ```

4. **Tricky Case**:
    ```python
    print(not True or True and False)
    # Step 1: not True = False
    # Step 2: and is evaluated (True and False = False)
    # Step 3: or is evaluated (False or False = False)
    ```

---

## **4. `if`, `elif`, and `else`**

### **Overview**:
Used for conditional execution of code blocks.

### **Syntax**:
```python
if condition1:
    # Block for condition1
elif condition2:
    # Block for condition2
else:
    # Block for all other cases
```

### **Key Points**:
- **`if`**: Executes the block if the condition is `True`.
- **`elif`**: Checked only if the preceding conditions are `False`.
- **`else`**: Executes if no preceding conditions are `True`.

### **Examples**:
1. **Basic Usage**:
    ```python
    num = 10
    if num > 20:
        print("Greater than 20")
    elif num == 10:
        print("Equal to 10")
    else:
        print("Less than 10")
    ```

2. **Edge Case: Multiple `elif` Statements**:
   Only the first `True` condition is executed:
    ```python
    x = 15
    if x > 10:
        print("A")
    elif x > 5:
        print("B")
    # Output: "A" (even though x > 5 is also True)
    ```

3. **Nested Conditions**:
    ```python
    x, y = 5, 10
    if x > 0:
        if y > 5:
            print("Both x and y are positive")
    ```

4. **Avoiding Redundancy**:
   Instead of multiple `if` statements:
    ```python
    # Inefficient
    if x > 5:
        print("X > 5")
    if x > 10:
        print("X > 10")
    ```

    Use:
    ```python
    if x > 10:
        print("X > 10")
    elif x > 5:
        print("X > 5")
    ```

---

## **5. Combining Concepts**

1. **Dice Roll Simulation**:
    ```python
    import random

    roll = random.randint(1, 6)
    if roll == 6:
        print("Jackpot! Rolled a 6")
    elif roll % 2 == 0:
        print(f"Even roll: {roll}")
    else:
        print(f"Odd roll: {roll}")
    ```

2. **Password Strength Checker**:
    ```python
    password = "Abc@1234"
    if len(password) < 8:
        print("Weak: Too short")
    elif not any(char.isdigit() for char in password):
        print("Weak: No numbers")
    elif not any(char.isupper() for char in password):
        print("Weak: No uppercase")
    elif not any(char in "@#$" for char in password):
        print("Weak: No special characters")
    else:
        print("Strong password")
    ```

3. **Guess the Number**:
    ```python
    import random
    secret = random.randint(1, 100)
    guess = int(input("Guess the number (1-100): "))

    if guess == secret:
        print("Correct!")
    elif guess > secret:
        print("Too high!")
    else:
        print("Too low!")
    ```

---
### End of Day 3 Notes 🎉