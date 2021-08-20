---
description: Review best practices to deal with 5XX errors
---

# 5XX Retry Logic Best Practices

## Introduction

Since DataHub is a proxy that passes through errors from full node software, our users will need to adopt defensive strategies for interacting with the API.

We are making it easy for our users to do the right thing and providing examples of pseudo-code to copy/paste.

For Example:

```ruby
tries = 3
begin
  r = RestClient.get(...)
rescue
  tries -= 1
  retry if tries > 0
end
```

### **The basics of a retry**

To decide when to retry a request, we need to consider what to look for. There are a handful of HTTP status codes that you can check against. This will let your retry logic differentiate between a failed request that is appropriate to retry—like a gateway error—and one that isn't—like a 404. In our examples, we will use **408, 500, 502, 503, 504, 522, and 524.**

The next consideration we want is how often to retry. We will start with a delay, then increase it each additional time. This is a concept known as "back-off". The time between requests will grow with each attempt. Finally, we'll also need to decide how many attempts to make before giving up.

**Here's an example of the logic we'll be using in pseudo-code:**

* If total attempts &gt; attempts, continue
* if status code type matches, continue
* if \(now - delay\) &gt; last attempt, try request
* else, return to the start

**Let's explore the best practices for NodeJs, Pyhton, Ruby, and Go:**

{% page-ref page="5xx-retry-logic-best-practices-nodejs.md" %}

{% page-ref page="5xx-retry-logic-best-practices-python.md" %}

{% page-ref page="5xx-retry-logic-best-practices-ruby.md" %}

{% page-ref page="5xx-retry-logic-best-practices-go.md" %}

