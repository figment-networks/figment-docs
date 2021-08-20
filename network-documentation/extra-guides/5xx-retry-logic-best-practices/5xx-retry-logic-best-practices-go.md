---
description: Review best practices to deal with 5XX errors in Go
---

# 5XX Retry Logic Best Practices - Go

## Method 1 - Using retry:

```go
package retry

import (
    "math/rand"
    "net/http"
    "time"
)

var (
    defaultSleep = 500 * time.Millisecond
)

// Func is the function to be executed and eventually retried.
type Func func() error

// HTTPFunc is the function to be executed and eventually retried.
// The only difference from Func is that it expects an *http.Response on the first returning argument.
type HTTPFunc func() (*http.Response, error)

// Do runs the passed function until the number of retries is reached.
// Whenever Func returns err it will sleep and Func will be executed again in a recursive fashion.
// The sleep value is slightly modified on every retry (exponential backoff) to prevent the thundering herd problem (https://en.wikipedia.org/wiki/Thundering_herd_problem).
// If no value is given to sleep it will defaults to 500ms.
func Do(fn Func, retries int, sleep time.Duration) error {
    if sleep == 0 {
        sleep = defaultSleep
    }

    if err := fn(); err != nil {
        retries--
        if retries <= 0 {
            return err
        }

        // preventing thundering herd problem (https://en.wikipedia.org/wiki/Thundering_herd_problem)
        sleep += (time.Duration(rand.Int63n(int64(sleep)))) / 2
        time.Sleep(sleep)

        return Do(fn, retries, 2*sleep)
    }

    return nil
}

// DoHTTP wraps Func and returns *http.Response and error as returning arguments.
func DoHTTP(fn HTTPFunc, retries int, sleep time.Duration) (*http.Response, error) {
    var res *http.Response

    err := Do(func() error {
        var err error
        res, err = fn()
        return err
    }, retries, sleep)

    return res, err
}
```

Check out this Awesome Github repo for more details and pseudo code - [Here](https://github.com/rafaeljesus/retry-go)

Simple Go Lang. Library for retry mechanism - [Check Here](https://github.com/avast/retry-go)

## Method 2 - Using go-retryablehttp

The `retryablehttp` package provides a familiar HTTP client interface with automatic retries and exponential backoff. It is a thin wrapper over the standard `net/http` client library and exposes nearly the same public API. This makes `retryablehttp` very easy to drop into existing programs.

`retryablehttp` Performs automatic retries under certain conditions. Mainly, if an error is returned by the client \(connection errors, etc.\), or if a 500-range response code is received \(except 501\), then a retry is invoked after a wait period. Otherwise, the response is returned and left to the caller to interpret.

The main difference from `net/http` is that requests which take a request body \(POST/PUT et. al\) can have the body provided in a number of ways \(some more or less efficient\) that allow "rewinding" the request body if the initial request fails so that the full request can be attempted again.

**Example Use**

Using this library should look almost identical to what you would do with `net/http`. The most simple example of a GET request is shown below:

```go
resp, err := retryablehttp.Get("/foo")
if err != nil {
    panic(err)
}
```

The returned response object is an `*http.Response` the same thing you would usually get from `net/http`. Had the request failed one or more times, the above call would block and retry with exponential backoff.

For more usage and examples see the [godoc ](https://pkg.go.dev/github.com/hashicorp/go-retryablehttp)& [GitHub ](https://github.com/hashicorp/go-retryablehttp/tree/991b9d0a42d13014e3689dd49a94c02be01f4237)

