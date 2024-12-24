# Python Crash Course NITK - Day 14 Notes


Object-Oriented Programming (OOP) is a programming paradigm based on the concept of objects. Python makes it simple to implement OOP through its syntax and dynamic typing.

---

# **1. Key Concepts in OOP**  
### **1.1. Classes and Objects**  
- **Class:** A blueprint for creating objects.  
- **Object:** An instance of a class, containing attributes (data) and methods (functions).  


### **1.2. Attributes and Methods**  
- **Attributes:** Variables associated with an object (e.g., `self.name`).  
- **Methods:** Functions defined inside a class and act upon its objects.


---

# **2. The `__init__` Method**  
- Special method called automatically when an object is created.  
- Used to initialize an object’s attributes.  


### **Syntax:**  
```python
class MyClass:
    def __init__(self, attribute1, attribute2):
        self.attribute1 = attribute1
        self.attribute2 = attribute2
```


### **Example:**  
```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

s1 = Student("Alice", 21)
print(s1.name)  # Output: Alice
print(s1.age)   # Output: 21
```

**Tricky Point:**  
`__init__` is not a constructor but an initializer in Python. Constructors are handled by `__new__`.

In Python, the methods `__new__` and `__init__` are both related to object creation, but they serve different purposes in the lifecycle of an object. 

### **`__new__`: The Constructor**
- **Role**: `__new__` is the actual constructor in Python. It is responsible for creating and returning a new instance of a class.
- **When it's called**: It is invoked **before** the `__init__` method.
- **Primary responsibility**: Allocates memory for the object and creates it.
- **Return value**: Must return an instance of the class (or a subclass). If it doesn't, Python will raise an error.
- **Customization**: If you want to control how an object is created (e.g., implementing a singleton pattern, or using a factory design), you override `__new__`.

**Example of `__new__`:**
```python
class CustomClass:
    def __new__(cls, *args, **kwargs):
        print("Creating instance in __new__")
        instance = super().__new__(cls)
        return instance

    def __init__(self, value):
        print("Initializing instance in __init__")
        self.value = value

obj = CustomClass(42)
```
**Output:**
```
Creating instance in __new__
Initializing instance in __init__
```


### **`__init__`: The Initializer**
- **Role**: `__init__` is not a constructor but an initializer. It initializes the already-created object.
- **When it's called**: It is invoked **after** the object has been created by `__new__`.
- **Primary responsibility**: Initializes the attributes of the object and sets up its state.
- **Return value**: Does not return anything (returns `None`).
- **Customization**: You typically override `__init__` to set initial values for instance attributes.

**Example of `__init__`:**
```python
class CustomClass:
    def __init__(self, value):
        print("Initializing instance")
        self.value = value

obj = CustomClass(42)
```
**Output:**
```
Initializing instance
```


### **Key Differences**
| Aspect              | `__new__`                             | `__init__`                     |
|---------------------|---------------------------------------|--------------------------------|
| **Purpose**         | Constructs and returns a new instance of the class. | Initializes the instance with specific attributes or states. |
| **Invocation**      | Automatically called when creating a new instance (`cls(*args, **kwargs)`). | Automatically called after `__new__` has created the object. |
| **Arguments**       | Takes the class itself (`cls`) as the first argument. | Takes the instance (`self`) as the first argument. |
| **Return Value**    | Must return an instance of the class. | Does not return anything (`None`). |
| **Overriding Use Cases** | Advanced use cases, like implementing a singleton or metaclass logic. | Setting up attributes and initializing the object's state. |


### **When to Use `__new__`?**
- If you need to customize how an instance of the class is created (e.g., creating instances from a pool, caching, or controlling subclassing).
- For immutable types (like `tuple`, `str`, etc.), where initialization must happen during object creation since they cannot be modified later.

### **When to Use `__init__`?**
- For typical classes, you almost always use `__init__` to initialize attributes and set up the object's state after it's been created by `__new__`.


### **An Immutable Example**
For immutable types like `tuple`, `__init__` can't be used to modify the object. Instead, you use `__new__` to customize its creation:

```python
class CustomTuple(tuple):
    def __new__(cls, iterable):
        print("In __new__")
        return super().__new__(cls, iterable)

    def __init__(self, iterable):
        print("In __init__")
        # Cannot modify the tuple here, as it's immutable

obj = CustomTuple([1, 2, 3])
print(obj)
```
**Output:**
```
In __new__
In __init__
(1, 2, 3)
```

