# Simple HTTP Forward Proxy (Python)

A minimal **HTTP forward proxy** built using Python sockets to understand how client requests travel through an intermediary server before reaching the destination.

This project demonstrates:

* HTTP request forwarding (GET / POST)
* HTTPS tunneling using the `CONNECT` method
* Bidirectional socket relaying
* Multi-threaded client handling

The implementation is intentionally simple and focused on learning networking fundamentals.

---

## 📌 Purpose

I built this project to learn:

* How HTTP requests are structured
* How forward proxies work internally
* TCP socket programming in Python
* Difference between HTTP forwarding and HTTPS tunneling
* Handling multiple connections using threads

The goal is to understand the **flow of data between client → proxy → server**.

---

## 🧱 Project Structure

```
simple-http-forward-proxy/
│
├── https_proxy.py   # Main proxy server
└── README.md        # Documentation
```

---

## ⚙️ Requirements

You only need:

* Python 3.x

No external libraries are required.

Check Python installation:

```
python --version
```

---

## ▶️ Running the Proxy

Open the project folder in **VS Code** or terminal and run:

```
python https_proxy.py
```

You should see:

```
[INFO] Starting HTTP Proxy on 0.0.0.0:8080 ...
```

This means the proxy server is running.

---

## 🌐 Configure Browser / Client Proxy

Set manual proxy configuration:

```
HTTP Proxy: 127.0.0.1
Port: 8080
```

After this, browser traffic will pass through the proxy.

For HTTPS websites, the browser automatically sends a `CONNECT` request and the proxy creates a secure TCP tunnel without decrypting data.

---

## 🔎 How It Works

### HTTP Flow

1. Client sends request to proxy
2. Proxy parses headers and extracts host
3. Proxy connects to destination server
4. Server response is relayed back to client

```
Client → Proxy → Server
       ←       ←
```

### HTTPS Flow

1. Browser sends `CONNECT host:443`
2. Proxy opens socket to server
3. Proxy relays encrypted bytes both directions

No TLS interception or inspection is performed.

---

## ✨ Features

* HTTP GET / POST forwarding
* HTTPS CONNECT tunneling
* Thread-per-connection model
* Raw socket communication
* Minimal logging for learning

---

## 🚫 Limitations (Intentional)

* No caching
* No authentication
* Blocking sockets
* No connection pooling
* No request modification
* Not production ready

This keeps the project simple and focused on learning.

---

## 🧠 Implementation Notes

* Built using Python `socket` module
* Each client connection runs in its own thread
* A relay function forwards bytes in both directions
* CONNECT method creates a tunnel instead of parsing HTTP
* Headers decoded using ISO-8859-1 for safe parsing

---

## 🧪 Testing Example

Using curl:

```
curl -x http://127.0.0.1:8080 http://example.com
```

If the page loads, the proxy is working.

---

## 🚀 Future Improvements

* Async version using asyncio
* Request logging dashboard
* Caching support
* Authentication
* Performance optimization
* Connection reuse

---

## ⚠️ Disclaimer

This project is an educational implementation to understand forward proxy mechanics.
It should not be used as a production proxy or for security-sensitive environments.
