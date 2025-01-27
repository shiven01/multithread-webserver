# Multithreaded Web Server in Rust

This is a simple multithreaded web server implemented in Rust. It uses a thread pool to handle incoming connections concurrently, allowing it to serve multiple requests simultaneously.

## Overview

The project consists of two main files:

- `lib.rs`: Contains the implementation of a `ThreadPool` for managing worker threads.
- `main.rs`: Implements a basic web server that listens for incoming TCP connections and handles them using the thread pool.

### Features

- **Thread Pool**: The `ThreadPool` struct manages a fixed number of worker threads to handle tasks concurrently.
- **HTTP Request Handling**: The server can handle basic HTTP GET requests and serve static files (e.g., HTML).
- **Concurrency**: The server can handle multiple connections simultaneously, thanks to the thread pool.

## How It Works

### Thread Pool (`lib.rs`)

- The `ThreadPool` struct creates a specified number of worker threads.
- Each worker thread listens for jobs (closures) on a shared channel.
- When a job is received, the worker executes it.

### Web Server (`main.rs`)

- The server listens for incoming TCP connections on `127.0.0.1:7878`.
- For each connection, a job is sent to the thread pool to handle the request.
- The server responds with either:
  - A "200 OK" response and the contents of `hello.html` for the root path (`/`).
  - A "200 OK" response and the contents of `hello.html` after a 5-second delay for the `/sleep` path.
  - A "404 NOT FOUND" response and the contents of `404.html` for all other paths.

## Usage

### Prerequisites

- Install [Rust](https://www.rust-lang.org/).

### Running the Server

1. Clone the repository or copy the code into your project.
2. Navigate to the project directory.
3. Run the server:
   ```bash
   cargo run
