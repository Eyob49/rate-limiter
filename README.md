# Rate Limiter

A thread-safe token bucket rate limiter implementation in Go.

## Features

- Token bucket algorithm for rate limiting
- Configurable capacity and refill rate
- Thread-safe concurrent access with `sync.Mutex`
- Time-based token refill

## Installation

```bash
git clone https://github.com/Eyob49/rate-limiter.git
cd rate-limiter
go build
```

## Usage

```go
package main

import (
    "fmt"
)

func main() {
    // Create limiter: capacity=5 tokens, refill 1 token per second
    limiter := NewTokenBucket(5, 1)

    // Simulate 10 requests
    for i := 1; i <= 10; i++ {
        if limiter.Allow() {
            fmt.Printf("Request %d: ALLOWED\n", i)
        } else {
            fmt.Printf("Request %d: BLOCKED (rate limit)\n", i)
        }
    }
}
```

## How It Works

Token Bucket Algorithm:
- Start with N tokens in a bucket (capacity)
- Each `Allow()` call consumes 1 token if available
- Tokens refill over time at a configured rate
- Once bucket is full, no more tokens are added

## Implementation

- `Limiter` interface defines the rate limiting contract
- `TokenBucket` implements token bucket algorithm
- Thread-safe with `sync.Mutex` protection