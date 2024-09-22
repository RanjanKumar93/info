Let's go through these concepts one by one: `sorted()`, `len()`, and floor division (`//`) in Python.

### 1. `sorted()`

The `sorted()` function returns a sorted list of the specified iterable (list, tuple, string, etc.). The original iterable remains unchanged.

#### Syntax:

```python
sorted(iterable, key=None, reverse=False)
```

- `iterable`: The sequence you want to sort.
- `key`: A function to customize the sort order. Default is `None`.
- `reverse`: If `True`, the iterable is sorted in descending order.

#### Example:

```python
# Sorting a list of numbers
numbers = [3, 1, 4, 2]
sorted_numbers = sorted(numbers)
print(sorted_numbers)  # Output: [1, 2, 3, 4]

# Sorting in descending order
sorted_numbers_desc = sorted(numbers, reverse=True)
print(sorted_numbers_desc)  # Output: [4, 3, 2, 1]

# Sorting a list of strings by length
words = ["apple", "banana", "cherry"]
sorted_words = sorted(words, key=len)
print(sorted_words)  # Output: ['apple', 'cherry', 'banana']
```

### 2. `len()`

The `len()` function returns the number of items in an object (e.g., list, tuple, string).

#### Syntax:

```python
len(s)
```

- `s`: The object you want to get the length of.

#### Example:

```python
# Length of a list
fruits = ["apple", "banana", "cherry"]
print(len(fruits))  # Output: 3

# Length of a string
text = "Hello, world!"
print(len(text))  # Output: 13
```

### 3. Floor Division (`//`)

The floor division operator (`//`) divides two numbers and rounds the result down to the nearest integer.

#### Syntax:

```python
result = a // b
```

- `a`: The dividend.
- `b`: The divisor.

#### Example:

```python
# Floor division of integers
result = 7 // 2
print(result)  # Output: 3

# Floor division of floats
result = 7.5 // 2
print(result)  # Output: 3.0

# Negative floor division
result = -7 // 2
print(result)  # Output: -4
```

### Summary:

- `sorted()`: Sorts an iterable and returns a new sorted list.
- `len()`: Returns the number of items in an object.
- `//`: Performs division and returns the floor of the result (the largest integer less than or equal to the division).
