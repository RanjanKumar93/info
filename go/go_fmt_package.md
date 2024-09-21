The `fmt` package in Go provides functions for formatted I/O, like printing to the console, scanning input, and formatting strings. It's a core package widely used in Go applications.

### Key Functions in `fmt`

- **Output (Printing):**
  - `Print`: Basic printing.
  - `Printf`: Formatted printing.
  - `Println`: Prints with a newline.
- **Input (Scanning):**

  - `Scan`: Reads from standard input.
  - `Scanf`: Formatted reading.
  - `Scanln`: Reads input and expects a newline at the end.

- **Formatting:**
  - `Sprintf`: Formats a string and returns it.
  - `Fprintf`: Prints formatted output to a specific writer (like a file).

Now, let's go through each of these functions in detail with code examples.

### 1. **Basic Printing: `Print`, `Println`, `Printf`**

#### **`fmt.Print`**

This function prints the arguments as is, without adding spaces or newlines.

```go
package main

import (
    "fmt"
)

func main() {
    fmt.Print("Hello")
    fmt.Print("Go!")
}
```

**Output:**

```
HelloGo!
```

#### **`fmt.Println`**

This prints each argument separated by a space and adds a newline at the end.

```go
package main

import (
    "fmt"
)

func main() {
    fmt.Println("Hello")
    fmt.Println("Go!")
}
```

**Output:**

```
Hello
Go!
```

#### **`fmt.Printf`**

This function is used for formatted output. You can include format specifiers in the string (e.g., `%d` for integers, `%s` for strings).

```go
package main

import (
    "fmt"
)

func main() {
    name := "Ranjan"
    age := 25
    fmt.Printf("My name is %s, and I am %d years old.\n", name, age)
}
```

**Output:**

```
My name is Ranjan, and I am 25 years old.
```

**Common Format Specifiers:**

- `%s`: String
- `%d`: Integer
- `%f`: Floating-point number
- `%v`: Default format for any value
- `%T`: Type of the value
- `%t`: Boolean
- `%p`: Pointer address

### 2. **Advanced Formatting**

#### **Width and Precision:**

You can control the width and precision of numbers and strings with `Printf`.

```go
package main

import (
    "fmt"
)

func main() {
    // Floating-point number with 2 decimal places
    fmt.Printf("Pi is %.2f\n", 3.14159)

    // String with minimum width of 10 characters, right-aligned
    fmt.Printf("'%10s'\n", "Go")

    // String with minimum width of 10 characters, left-aligned
    fmt.Printf("'%-10s'\n", "Go")
}
```

**Output:**

```
Pi is 3.14
'        Go'
'Go        '
```

#### **Verbs for Data Types:**

`fmt.Printf` supports various verbs (placeholders) to format data types properly.

```go
package main

import (
    "fmt"
)

func main() {
    x := 123
    b := true
    p := &x

    fmt.Printf("Integer: %d\n", x)
    fmt.Printf("Boolean: %t\n", b)
    fmt.Printf("Pointer: %p\n", p)
}
```

**Output:**

```
Integer: 123
Boolean: true
Pointer: 0xc0000b0010
```

### 3. **Formatting with `Sprintf`**

`fmt.Sprintf` works like `Printf` but returns the formatted string instead of printing it to the console.

```go
package main

import (
    "fmt"
)

func main() {
    name := "Ranjan"
    age := 25
    message := fmt.Sprintf("My name is %s, and I am %d years old.", name, age)
    fmt.Println(message)
}
```

**Output:**

```
My name is Ranjan, and I am 25 years old.
```

### 4. **Printing to Files or Buffers: `Fprintf`**

You can direct output to files or buffers using `Fprintf`. Here’s an example of writing to a file.

```go
package main

import (
    "fmt"
    "os"
)

func main() {
    file, err := os.Create("output.txt")
    if err != nil {
        fmt.Println("Error creating file:", err)
        return
    }
    defer file.Close()

    fmt.Fprintf(file, "Hello, %s!", "file")
}
```

This creates a file named `output.txt` with the content:

```
Hello, file!
```

### 5. **Reading Input: `Scan`, `Scanf`, `Scanln`**

#### **`fmt.Scan`**

This function reads input from the console. It stops scanning when a space is encountered.

```go
package main

import (
    "fmt"
)

func main() {
    var name string
    fmt.Print("Enter your name: ")
    fmt.Scan(&name)
    fmt.Println("Hello,", name)
}
```

**Input/Output:**

```
Enter your name: Ranjan
Hello, Ranjan
```

#### **`fmt.Scanln`**

Similar to `Scan`, but it stops scanning at a newline. Each argument is separated by whitespace.

```go
package main

import (
    "fmt"
)

func main() {
    var name string
    var age int
    fmt.Print("Enter your name and age: ")
    fmt.Scanln(&name, &age)
    fmt.Printf("Hello, %s. You are %d years old.\n", name, age)
}
```

**Input/Output:**

```
Enter your name and age: Ranjan 25
Hello, Ranjan. You are 25 years old.
```

#### **`fmt.Scanf`**

`Scanf` works similarly to `Printf`, but for input. You provide a format string to control how the input is parsed.

```go
package main

import (
    "fmt"
)

func main() {
    var name string
    var age int
    fmt.Print("Enter your name and age: ")
    fmt.Scanf("%s %d", &name, &age)
    fmt.Printf("Hello, %s. You are %d years old.\n", name, age)
}
```

**Input/Output:**

```
Enter your name and age: Ranjan 25
Hello, Ranjan. You are 25 years old.
```

### 6. **Error Handling with `fmt`**

The `fmt` package supports error handling via the `Errorf` function. It formats the error message and returns an `error` type.

```go
package main

import (
    "errors"
    "fmt"
)

func validateAge(age int) error {
    if age < 18 {
        return fmt.Errorf("age %d is too young", age)
    }
    return nil
}

func main() {
    err := validateAge(16)
    if err != nil {
        fmt.Println("Error:", err)
    }
}
```

**Output:**

```
Error: age 16 is too young
```

### 7. **Printing Structs and Complex Types**

When printing structs or slices, Go provides default formatting options:

```go
package main

import (
    "fmt"
)

type Person struct {
    Name string
    Age  int
}

func main() {
    p := Person{Name: "Ranjan", Age: 25}
    fmt.Printf("%v\n", p)   // Default format
    fmt.Printf("%+v\n", p)  // Shows field names
    fmt.Printf("%#v\n", p)  // Go syntax representation
}
```

**Output:**

```
{Ranjan 25}
{Name:Ranjan Age:25}
main.Person{Name:"Ranjan", Age:25}
```

### Summary of Key `fmt` Functions:

1. **Basic Output:**

   - `Print()`: Prints without a newline.
   - `Println()`: Prints with a newline.
   - `Printf()`: Prints formatted output.

2. **Advanced Formatting:**

   - `%d`, `%s`, `%f`, `%v`, `%+v`, `%#v`: Format specifiers.

3. **Input:**

   - `Scan()`: Reads space-separated input.
   - `Scanln()`: Reads input, stopping at newline.
   - `Scanf()`: Reads formatted input.

4. **File/Buffer Writing:**

   - `Fprintf()`: Prints formatted output to files or buffers.

5. **Error Handling:**
   - `Errorf()`: Formats and returns an error.

The `fmt` package is powerful and highly flexible for both input and output operations. It helps in formatting and managing strings, struct formatting, reading input, and even creating custom error messages.
