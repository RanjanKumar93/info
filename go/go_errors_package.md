The `errors` package in Go provides utilities for creating and handling errors. It is a key part of Go’s error-handling mechanism, which relies on returning error values from functions instead of exceptions (like in other languages).

### Key Concepts of the `errors` Package:

1. **Creating Errors**: Generate new error values.
2. **Wrapping Errors**: Add context to an error using the `fmt.Errorf` or `errors` package.
3. **Unwrapping Errors**: Extract wrapped errors.
4. **Comparing Errors**: Check if two errors are equivalent.
5. **Custom Error Types**: Create custom error types by implementing the `error` interface.

---

### 1. **Creating Errors**

You can create a new error using the `errors.New` function, which returns an error with a given message.

```go
package main

import (
    "errors"
    "fmt"
)

func main() {
    err := errors.New("something went wrong")
    if err != nil {
        fmt.Println("Error:", err) // Output: Error: something went wrong
    }
}
```

### 2. **Wrapping Errors**

#### **`fmt.Errorf` with `%w`**: Wraps an error with additional context, preserving the original error. The `%w` verb is used to wrap an error.

```go
package main

import (
    "errors"
    "fmt"
)

func openFile() error {
    return errors.New("file not found")
}

func main() {
    err := openFile()
    if err != nil {
        wrappedErr := fmt.Errorf("failed to open file: %w", err)
        fmt.Println(wrappedErr) // Output: failed to open file: file not found
    }
}
```

#### **`errors.Unwrap`**: Unwraps a wrapped error to retrieve the original one.

```go
package main

import (
    "errors"
    "fmt"
)

func openFile() error {
    return errors.New("file not found")
}

func main() {
    err := openFile()
    wrappedErr := fmt.Errorf("failed to open file: %w", err)
    unwrappedErr := errors.Unwrap(wrappedErr)
    fmt.Println("Original Error:", unwrappedErr) // Output: Original Error: file not found
}
```

### 3. **Checking for Specific Errors**

#### **`errors.Is`**: Used to compare an error against a target error (including wrapped errors).

```go
package main

import (
    "errors"
    "fmt"
)

var ErrFileNotFound = errors.New("file not found")

func openFile() error {
    return fmt.Errorf("could not read config: %w", ErrFileNotFound)
}

func main() {
    err := openFile()
    if errors.Is(err, ErrFileNotFound) {
        fmt.Println("Error: File not found!") // Output: Error: File not found!
    }
}
```

### 4. **Custom Error Types**

You can define custom error types by implementing the `error` interface, which consists of a single `Error()` method.

```go
package main

import (
    "fmt"
)

// Custom error type
type MyError struct {
    Code    int
    Message string
}

func (e *MyError) Error() string {
    return fmt.Sprintf("Error %d: %s", e.Code, e.Message)
}

func riskyOperation() error {
    return &MyError{Code: 123, Message: "operation failed"}
}

func main() {
    err := riskyOperation()
    if err != nil {
        fmt.Println(err) // Output: Error 123: operation failed
    }
}
```

### 5. **Checking Custom Error Types**

#### **`errors.As`**: Used to check if an error can be assigned to a particular custom error type.

```go
package main

import (
    "errors"
    "fmt"
)

// Custom error type
type MyError struct {
    Code    int
    Message string
}

func (e *MyError) Error() string {
    return fmt.Sprintf("Error %d: %s", e.Code, e.Message)
}

func riskyOperation() error {
    return &MyError{Code: 123, Message: "operation failed"}
}

func main() {
    err := riskyOperation()
    var myErr *MyError
    if errors.As(err, &myErr) {
        fmt.Println("Custom error code:", myErr.Code) // Output: Custom error code: 123
    }
}
```

### 6. **Combining Errors**

#### **`errors.Join`**: Combines multiple errors into one.

```go
package main

import (
    "errors"
    "fmt"
)

func main() {
    err1 := errors.New("failed to open file")
    err2 := errors.New("network issue")
    combinedErr := errors.Join(err1, err2)
    fmt.Println(combinedErr) // Output: failed to open file; network issue
}
```

### Summary of Common `errors` Functions:

1. **`errors.New`**: Create a new error.
2. **`errors.Unwrap`**: Unwraps the wrapped error.
3. **`errors.Is`**: Checks if an error matches a specific error.
4. **`errors.As`**: Checks if an error can be assigned to a custom error type.
5. **`errors.Join`**: Combines multiple errors.

The `errors` package helps manage error handling in Go, giving you control over creating, wrapping, and inspecting errors efficiently.
