# RocketHTTP - https://blog.lowlevelforest.com/

RocketHTTP is a high-performance HTTP client library written in Go and designed to handle up to 1000,000 concurrent requests. It integrates non-blocking operations with Go routines, in-memory caching, HTTP/2 support, and allows Python developers to use the library by loading it as a shared object (`.so`) file.

## Key Features

- **High Concurrency**: RocketHTTP can handle a massive number of concurrent connections thanks to Go routines, making it a perfect fit for applications requiring high scalability.
- **In-Memory Caching**: Caching is built into the library to improve the efficiency of repeated requests with customizable time-to-live (TTL).
- **HTTP/2 Support**: The library allows seamless integration of HTTP/2 for better performance in modern web applications.
- **KeepAlive and Custom Configuration**: Supports configurable KeepAlive settings and allows fine-tuning for idle connections, transport settings, and timeouts.
- **Supports Multiple HTTP Methods**: RocketHTTP provides support for all major HTTP methods including GET, POST, PUT, PATCH, DELETE, HEAD, OPTIONS, CONNECT, TRACE.

## How RocketHTTP Compares to FastAPI

While **FastAPI** is a powerful framework for building APIs and is typically used for server-side development, **RocketHTTP** focuses on being a client-side solution optimized for high concurrency, low-latency requests. Below is a comparison:

| Feature          | RocketHTTP                        | FastAPI                            |
|------------------|-----------------------------------|------------------------------------|
| Use Case         | HTTP client for sending requests  | API server framework               |
| Concurrency      | Built-in Go routines for handling 1000,000 requests | FastAPI uses async capabilities to handle multiple requests |
| In-Memory Cache  | Yes, built-in cache with TTL      | Not available by default           |
| HTTP/2 Support   | Supported                         | Supported, but requires additional configuration |
| Python Support   | Integrated as a shared `.so` file | Fully native for Python developers |
| Speed            | Highly optimized for request handling | Fast, but more focused on API development |

## Comparison of RocketHTTP with FastAPI, Asyncio, Trio, and uvloop

To understand the differences between **RocketHTTP**, **FastAPI**, **Asyncio**, **Trio**, and **uvloop**, we’ll compare their capabilities, use cases, and performance characteristics.

| Feature           | RocketHTTP                            | FastAPI                            | Asyncio                            | Trio                                | uvloop                            |
|-------------------|---------------------------------------|------------------------------------|-----------------------------------|-------------------------------------|-----------------------------------|
| **Type**          | HTTP Client Library                    | Web Framework                       | Asynchronous I/O Framework         | Asynchronous I/O Framework           | High-performance Event Loop        |
| **Use Case**      | High-performance HTTP client           | Building APIs and web applications  | Asynchronous I/O operations        | Asynchronous I/O operations          | Replacement for asyncio’s event loop|
| **Concurrency**   | Handles up to 1000,000 concurrent requests | Uses async/await for concurrency    | Handles concurrency with async/await | Designed for structured concurrency  | Enhances asyncio with better performance |
| **HTTP Support**  | Full support for HTTP methods          | Full support with routing and middleware | Not directly tied to HTTP          | Not directly tied to HTTP            | Not directly tied to HTTP          |
| **In-Memory Cache**| Yes, with TTL support                  | No built-in caching; requires external tools | Not applicable                      | Not applicable                        | Not applicable                      |
| **HTTP/2 Support** | Yes                                    | Yes, with additional configuration  | Supports with additional libraries | Supports with additional libraries    | Not directly applicable            |
| **Python Integration** | Load as a shared object (`.so`)   | Native Python library               | Native Python library              | Native Python library                | Native Python library              |
| **Performance**   | Optimized for high concurrency and low latency | High performance, optimized for APIs | Performance depends on implementation | Structured concurrency can improve performance | Improves performance of asyncio    |
| **Ease of Use**   | Requires CFFI for Python integration   | Easy to use with Python’s async/await | Easy to use with Python’s async/await | Requires learning Trio’s abstractions | Easy to use with asyncio            |
| **Examples**      | HTTP client for making requests        | Building RESTful APIs, web services | Can be used with web frameworks (e.g., aiohttp) | Can be used with web frameworks (e.g., asks) | Enhances asyncio’s event loop       |

