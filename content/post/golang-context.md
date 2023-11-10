+++
author = "Okan"
title = "Golang Context "
date = "2023-11-03"
description = "My Exploration on Golang Contexts"
tags = [
    "golang",
    "context"
]
+++

## Introduction

I'm sure that all of us have encountered a chain of dependencies. For instance, when developing software, we use various tools and frameworks. These frameworks, in turn, rely on other libraries, and these libraries may use yet another set of dependencies. The depth of this chain can be quite extensive. Can you imagine this hierarchical and layered system of execution? We often utilize this model in web services. The client calls the server, the server calls services or databases, and the list goes on. This is illustrated in the figure below:
{{< image
src="/hierarchy.png"
alt="This is sample image" >}}

When any actor in the chain cancels their operation or a timeout occurs, we need to propagate this 'cancel' signal to their descendants. Contexts come to the rescue for this purpose. They have two main missions:

- Enabling implicit cancellation with a deadline and timeout.
- Facilitating explicit cancellation.

In addition to these two functions, contexts can also propagate data.

## Context Internals

As you know from CS 101, the best way to represent any hierarchical sequential relationship is by using trees. A tree data structure has a root node and descendants of this root, forming the context.
{{< image
src="/context.png"
alt="This is sample image" >}}

To create node context node we use `ctx := context.Background()`.This is empty node. Also these nodes satisfy the following interface : 
```go
type Context interface {
    Deadline() (deadline time.Time, ok bool)
    Done() <-chan struct{}
    Err() error
    Value(key interface{}) interface{}
}
```
To derive new nodes from the any node we can use following four methods :
- `WithCancel(parent Context) (Context,CancelFunc)`
- `WithTimeout(parent Context, timeout time.Duration) (Context, CancelFunc)`
- `WithDeadline(parent Context, d time.Time) (Context, CancelFunc)`
- `WithValue(parent Context, key, val any) Context`

These functions return derived context node mostly with cancel function. Derived context can be passed to functions to control timeout, deadline or cancellation. **If any node is cancelled,its descendants also cancelled but this does not affects the ancestor nodes.**

In function declaration, context should be first parameter as shown below : 
```go 
func printTheValues(ctx context.Context, keys ...string) {
	for _, key := range keys {
		if v := ctx.Value(key); v != nil {
			stringified, ok := v.(string)
			if !ok {
				continue
			}
			println(key, stringified)
		}
	}
}
```

It is ok, if you do not understand the example above we will come to that. I am putting the snippet only for showing proper context arguman usage.

## Example of Timeout/Deadline







