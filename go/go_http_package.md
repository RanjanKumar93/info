The `http` package in Go is part of the standard library and provides essential tools to create web servers, handle HTTP requests and responses, and work with clients and servers.

### 1. **Basic HTTP Server**

A simple web server can be created using the `http.ListenAndServe` function.

```go
package main

import (
	"fmt"
	"net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "Hello, World!")
}

func main() {
	http.HandleFunc("/", handler)
	http.ListenAndServe(":8080", nil)
}
```

- **Explanation**:
  - `http.HandleFunc("/", handler)` maps the root URL ("/") to the `handler` function.
  - `http.ListenAndServe(":8080", nil)` starts a server on port 8080.
  - When you visit `http://localhost:8080/`, it displays "Hello, World!".

### 2. **Routing with `http.ServeMux`**

You can use `ServeMux` to handle different routes.

```go
package main

import (
	"fmt"
	"net/http"
)

func homeHandler(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "Welcome to Home Page!")
}

func aboutHandler(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "About Us")
}

func main() {
	mux := http.NewServeMux()
	mux.HandleFunc("/", homeHandler)
	mux.HandleFunc("/about", aboutHandler)

	http.ListenAndServe(":8080", mux)
}
```

- **Explanation**:
  - `ServeMux` is a multiplexer that allows you to register multiple routes and handle them separately.

### 3. **Handling Query Parameters**

Query parameters are often used to pass data in URLs.

```go
package main

import (
	"fmt"
	"net/http"
)

func queryHandler(w http.ResponseWriter, r *http.Request) {
	query := r.URL.Query()
	name := query.Get("name")
	fmt.Fprintf(w, "Hello, %s!", name)
}

func main() {
	http.HandleFunc("/", queryHandler)
	http.ListenAndServe(":8080", nil)
}
```

- **Explanation**:
  - `r.URL.Query()` parses the query parameters, and `query.Get("name")` retrieves the value of the "name" parameter.
  - Visiting `http://localhost:8080/?name=Go` displays "Hello, Go!".

### 4. **Handling POST Requests**

To handle POST requests, you can read the form data sent by the client.

```go
package main

import (
	"fmt"
	"net/http"
)

func formHandler(w http.ResponseWriter, r *http.Request) {
	if r.Method == http.MethodPost {
		err := r.ParseForm()
		if err != nil {
			http.Error(w, "Error parsing form", http.StatusBadRequest)
			return
		}
		name := r.FormValue("name")
		fmt.Fprintf(w, "Hello, %s!", name)
	} else {
		http.Error(w, "Only POST method is allowed", http.StatusMethodNotAllowed)
	}
}

func main() {
	http.HandleFunc("/", formHandler)
	http.ListenAndServe(":8080", nil)
}
```

- **Explanation**:
  - `r.ParseForm()` parses form data sent in a POST request.
  - `r.FormValue("name")` retrieves the form field's value.
  - Only the POST method is allowed, and a 405 status is returned for other methods.

### 5. **Serving Static Files**

You can serve static files such as images, CSS, or JavaScript files using `http.FileServer`.

```go
package main

import (
	"net/http"
)

func main() {
	fs := http.FileServer(http.Dir("./static"))
	http.Handle("/static/", http.StripPrefix("/static/", fs))

	http.ListenAndServe(":8080", nil)
}
```

- **Explanation**:
  - `http.Dir("./static")` points to the directory containing your static files.
  - `http.StripPrefix("/static/", fs)` ensures that the `/static/` prefix is removed from the URL before searching for files.

### 6. **Middleware**

Middleware allows you to process requests before they reach your handler functions.

```go
package main

import (
	"fmt"
	"net/http"
	"time"
)

func loggingMiddleware(next http.Handler) http.Handler {
	return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
		start := time.Now()
		next.ServeHTTP(w, r)
		fmt.Printf("Request processed in %s\n", time.Since(start))
	})
}

func helloHandler(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "Hello, World!")
}

func main() {
	mux := http.NewServeMux()
	mux.HandleFunc("/", helloHandler)

	// Apply middleware
	http.ListenAndServe(":8080", loggingMiddleware(mux))
}
```

