# Python

### **Ch 1. Introduction**
- **Python Overview**: Python is a high-level, interpreted language known for its readability and simplicity. It supports multiple paradigms like procedural, object-oriented, and functional programming.
- **Hello World**: 
  ```python
  print("Hello, World!")
  ```

### **Ch 2. Variables**
- **Variable Assignment**: No need for explicit declaration. Type inference is automatic.
  ```python
  x = 10
  name = "Alice"
  ```
- **Dynamic Typing**: Variables can change types.
  ```python
  x = 5
  x = "Now I'm a string"
  ```

### **Ch 3. Functions**
- **Defining Functions**:
  ```python
  def greet(name):
      return f"Hello, {name}!"
  print(greet("Alice"))
  ```
- **Default Arguments**:
  ```python
  def greet(name="World"):
      return f"Hello, {name}!"
  print(greet())
  ```

### **Ch 4. Scope**
- **Local vs. Global Variables**:
  ```python
  x = 10  # Global scope

  def func():
      x = 5  # Local scope
      print(x)
  func()  # Outputs 5
  print(x)  # Outputs 10
  ```
- **`global` Keyword**:
  ```python
  def func():
      global x
      x = 5
  func()
  print(x)  # Now outputs 5
  ```

### **Ch 5. Testing and Debugging**
- **`assert` Statement**: Helps with debugging by ensuring conditions hold true.
  ```python
  def add(a, b):
      return a + b
  assert add(2, 3) == 5
  ```
- **Exception Handling**:
  ```python
  try:
      x = 1 / 0
  except ZeroDivisionError:
      print("Cannot divide by zero!")
  ```

### **Ch 6. Computing**
- **Basic Arithmetic**:
  ```python
  a = 10 + 5
  b = 10 - 5
  c = 10 * 5
  d = 10 / 5
  ```
- **Exponentiation**:
  ```python
  e = 2 ** 3  # 8
  ```

### **Ch 7. Comparisons**
- **Equality/Inequality**:
  ```python
  x = 5
  print(x == 5)  # True
  print(x != 5)  # False
  ```
- **Relational Operators**:
  ```python
  print(x > 3)  # True
  print(x < 10)  # True
  ```

### **Ch 8. Loops**
- **`for` Loop**:
  ```python
  for i in range(5):
      print(i)
  ```
- **`while` Loop**:
  ```python
  count = 0
  while count < 5:
      print(count)
      count += 1
  ```

### **Ch 9. Lists**
- **List Creation and Access**:
  ```python
  fruits = ["apple", "banana", "cherry"]
  print(fruits[0])  # Outputs "apple"
  ```
- **List Methods**:
  ```python
  fruits.append("date")
  fruits.remove("banana")
  print(fruits)  # Outputs ['apple', 'cherry', 'date']
  ```

### **Ch 10. Dictionaries**
- **Creating a Dictionary**:
  ```python
  person = {"name": "Alice", "age": 25}
  print(person["name"])  # Outputs "Alice"
  ```
- **Adding and Removing**:
  ```python
  person["job"] = "Engineer"
  del person["age"]
  print(person)  # Outputs {'name': 'Alice', 'job': 'Engineer'}
  ```

### **Ch 11. Sets**
- **Set Creation**:
  ```python
  fruits = {"apple", "banana", "cherry"}
  print(fruits)  # Outputs {'apple', 'banana', 'cherry'}
  ```
- **Set Operations**:
  ```python
  fruits.add("date")
  fruits.remove("banana")
  print(fruits)  # Outputs {'apple', 'cherry', 'date'}
  ```

### **Ch 12. Errors**
- **Common Exceptions**:
  - `ZeroDivisionError`: Raised when dividing by zero.
  - `IndexError`: Raised when accessing an invalid list index.
  ```python
  try:
      lst = [1, 2, 3]
      print(lst[5])
  except IndexError:
      print("Index out of range!")
  ```
- **Raising Exceptions**:
  ```python
  def check_age(age):
      if age < 18:
          raise ValueError("Age must be 18 or above")
  ```