### Detailed Comparison

1. **RocketHTTP**
   - **Type**: HTTP client library written in Go, designed for high-performance HTTP request handling.
   - **Use Case**: Ideal for applications needing to make a large number of concurrent HTTP requests efficiently.
   - **Concurrency**: Utilizes Go routines for handling concurrency, optimized for up to 100,000 concurrent requests.
   - **HTTP Support**: Supports all major HTTP methods with in-memory caching and HTTP/2.
   - **Python Integration**: Exposes a shared object (`.so`) file that Python can utilize via CFFI.
   - **Performance**: Optimized for handling a high volume of requests with low latency.

2. **FastAPI**
   - **Type**: Modern web framework for building APIs with Python.
   - **Use Case**: Ideal for building fast and scalable web applications and APIs with automatic documentation support.
   - **Concurrency**: Uses async/await syntax for handling asynchronous requests, leveraging Starlette for async capabilities.
   - **HTTP Support**: Full support for HTTP methods with additional features for routing, validation, and middleware.
   - **Python Integration**: Native Python library, making it straightforward to use within Python projects.
   - **Performance**: High performance due to asynchronous handling and efficient routing.

3. **Asyncio**
   - **Type**: Standard Python library for asynchronous I/O operations.
   - **Use Case**: Provides the core infrastructure for asynchronous programming in Python.
   - **Concurrency**: Uses async/await syntax and event loops to manage concurrency.
   - **HTTP Support**: Not directly related to HTTP; it is a general-purpose asynchronous I/O framework.
   - **Python Integration**: Native Python library, widely used across various asynchronous frameworks and applications.
   - **Performance**: Provides the foundation for asynchronous I/O; performance depends on the specific implementation.

4. **Trio**
   - **Type**: Asynchronous I/O library for Python with a focus on structured concurrency.
   - **Use Case**: Designed for structured concurrency and easier reasoning about concurrency issues.
   - **Concurrency**: Uses structured concurrency principles to manage tasks and resources more effectively.
   - **HTTP Support**: Not directly tied to HTTP; can be used with Trio-based HTTP libraries.
   - **Python Integration**: Native Python library, designed to be user-friendly and reliable.
   - **Performance**: Emphasizes structured concurrency, which can improve reliability and maintainability.

5. **uvloop**
   - **Type**: High-performance event loop for asyncio.
   - **Use Case**: Enhances the performance of asyncio by providing a faster event loop implementation.
   - **Concurrency**: Works with asyncio to provide improved performance for handling concurrency.
   - **HTTP Support**: Not directly related to HTTP; it is used to optimize asyncio’s event loop.
   - **Python Integration**: Native Python library, integrates seamlessly with asyncio applications.
   - **Performance**: Provides significant performance improvements over the default asyncio event loop.

### Conclusion

- **RocketHTTP** is specialized for high-performance HTTP requests and is a good choice if you need to handle a large number of concurrent HTTP connections with caching and HTTP/2 support.
- **FastAPI** is excellent for building modern web APIs and provides a comprehensive suite of features for API development, including asynchronous handling with Python’s async/await syntax.
- **Asyncio** is the core library for asynchronous programming in Python and provides the building blocks for concurrency but is not an HTTP library itself.
- **Trio** offers an alternative to asyncio with a focus on structured concurrency, which can be beneficial for managing complex concurrent operations.
- **uvloop** enhances asyncio’s event loop, improving performance but still relies on asyncio’s abstractions.


## Supported HTTP Methods

RocketHTTP supports the following HTTP methods:
- **GET**
- **POST**
- **PUT**
- **PATCH**
- **DELETE**
- **HEAD**
- **OPTIONS**
- **CONNECT**
- **TRACE**

## Example Usage in Python

You can use RocketHTTP in Python by loading the `.so` file and invoking the appropriate HTTP method.

### Installation