### Summary
- **`__new__`**: Handles object creation and is the true constructor.
- **`__init__`**: Handles object initialization after creation.
Understanding this distinction is crucial when working with advanced object-oriented programming patterns in Python.


---

# **3. The `self` Parameter**  
- Represents the instance of the class.  
- Used to access instance variables and methods.  
- Must be the first parameter of instance methods.  


### **Tricky Concept:**  
The name `self` is just a convention. You can name it anything, but it’s recommended to stick to `self` for readability.  
```python
class Example:
    def display(this):
        print("Using 'this' instead of 'self'")
```


---

# **4. Access Specifiers**  
Python doesn’t have traditional private, protected, and public access specifiers like other languages. Instead, it uses naming conventions:  
- **Public (default):** Accessible anywhere (e.g., `self.name`).  
- **Protected (_variable):** Indicated by a single underscore (`_name`). Treated as non-public but accessible.  
- **Private (__variable):** Indicated by double underscores (`__name`). Name mangled to prevent unintentional access.



### **Example:**  
```python
class Test:
    def __init__(self):
        self.public = "I am public"
        self._protected = "I am protected"
        self.__private = "I am private"

t = Test()
print(t.public)       # Accessible
print(t._protected)   # Accessible but non-public
# print(t.__private)  # AttributeError
print(t._Test__private)  # Accessible using name mangling
```



---

# **5. Methods in Classes**  
### **5.1. Instance Methods**  
Operate on instance attributes. Require `self` as the first parameter.  

```python
class Person:
    def greet(self):
        print(f"Hello, my name is {self.name}")
```



### **5.2. Class Methods**  
Operate on class variables. Use `@classmethod` and `cls` as the first parameter.  

```python
class MyClass:
    class_variable = 0

    @classmethod
    def increment(cls):
        cls.class_variable += 1
```



### **5.3. Static Methods**  
Don’t operate on instance or class variables. Use `@staticmethod`.  

```python
class Math:
    @staticmethod
    def add(a, b):
        return a + b
```

Instance variables and class variables are two types of variables used in Python classes, and they differ in scope, accessibility, and behavior. 


### **Instance Variables**
- **Definition**: Variables that are tied to a specific instance of a class.
- **Scope**: Unique to each instance of the class.
- **Storage**: Stored in the instance’s `__dict__`.
- **Declaration**: Typically declared and initialized inside the `__init__` method using `self`.
- **Access**: Accessed and modified through the instance (`self.variable_name`).
- **Use Case**: Represent data that varies from one instance to another.

**Example of Instance Variables:**
```python
class Person:
    def __init__(self, name, age):
        self.name = name  # Instance variable
        self.age = age    # Instance variable

person1 = Person("Alice", 30)
person2 = Person("Bob", 25)

# Unique to each instance
print(person1.name, person1.age)  # Output: Alice 30
print(person2.name, person2.age)  # Output: Bob 25
```


### **Class Variables**
- **Definition**: Variables that are shared among all instances of a class.
- **Scope**: Belong to the class itself and not any specific instance.
- **Storage**: Stored in the class’s `__dict__`.
- **Declaration**: Declared directly inside the class body, outside any instance methods.
- **Access**: Accessed through the class (`ClassName.variable_name`) or an instance.
- **Use Case**: Represent data or behavior that should be the same across all instances of the class.

**Example of Class Variables:**
```python
class Person:
    species = "Homo sapiens"  # Class variable

    def __init__(self, name):
        self.name = name  # Instance variable

person1 = Person("Alice")
person2 = Person("Bob")

# Shared across all instances
print(person1.species)  # Output: Homo sapiens
print(person2.species)  # Output: Homo sapiens

# Modify class variable
Person.species = "Homo sapiens sapiens"
print(person1.species)  # Output: Homo sapiens sapiens
print(person2.species)  # Output: Homo sapiens sapiens
```


### **Key Differences**
| Aspect              | Instance Variable                      | Class Variable                  |
|---------------------|----------------------------------------|---------------------------------|
| **Belongs To**      | A specific instance of the class.      | The class itself, shared among all instances. |
| **Storage**         | Stored in the `__dict__` of the instance. | Stored in the `__dict__` of the class. |
| **Scope**           | Unique for each instance.              | Shared across all instances.   |
| **Access**          | Accessed using `self.variable_name`.   | Accessed using `ClassName.variable_name` or `self.variable_name`. |
| **Declaration**     | Inside instance methods (usually `__init__`). | Inside the class body, outside methods. |
| **Modification**    | Modifying through an instance affects only that instance. | Modifying through the class affects all instances (unless overridden in an instance). |


