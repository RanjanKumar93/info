In Python, errors and exceptions indicate that something went wrong during the execution of a program. These can be categorized into two main types: **Syntax Errors** and **Exceptions**.

### 1. **Syntax Errors**

Syntax errors occur when Python's parser encounters code that is incorrect in terms of the language syntax. These are detected before the code is executed.

#### Example:

```python
# SyntaxError: Missing colon (expected ":" after "if" statement)
if True
    print("This will cause a syntax error")
```

- **Common Causes**: Missing colons, incorrect indentation, unclosed parentheses, etc.

### 2. **Exceptions**

Exceptions occur during runtime when the code is syntactically correct but an error arises during execution. Python provides several built-in exceptions, and you can also define your own custom exceptions.

#### Built-in Exceptions in Python:

1. **TypeError**

   - Raised when an operation or function is applied to an object of inappropriate type.
   - Example:

   ```python
   result = '2' + 2  # TypeError: Can't add a string and an integer
   ```

2. **ValueError**

   - Raised when a function receives an argument of the right type but an inappropriate value.
   - Example:

   ```python
   number = int('abc')  # ValueError: Invalid literal for int() with base 10
   ```

3. **NameError**

   - Raised when a local or global name is not found.
   - Example:

   ```python
   print(x)  # NameError: name 'x' is not defined
   ```

4. **IndexError**

   - Raised when trying to access an element from a list, tuple, or string using an index that is out of range.
   - Example:

   ```python
   my_list = [1, 2, 3]
   print(my_list[5])  # IndexError: List index out of range
   ```

5. **KeyError**

   - Raised when trying to access a dictionary with a key that doesn't exist.
   - Example:

   ```python
   my_dict = {'name': 'Alice'}
   print(my_dict['age'])  # KeyError: 'age'
   ```

6. **AttributeError**

   - Raised when an invalid attribute is referenced on an object.
   - Example:

   ```python
   my_list = [1, 2, 3]
   my_list.append()  # AttributeError: append() missing 1 required positional argument
   ```

7. **ZeroDivisionError**

   - Raised when trying to divide a number by zero.
   - Example:

   ```python
   result = 10 / 0  # ZeroDivisionError: Division by zero
   ```

8. **FileNotFoundError**

   - Raised when trying to open a file that doesn't exist.
   - Example:

   ```python
   with open('non_existent_file.txt', 'r') as file:
       content = file.read()  # FileNotFoundError: No such file or directory
   ```

9. **IOError**

   - Raised when an input/output operation fails (like opening a file).
   - Example:

   ```python
   with open('/restricted_file.txt', 'r') as file:
       content = file.read()  # IOError: Permission denied
   ```

10. **ImportError**

    - Raised when an import statement fails to find the module definition or when a `from ... import` fails to find a name that is to be imported.
    - Example:

    ```python
    import non_existent_module  # ImportError: No module named 'non_existent_module'
    ```

11. **IndentationError**

    - Raised when the indentation is not correct in the code.
    - Example:

    ```python
    def my_function():
    print("Hello")  # IndentationError: expected an indented block
    ```

12. **MemoryError**

    - Raised when an operation runs out of memory.
    - Example:

    ```python
    huge_list = [1] * (10**10)  # MemoryError: Ran out of memory
    ```

13. **StopIteration**

    - Raised to signal the end of an iterator's sequence.
    - Example:

    ```python
    my_iter = iter([1, 2, 3])
    print(next(my_iter))  # Outputs 1
    print(next(my_iter))  # Outputs 2
    print(next(my_iter))  # Outputs 3
    print(next(my_iter))  # StopIteration
    ```

14. **OverflowError**

    - Raised when a calculation exceeds the maximum limit for a numeric type.
    - Example:

    ```python
    import math
    print(math.exp(1000))  # OverflowError: math range error
    ```

15. **RecursionError**

    - Raised when the maximum recursion depth is exceeded.
    - Example:

    ```python
    def recursive_function():
        recursive_function()

    recursive_function()  # RecursionError: maximum recursion depth exceeded
    ```

16. **AssertionError**

    - Raised when an `assert` statement fails.
    - Example:

    ```python
    x = 5
    assert x == 10, "x should be 10"  # AssertionError: x should be 10
    ```

17. **UnicodeError**

    - Raised when a Unicode-related encoding or decoding error occurs.
    - Example:

    ```python
    text = b'\x80abc'
    text.decode('utf-8')  # UnicodeDecodeError: 'utf-8' codec can't decode byte 0x80
    ```

18. **NotImplementedError**

    - Raised when an abstract method that is not implemented in a subclass is called.
    - Example:

    ```python
    class BaseClass:
        def do_something(self):
            raise NotImplementedError("Subclass must implement this method")

    class SubClass(BaseClass):
        pass

    obj = SubClass()
    obj.do_something()  # NotImplementedError: Subclass must implement this method
    ```

### Handling Exceptions:

You can handle exceptions using `try`, `except`, and optionally `finally` blocks. Here's an example:

```python
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print(f"Error occurred: {e}")
finally:
    print("This will always execute")
```

### Custom Exceptions:

You can create your own exceptions by subclassing the built-in `Exception` class.

```python
class CustomError(Exception):
    def __init__(self, message):
        self.message = message

try:
    raise CustomError("This is a custom error")
except CustomError as e:
    print(e.message)
```

By understanding and handling these exceptions, you can write more robust and error-tolerant Python programs.
