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