### **Example Demonstrating the Difference**
```python
class Example:
    class_var = "Shared"  # Class variable

    def __init__(self, instance_var):
        self.instance_var = instance_var  # Instance variable

# Creating instances
obj1 = Example("Unique to obj1")
obj2 = Example("Unique to obj2")

# Accessing instance and class variables
print(obj1.instance_var)  # Output: Unique to obj1
print(obj2.instance_var)  # Output: Unique to obj2
print(obj1.class_var)     # Output: Shared
print(obj2.class_var)     # Output: Shared

# Modifying instance variable
obj1.instance_var = "Changed for obj1"
print(obj1.instance_var)  # Output: Changed for obj1
print(obj2.instance_var)  # Output: Unique to obj2

# Modifying class variable
Example.class_var = "Modified Class Variable"
print(obj1.class_var)     # Output: Modified Class Variable
print(obj2.class_var)     # Output: Modified Class Variable
```


### **Instance-Specific Override of Class Variables**
If you assign a value to a class variable through an instance, it creates an **instance-specific copy**, leaving the original class variable unchanged:

```python
class Example:
    class_var = "Shared"

obj1 = Example()
obj2 = Example()

obj1.class_var = "Instance-specific"  # Overrides only for obj1

print(obj1.class_var)  # Output: Instance-specific
print(obj2.class_var)  # Output: Shared
print(Example.class_var)  # Output: Shared
```

This behavior can sometimes lead to confusion, so it's important to know when and where to use class and instance variables.


---

# **6. Inheritance**  
Inheritance allows one class to derive properties and methods from another.



### **Syntax:**  
```python
class Parent:
    pass

class Child(Parent):
    pass
```



### **Types of Inheritance:**  
1. **Single Inheritance:** One parent, one child.  
2. **Multiple Inheritance:** One child, multiple parents.  
   ```python
   class A: pass
   class B: pass
   class C(A, B): pass
   ```
3. **Multilevel Inheritance:** Chain of inheritance.  
4. **Hierarchical Inheritance:** One parent, multiple children.  



### **Method Overriding:**  
Allows a child class to redefine a method from its parent.  
```python
class Parent:
    def greet(self):
        print("Hello from Parent")

class Child(Parent):
    def greet(self):
        print("Hello from Child")

c = Child()
c.greet()  # Output: Hello from Child
```

---

# **7. Tricky and Confusing Concepts in OOP**  


### **1. Variable Shadowing:**  
When instance and class variables have the same name.  
```python
class Test:
    var = 10
    def __init__(self, var):
        self.var = var

t = Test(20)
print(t.var)   # Instance variable: 20
print(Test.var)  # Class variable: 10
```


### **2. Multiple Inheritance Conflicts:**  
Handled by the **Method Resolution Order (MRO)**.  
```python
class A: pass
class B: pass
class C(A, B): pass

print(C.mro())  # Outputs the hierarchy of class resolution
```


### **3. Private Members and Inheritance:**  
Private members are not inherited directly.  

```python
class Parent:
    __private = "Private"

class Child(Parent):
    pass

c = Child()
# print(c.__private)  # Error
```


---

# **8. Practical Examples**  
### **Example: Real-World Bank Account Class**  
```python
class BankAccount:
    def __init__(self, owner, balance=0):
        self.owner = owner
        self.__balance = balance  # Private attribute

    def deposit(self, amount):
        self.__balance += amount

    def withdraw(self, amount):
        if amount <= self.__balance:
            self.__balance -= amount
        else:
            print("Insufficient funds")

    def get_balance(self):
        return self.__balance

# Usage
account = BankAccount("Alice", 1000)
account.deposit(500)
print(account.get_balance())  # Output: 1500
account.withdraw(2000)        # Output: Insufficient funds
```

---

### **Example: Employee and Manager Inheritance**  
```python
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def display(self):
        print(f"Name: {self.name}, Salary: {self.salary}")

class Manager(Employee):
    def __init__(self, name, salary, department):
        super().__init__(name, salary)
        self.department = department

    def display(self):
        super().display()
        print(f"Department: {self.department}")

m = Manager("John", 90000, "HR")
m.display()
```

---

### End of Day 14 Notes 🎉
