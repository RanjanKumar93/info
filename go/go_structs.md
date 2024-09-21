Structs in Go are a fundamental concept for defining custom data types that group related fields together. They are used to create more complex types by combining simple data types, and they allow you to model real-world objects and manage complex data structures in an organized way.

Let's dive into everything about structs, starting from the basics to more advanced concepts with code examples.

### 1. **Defining a Struct**

A struct is a collection of fields. Each field has a name and a type.

```go
package main

import "fmt"

// Defining a struct called `Person`
type Person struct {
    firstName string
    lastName  string
    age       int
}

func main() {
    // Creating an instance of the `Person` struct
    person := Person{
        firstName: "John",
        lastName:  "Doe",
        age:       30,
    }

    fmt.Println(person) // Output: {John Doe 30}
}
```

### 2. **Accessing Struct Fields**

You can access individual fields of a struct using the dot (`.`) notation.

```go
func main() {
    person := Person{
        firstName: "John",
        lastName:  "Doe",
        age:       30,
    }

    fmt.Println("First Name:", person.firstName)
    fmt.Println("Last Name:", person.lastName)
    fmt.Println("Age:", person.age)
}
```

### 3. **Anonymous Structs**

Go also supports creating structs without defining them beforehand.

```go
func main() {
    // Anonymous struct
    person := struct {
        firstName string
        lastName  string
        age       int
    }{
        firstName: "Alice",
        lastName:  "Smith",
        age:       25,
    }

    fmt.Println(person) // Output: {Alice Smith 25}
}
```

### 4. **Struct Methods**

In Go, you can define methods on structs. Methods are functions with a receiver argument, which is typically the struct itself.

```go
// Adding a method to the `Person` struct
func (p Person) fullName() string {
    return p.firstName + " " + p.lastName
}

func main() {
    person := Person{
        firstName: "John",
        lastName:  "Doe",
        age:       30,
    }

    fmt.Println("Full Name:", person.fullName()) // Output: Full Name: John Doe
}
```

### 5. **Pointer Receivers vs Value Receivers**

In Go, methods can have either pointer or value receivers. If you want the method to modify the struct, you should use a pointer receiver (`*`).

- **Value Receiver** (the struct is copied):

```go
func (p Person) birthday() {
    p.age += 1
}

func main() {
    person := Person{firstName: "John", age: 30}
    person.birthday()
    fmt.Println(person.age) // Output: 30 (no change, since value receiver doesn't modify the original)
}
```

- **Pointer Receiver** (the struct is updated):

```go
func (p *Person) birthday() {
    p.age += 1
}

func main() {
    person := Person{firstName: "John", age: 30}
    person.birthday()
    fmt.Println(person.age) // Output: 31 (pointer receiver modifies the original)
}
```

### 6. **Structs and Functions**

You can pass structs as function arguments and return them from functions.

```go
func updateName(p *Person, newName string) {
    p.firstName = newName
}

func main() {
    person := Person{firstName: "John", age: 30}
    updateName(&person, "Michael")
    fmt.Println(person.firstName) // Output: Michael
}
```

### 7. **Embedded Structs (Composition)**

Go doesn't support inheritance, but it uses composition by embedding structs.

```go
type Address struct {
    city  string
    state string
}

type Employee struct {
    Person  // Embedding the `Person` struct
    company string
    Address // Embedding the `Address` struct
}

func main() {
    emp := Employee{
        Person: Person{
            firstName: "Alice",
            lastName:  "Smith",
            age:       28,
        },
        company: "Tech Corp",
        Address: Address{
            city:  "New York",
            state: "NY",
        },
    }

    fmt.Println(emp.firstName) // Output: Alice (field from the embedded Person struct)
    fmt.Println(emp.city)      // Output: New York (field from the embedded Address struct)
}
```

### 8. **Tags in Struct Fields**

Struct fields can have associated tags. Tags are often used for purposes like serialization (e.g., JSON).

```go
type Person struct {
    FirstName string `json:"first_name"`
    LastName  string `json:"last_name"`
    Age       int    `json:"age"`
}

func main() {
    person := Person{FirstName: "John", LastName: "Doe", Age: 30}
    fmt.Println(person)
}
```

This tag information is often used by packages like `encoding/json` to determine how to marshal/unmarshal data.

### 9. **Zero Values in Structs**

When you declare a struct without initializing its fields, Go automatically assigns each field a "zero value":

- `0` for numbers
- `""` for strings
- `false` for booleans

```go
func main() {
    var person Person
    fmt.Println(person) // Output: {  0} (empty string for names, 0 for age)
}
```

### 10. **Comparing Structs**

Structs can be compared using the `==` operator, but only if all the fields are comparable.

```go
func main() {
    p1 := Person{firstName: "John", lastName: "Doe", age: 30}
    p2 := Person{firstName: "John", lastName: "Doe", age: 30}

    fmt.Println(p1 == p2) // Output: true (all fields match)
}
```

### Summary

- **Structs** allow you to group fields and create complex data structures.
- You can access and modify struct fields using the dot (`.`) notation.
- **Methods** can be defined on structs with value or pointer receivers.
- Structs can be passed to functions and returned from functions.
- Go uses **composition** through embedded structs rather than inheritance.
- Struct fields can have **tags** for special metadata (e.g., JSON).

This should cover all the basic to intermediate concepts related to structs in Go.
