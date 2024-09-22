### **Object-Oriented Programming (OOP)**

#### **Ch 1. Classes**
A **class** is a blueprint for creating objects. Objects are instances of classes that contain attributes (data) and methods (functions).

**Example**:
```python
class Car:
    def __init__(self, brand, model, year):
        self.brand = brand  # Attribute
        self.model = model  # Attribute
        self.year = year    # Attribute

    def start_engine(self):  # Method
        print(f"The engine of {self.brand} {self.model} is started.")

# Creating an object of the class
my_car = Car("Toyota", "Corolla", 2020)

# Accessing attributes and calling a method
print(my_car.brand)  # Output: Toyota
my_car.start_engine()  # Output: The engine of Toyota Corolla is started.
```

#### **Ch 2. Encapsulation**
**Encapsulation** is the concept of restricting access to certain details of an object, exposing only what is necessary. This is typically done using access modifiers like `private`, `protected`, and `public`. In Python, we use `_` or `__` to indicate private or protected attributes.

**Example**:
```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  # Private attribute

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount

    def get_balance(self):
        return self.__balance

# Creating an object and accessing balance
account = BankAccount(1000)
account.deposit(500)
print(account.get_balance())  # Output: 1500
# print(account.__balance)  # This will raise an AttributeError due to private access
```

#### **Ch 3. Abstraction**
**Abstraction** means hiding the implementation details and showing only the functionality to the user. It is often achieved through abstract classes or interfaces.

**Example**:
```python
from abc import ABC, abstractmethod

class Shape(ABC):  # Abstract base class
    @abstractmethod
    def area(self):
        pass

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14 * (self.radius ** 2)

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

# Creating objects of concrete classes
circle = Circle(5)
rectangle = Rectangle(4, 6)

print(circle.area())  # Output: 78.5
print(rectangle.area())  # Output: 24
```

#### **Ch 4. Inheritance**
**Inheritance** is a mechanism where one class (child class) inherits attributes and methods from another class (parent class). It allows code reuse and the creation of hierarchical relationships.

**Example**:
```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        print(f"{self.name} makes a sound.")

class Dog(Animal):  # Dog class inherits from Animal
    def speak(self):
        print(f"{self.name} barks.")

# Creating an object of the child class
dog = Dog("Buddy")
dog.speak()  # Output: Buddy barks
```

#### **Ch 5. Polymorphism**
**Polymorphism** means "many forms" and allows objects of different classes to be treated as objects of a common base class. It provides flexibility by allowing different classes to implement the same method.

**Example**:
```python
class Cat:
    def speak(self):
        print("Meow")

class Dog:
    def speak(self):
        print("Bark")

# Using polymorphism
def animal_sound(animal):
    animal.speak()

cat = Cat()
dog = Dog()

animal_sound(cat)  # Output: Meow
animal_sound(dog)  # Output: Bark
```

### **Summary**
1. **Classes**: Blueprints for creating objects.
2. **Encapsulation**: Hiding internal state and requiring all interaction through methods.
3. **Abstraction**: Hiding complex implementation details and exposing only the essentials.
4. **Inheritance**: Reusing code by inheriting properties and behaviors from a parent class.
5. **Polymorphism**: Allowing objects to be treated as instances of their parent class and enabling method overriding.

These principles form the core of object-oriented programming, making code more modular, reusable, and organized.
