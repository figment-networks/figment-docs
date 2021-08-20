---
description: Review best practices to deal with 5XX errors in Ruby
---

# 5XX Retry Logic Best Practices - Ruby

## Method 1 `ensure`

The `ensure` keyword is used for ensuring that a block of code runs, even when an exception happens.

We’d like to ensure the TCP connection opened by Net::HTTP.start is closed, even if the request fails because it times out, for example. To do this, we’ll first wrap our request in a `begin`/`ensure`/`end` block. The code in the ensure part will always run, even if an exception is raised in the preceding begin block.

```ruby
require "net/http"

begin
  puts "Opening TCP connection..."
  http = Net::HTTP.start(uri.host, uri.port)
  puts "Sending HTTP request..."
  puts http.request_get(uri.path).body
ensure
  if http
    puts "Closing the TCP connection..."
    http.finish
  end
end
```

The `retry` keyword allows to retry a piece of code in a block. Combined with a `rescue` block, we can use it to try again if we fail to open the connection, or if the API takes too long to respond.

To do that, we’ll add a `read_timeout` to the `Net::HTTP.start` call which sets the timeout to 10 seconds. If a response to our request hasn’t come in by then, it’ll raise a `Net::ReadTimeout`.

We’ll also match on `Errno::ECONNREFUSED` to handle the API being down completely, which would prevent us from opening the TCP connection. In that case, the http variable is nil.

The exception is rescued and `retry` is called to start the `begin` block again, which results in the code doing the same request until no timeout occurs. We’ll reuse the `http` object which holds the connection if it already exists.

```ruby
require "net/http"

http = nil
uri = URI("http://localhost:4567/")

begin
  unless http
    puts "Opening TCP connection..."
    http = Net::HTTP.start(uri.host, uri.port, read_timeout: 10)
  end
  puts "Executing HTTP request..."
  puts http.request_get(uri.path).body
rescue Errno::ECONNREFUSED, Net::ReadTimeout => e
  puts "Timeout (#{e}), retrying in 1 second..."
  sleep(1)
  retry
ensure
  if http
    puts "Closing the TCP connection..."
    http.finish
  end
end
```

Now, our request will retry every second until no `Net::ReadTimeout` is raised.

Giving up: reraising exceptions using `raise`

Whenever a timeout happens, we’ll increment the number and check if it’s less than or equal to three, because we’d like to retry three retries at most. If so, we’ll retry. If not, we’ll raise to reraise the last exception.

```ruby
require "net/http"

http = nil
uri = URI("http://localhost:4567/")
retries = 0

begin
  unless http
    puts "Opening TCP connection..."
    http = Net::HTTP.start(uri.host, uri.port, read_timeout: 1)
  end
  puts "Executing HTTP request..."
  puts http.request_get(uri.path).body
rescue Errno::ECONNREFUSED, Net::ReadTimeout => e
  if (retries += 1) <= 3
    puts "Timeout (#{e}), retrying in #{retries} second(s)..."
    sleep(retries)
    retry
  else
    raise
  end
ensure
  if http
    puts 'Closing the TCP connection...'
    http.finish
  end
end
```

By using the `retries` variable in the call to `sleep`, we can increase the wait time for every new attempt. Check out the source [HERE](https://blog.appsignal.com/2018/05/16/ensure-retry-and-reraise-exceptions-in-ruby.html).

## Method 2

When we are sending an HTTP request and would like to have 3 retries if it fails due to connection errors. We can do this by following the steps below:

```ruby
require 'http'

def send_request(params)
  with_connection_retry { HTTP.post("http://example.com/resource", params: 
    params) }
end

def with_connection_retry
  retries = 0

  loop do
    yield
  rescue HTTP::ConnectionError => e
    retries += 1

    raise e if retries >= 3
  end
end
```

Another way to perform the same action is by using Ruby's native API instead of using loops:

```ruby
def send_request(params)
  with_connection_retry { HTTP.post("http://example.com/resource", params: 
    params) }
end

def with_connection_retry
  retries ||= 0

  begin
    yield
  rescue HTTP::ConnectionError => e
    retries += 1
    raise e if retries >= 3
    retry
  end
end
```

