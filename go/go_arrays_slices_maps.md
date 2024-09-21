In Go, arrays, slices, and maps are foundational data structures, each with distinct characteristics and use cases.

### 1. **Arrays** in Go

An **array** is a fixed-length sequence of elements, where all elements are of the same type. Once declared, the size of the array cannot be changed.

#### Declaring Arrays

```go
package main

import "fmt"

func main() {
    var arr [5]int  // Declares an array of 5 integers, initialized to zero
    fmt.Println(arr) // Output: [0 0 0 0 0]

    arr[0] = 10     // Assign value to the first element
    fmt.Println(arr) // Output: [10 0 0 0 0]

    // Declare and initialize an array
    fruits := [3]string{"Apple", "Banana", "Cherry"}
    fmt.Println(fruits) // Output: [Apple Banana Cherry]
}
```

#### Key Points:

- Arrays are **fixed in size**.
- Access elements using zero-based indexing.
- If you try to access an index out of range, you'll get a runtime error.

#### Looping Over Arrays

```go
func main() {
    numbers := [5]int{10, 20, 30, 40, 50}

    for i, v := range numbers {
        fmt.Printf("Index: %d, Value: %d\n", i, v)
    }
}
```

---

### 2. **Slices** in Go

A **slice** is a more flexible, powerful version of an array. Unlike arrays, slices are dynamic and can grow or shrink in size. Slices are backed by arrays, but their size can be adjusted.

#### Declaring and Initializing Slices

```go
func main() {
    // Declare a slice using make()
    nums := make([]int, 3) // Create a slice of 3 integers
    fmt.Println(nums)      // Output: [0 0 0]

    // Declare and initialize a slice
    fruits := []string{"Apple", "Banana", "Cherry"}
    fmt.Println(fruits) // Output: [Apple Banana Cherry]
}
```

#### Key Points:

- Slices are **dynamic**.
- **Capacity**: Every slice has a length (number of elements it contains) and a capacity (number of elements it can hold without allocating more memory).
- Slices are more commonly used than arrays due to their flexibility.

#### Slicing an Array

```go
func main() {
    arr := [5]int{1, 2, 3, 4, 5}
    slice := arr[1:4] // Slice from index 1 to 3 (4 is excluded)
    fmt.Println(slice) // Output: [2 3 4]
}
```

#### Slicing a Slice

```go
func main() {
    fruits := []string{"Apple", "Banana", "Cherry", "Mango", "Orange"}
    subset := fruits[1:4] // Slice from index 1 to 3
    fmt.Println(subset)    // Output: [Banana Cherry Mango]
}
```

#### Appending to a Slice

The `append()` function adds elements to the end of a slice. If the slice doesn’t have enough capacity, Go allocates a new array.

```go
func main() {
    nums := []int{1, 2, 3}
    nums = append(nums, 4, 5) // Appending elements to the slice
    fmt.Println(nums)         // Output: [1 2 3 4 5]
}
```

#### Slice Capacity and Length

```go
func main() {
    nums := make([]int, 3, 5) // Slice of length 3, capacity 5
    fmt.Println(len(nums))    // Output: 3
    fmt.Println(cap(nums))    // Output: 5
}
```

#### Looping Over Slices

```go
func main() {
    fruits := []string{"Apple", "Banana", "Cherry"}

    for i, v := range fruits {
        fmt.Printf("Index: %d, Value: %s\n", i, v)
    }
}
```

---

### 3. **Maps** in Go

A **map** is an unordered collection of key-value pairs. Maps are like dictionaries in other languages. They provide efficient lookups, updates, and deletions.

#### Declaring and Initializing Maps

```go
func main() {
    // Declare a map using make()
    ageMap := make(map[string]int)

    // Initialize a map with values
    ageMap = map[string]int{
        "Alice": 25,
        "Bob":   30,
        "Cathy": 22,
    }

    fmt.Println(ageMap) // Output: map[Alice:25 Bob:30 Cathy:22]
}
```

#### Accessing and Modifying Maps

```go
func main() {
    ageMap := map[string]int{
        "Alice": 25,
        "Bob":   30,
    }

    // Access value by key
    fmt.Println(ageMap["Alice"]) // Output: 25

    // Modify value
    ageMap["Alice"] = 26
    fmt.Println(ageMap) // Output: map[Alice:26 Bob:30]

    // Add new key-value pair
    ageMap["Cathy"] = 22
    fmt.Println(ageMap) // Output: map[Alice:26 Bob:30 Cathy:22]
}
```

#### Key Points:

- Maps are **unordered**, meaning the order of elements when iterating is not guaranteed.
- Accessing a non-existing key returns the zero value for the value type.

#### Checking If a Key Exists

```go
func main() {
    ageMap := map[string]int{
        "Alice": 25,
        "Bob":   30,
    }

    age, exists := ageMap["Alice"]
    if exists {
        fmt.Println("Alice's age:", age) // Output: Alice's age: 25
    } else {
        fmt.Println("Alice not found")
    }
}
```

#### Deleting an Element from a Map

```go
func main() {
    ageMap := map[string]int{
        "Alice": 25,
        "Bob":   30,
    }

    delete(ageMap, "Alice") // Remove Alice from the map
    fmt.Println(ageMap)     // Output: map[Bob:30]
}
```

#### Looping Over a Map

```go
func main() {
    ageMap := map[string]int{
        "Alice": 25,
        "Bob":   30,
        "Cathy": 22,
    }

    for key, value := range ageMap {
        fmt.Printf("Key: %s, Value: %d\n", key, value)
    }
}
```

---

### Key Differences

1. **Arrays**:
   - Fixed size.
   - Not commonly used in Go due to the lack of flexibility.
2. **Slices**:

   - Flexible, resizable.
   - Most commonly used for handling collections of elements.
   - Backed by arrays but dynamic in size.

3. **Maps**:
   - Unordered collection of key-value pairs.
   - Great for fast lookups, deletions, and updates.

These are the basics of arrays, slices, and maps in Go.