1. Clone the repository:

```bash
git clone https://github.com/coffeecms/Python_RocketHTTP.git
```

2. Copy file "rockethttp.so" into your Python project folder then install `cffi` in Python if you haven't:

```bash
pip install cffi
```

3. Use RocketHTTP in your Python project by loading the shared library.

### Sample Code

Here’s a basic Python example to use RocketHTTP for different HTTP methods:

```python
from cffi import FFI

# Initialize FFI and load the shared library
ffi = FFI()
C = ffi.dlopen("./rockethttp.so")

# Declare Go function to call from Python
ffi.cdef("""
    char* GoSendRequestWithCache(char* method, char* url, char* body, int useHTTP2, int keepAlive, int maxWorkers, int ttl);
""")

# Function to send HTTP requests using RocketHTTP
def send_request_with_cache(method, url, body='', use_http2=False, keep_alive=True, max_workers=10, ttl=60):
    result = C.GoSendRequestWithCache(
        method.encode('utf-8'), 
        url.encode('utf-8'), 
        body.encode('utf-8'),
        int(use_http2), 
        int(keep_alive), 
        max_workers, 
        ttl
    )
    return ffi.string(result).decode('utf-8')

# Example GET request with caching enabled (TTL = 120 seconds)
response = send_request_with_cache("GET", "https://jsonplaceholder.typicode.com/todos/1", use_http2=True, ttl=120)
print("GET Response:", response)

# Example POST request with a JSON body
response = send_request_with_cache("POST", "https://jsonplaceholder.typicode.com/posts", body='{"title":"foo","body":"bar","userId":1}', ttl=120)
print("POST Response:", response)
```

### Method-Specific Examples

Here are examples for each HTTP method supported:

#### GET

```python
response = send_request_with_cache("GET", "https://jsonplaceholder.typicode.com/todos/1", ttl=120)
print("GET Response:", response)
```

#### POST

```python
response = send_request_with_cache("POST", "https://jsonplaceholder.typicode.com/posts", body='{"title":"foo","body":"bar","userId":1}', ttl=120)
print("POST Response:", response)
```

#### PUT

```python
response = send_request_with_cache("PUT", "https://jsonplaceholder.typicode.com/posts/1", body='{"id":1,"title":"foo","body":"bar","userId":1}', ttl=120)
print("PUT Response:", response)
```

#### PATCH

```python
response = send_request_with_cache("PATCH", "https://jsonplaceholder.typicode.com/posts/1", body='{"title":"updated title"}', ttl=120)
print("PATCH Response:", response)
```

#### DELETE

```python
response = send_request_with_cache("DELETE", "https://jsonplaceholder.typicode.com/posts/1", ttl=120)
print("DELETE Response:", response)
```

#### OPTIONS

```python
response = send_request_with_cache("OPTIONS", "https://jsonplaceholder.typicode.com/posts", ttl=120)
print("OPTIONS Response:", response)
```

#### HEAD

```python
response = send_request_with_cache("HEAD", "https://jsonplaceholder.typicode.com/todos/1", ttl=120)
print("HEAD Response:", response)
```

#### TRACE

```python
response = send_request_with_cache("TRACE", "https://jsonplaceholder.typicode.com/todos/1", ttl=120)
print("TRACE Response:", response)
```

## Custom Configuration

RocketHTTP allows several custom configurations, including:
- **use_http2**: Set `True` to enable HTTP/2.
- **keep_alive**: Enable or disable KeepAlive for long-lived connections.
- **max_workers**: Configure the maximum number of Go routines to handle concurrent requests.
- **ttl**: Configure the cache time-to-live for GET and HEAD requests.

### Sample Configuration:

```python
response = send_request_with_cache(
    "GET", 
    "https://jsonplaceholder.typicode.com/todos/1", 
    use_http2=True, 
    keep_alive=True, 
    max_workers=100, 
    ttl=300
)
print("Response:", response)
```

## Contributing

Feel free to fork the repository, submit issues, or open pull requests to improve RocketHTTP.

## License

This project is licensed under the MIT License.
