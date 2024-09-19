The `strconv` package in Go provides functions for converting strings to basic data types and vice versa. It is essential for parsing or formatting numeric values, booleans, and other types from/to strings.

### Key Features of `strconv`:

1. **String to Number Conversion**
   - Parse numbers (integers and floats) from strings.
2. **Number to String Conversion**
   - Convert numbers (integers and floats) to strings.
3. **Boolean Parsing**
   - Parse boolean values from strings.
4. **Quoted String Handling**
   - Parse and format quoted strings.
5. **Miscellaneous Conversions**
   - Convert between byte slices and strings, etc.

---

### 1. **String to Integer Conversion**

#### **`strconv.Atoi`**: Converts a string to an integer.

```go
package main

import (
    "fmt"
    "strconv"
)

func main() {
    str := "123"
    num, err := strconv.Atoi(str)
    if err != nil {
        fmt.Println("Error:", err)
    } else {
        fmt.Println("Integer:", num) // Output: 123
    }
}
```

#### **`strconv.ParseInt`**: Converts a string to an integer with more control over the base and bit size.

```go
package main

import (
    "fmt"
    "strconv"
)

func main() {
    str := "101"
    num, err := strconv.ParseInt(str, 2, 64) // Binary string to integer
    if err != nil {
        fmt.Println("Error:", err)
    } else {
        fmt.Println("Parsed Integer:", num) // Output: 5
    }
}
```

### 2. **Integer to String Conversion**

#### **`strconv.Itoa`**: Converts an integer to a string.

```go
package main

import (
    "fmt"
    "strconv"
)

func main() {
    num := 123
    str := strconv.Itoa(num)
    fmt.Println("String:", str) // Output: "123"
}
```

#### **`strconv.FormatInt`**: Converts an integer to a string in a specified base.

```go
package main

import (
    "fmt"
    "strconv"
)

func main() {
    num := int64(5)
    str := strconv.FormatInt(num, 2) // Convert to binary string
    fmt.Println("Binary String:", str) // Output: "101"
}
```

### 3. **String to Float Conversion**

#### **`strconv.ParseFloat`**: Converts a string to a floating-point number.

```go
package main

import (
    "fmt"
    "strconv"
)

func main() {
    str := "3.14"
    num, err := strconv.ParseFloat(str, 64)
    if err != nil {
        fmt.Println("Error:", err)
    } else {
        fmt.Println("Float:", num) // Output: 3.14
    }
}
```

### 4. **Float to String Conversion**

#### **`strconv.FormatFloat`**: Converts a floating-point number to a string.

```go
package main

import (
    "fmt"
    "strconv"
)

func main() {
    num := 3.14159
    str := strconv.FormatFloat(num, 'f', 2, 64) // 2 decimal places
    fmt.Println("Formatted String:", str) // Output: "3.14"
}
```

### 5. **String to Boolean Conversion**

#### **`strconv.ParseBool`**: Converts a string to a boolean.

```go
package main

import (
    "fmt"
    "strconv"
)

func main() {
    str := "true"
    b, err := strconv.ParseBool(str)
    if err != nil {
        fmt.Println("Error:", err)
    } else {
        fmt.Println("Boolean:", b) // Output: true
    }
}
```

### 6. **Boolean to String Conversion**

#### **`strconv.FormatBool`**: Converts a boolean to a string.

```go
package main

import (
    "fmt"
    "strconv"
)

func main() {
    b := true
    str := strconv.FormatBool(b)
    fmt.Println("String:", str) // Output: "true"
}
```

### 7. **Handling Quoted Strings**

#### **`strconv.Quote`**: Returns a double-quoted string literal, suitable for Go source code.

```go
package main

import (
    "fmt"
    "strconv"
)

func main() {
    str := "hello"
    quotedStr := strconv.Quote(str)
    fmt.Println("Quoted String:", quotedStr) // Output: "\"hello\""
}
```

#### **`strconv.Unquote`**: Removes surrounding quotes from a quoted string.

```go
package main

import (
    "fmt"
    "strconv"
)

func main() {
    quotedStr := "\"hello\""
    str, err := strconv.Unquote(quotedStr)
    if err != nil {
        fmt.Println("Error:", err)
    } else {
        fmt.Println("Unquoted String:", str) // Output: "hello"
    }
}
```

### 8. **Miscellaneous Functions**

#### **`strconv.Itoa` and `strconv.FormatInt`**

These two functions convert integers to strings. While `Itoa` only works for base-10 integers, `FormatInt` allows conversion in any base (like binary, hexadecimal, etc.).

---

### Summary of Common `strconv` Functions:

1. **String to Integer/Float/Bool**:
   - `strconv.Atoi`, `strconv.ParseInt`, `strconv.ParseFloat`, `strconv.ParseBool`
2. **Integer/Float/Bool to String**:
   - `strconv.Itoa`, `strconv.FormatInt`, `strconv.FormatFloat`, `strconv.FormatBool`
3. **Quoted String Handling**:
   - `strconv.Quote`, `strconv.Unquote`
4. **Error Handling**:
   - Most functions return a value and an error, so proper error handling is essential.

The `strconv` package is very useful for converting between Go's basic types and strings, which is a common requirement when parsing input or formatting output.