- **Explanation**:
  - `loggingMiddleware` measures the time taken to process a request.
  - Middleware wraps the main handler to apply additional logic before and after request handling.

### 7. **Custom HTTP Server**

You can customize various settings of the HTTP server.

```go
package main

import (
	"fmt"
	"net/http"
	"time"
)

func helloHandler(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "Hello, World!")
}

func main() {
	server := &http.Server{
		Addr:         ":8080",
		Handler:      http.HandlerFunc(helloHandler),
		ReadTimeout:  10 * time.Second,
		WriteTimeout: 10 * time.Second,
	}

	server.ListenAndServe()
}
```

- **Explanation**:
  - `ReadTimeout` and `WriteTimeout` specify how long the server will wait for reading and writing.
  - You can also configure other settings like `IdleTimeout`, `TLSConfig`, etc.

### 8. **HTTP Clients**

The `http` package also provides functionality for making HTTP requests to other servers.

```go
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
)

func main() {
	resp, err := http.Get("https://jsonplaceholder.typicode.com/posts/1")
	if err != nil {
		panic(err)
	}
	defer resp.Body.Close()

	body, err := ioutil.ReadAll(resp.Body)
	if err != nil {
		panic(err)
	}

	fmt.Println(string(body))
}
```

- **Explanation**:
  - `http.Get` sends a GET request to the specified URL.
  - `ioutil.ReadAll` reads the response body, and `defer resp.Body.Close()` ensures the body is closed after reading.

### 9. **Advanced: Handling JSON Data**

You often work with JSON data in modern web applications.

```go
package main

import (
	"encoding/json"
	"net/http"
)

type Response struct {
	Message string `json:"message"`
}

func jsonHandler(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "application/json")
	response := Response{Message: "Hello, JSON!"}
	json.NewEncoder(w).Encode(response)
}

func main() {
	http.HandleFunc("/", jsonHandler)
	http.ListenAndServe(":8080", nil)
}
```

- **Explanation**:
  - The `Response` struct is encoded as JSON using `json.NewEncoder`.
  - The `Content-Type` header is set to `application/json`.

### 10. **Advanced: HTTP/2 Support**

Go’s `http` package natively supports HTTP/2 if the server is running with TLS.

```go
package main

import (
	"net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
	w.Write([]byte("Hello, HTTP/2!"))
}

func main() {
	http.HandleFunc("/", handler)
	http.ListenAndServeTLS(":443", "cert.pem", "key.pem", nil)
}
```

- **Explanation**:
  - HTTP/2 is automatically used when `ListenAndServeTLS` is used.
  - You need to provide a TLS certificate (`cert.pem`) and a private key (`key.pem`).

### 11. **Testing HTTP Handlers**

Testing is a critical part of development. Here's how you can test HTTP handlers.

```go
package main

import (
	"net/http"
	"net/http/httptest"
	"testing"
)

func TestHelloHandler(t *testing.T) {
	req, err := http.NewRequest("GET", "/", nil)
	if err != nil {
		t.Fatal(err)
	}

	rr := httptest.NewRecorder()
	handler := http.HandlerFunc(helloHandler)
	handler.ServeHTTP(rr, req)

	if status := rr.Code; status != http.StatusOK {
		t.Errorf("handler returned wrong status code: got %v want %v", status, http.StatusOK)
	}

	expected := "Hello, World!"
	if rr.Body.String() != expected {
		t.Errorf("handler returned unexpected body: got %v want %v", rr.Body.String(), expected)
	}
}
```

- **Explanation**:
  - `httptest.NewRecorder()` simulates an HTTP response writer for testing.
  - `http.NewRequest` creates a new HTTP request.
  - You can check the response status and body to verify correctness.

---

This should give you a solid foundation in the `http` package. We covered everything from basic routing to JSON handling, HTTP clients, middleware, testing, and even HTTP/2 support.
