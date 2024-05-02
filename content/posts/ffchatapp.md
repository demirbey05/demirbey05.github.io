+++
author = "Okan"
title = "Websocket Chat App with Golang "
date = "2023-10-28"
description = "Basic implementation of websocket for chatting"
tags = [
    "golang",
]
+++

## Introduction

Just two months ago, I decided to dedicate my weekends to exploring Golang. I completed [A Tour of Go](https://go.dev/tour/list), and I must say, I was very impressed by Golang's simplicity and performance ratio. It's as powerful and straightforward as any developer could dream of. After that weekend, I couldn't continue my Golang journey because I shifted my focus to C/C++. Currently, I'm fully immersed in developing on-chain games. These games are entirely implemented on the blockchain, and their latency and throughput are entirely dependent on the blockchain. This results in a highly unsatisfactory user experience. Imagine playing CS2 and after shooting someone, you have to wait for the blockchain consensus to register the kill. That's the current state of on-chain games - severely lacking in terms of both latency and throughput. Two weeks ago, I crafted a rollup architecture specifically to address these issues,[as illustrated here](https://x.com/okan_buidl/status/1713679567020347843?t=-KmYSEEJ3eHOvIslqM4knw&s=33). Building such a system requires a deep mastery of Golang, which is why I've committed to furthering my journey with it. The best way to master something is to get your hands dirty, so I've embarked on my Golang build journey. My inaugural project is a Chat application.You can reach the repo from [here](https://github.com/demirbey05/chat-app-websocket). Let's start.


## Server-Side Rendering the Webpage

I decided that the first step should be to serve the front-end code. For this task, I utilized the Gin framework. You can access the front-end code from the repository.
I created my project folder and `main.go` . In Gin framework, you need to define relative paths of HTTP requests and its handlers as shown below : 
```go
func main(){
    r := gin.Default() // Create *gin.Engine object

    r.GET("/",HomeHandler)
    r.LoadHTMLFiles("static/index.html")
    r.Run("0.0.0.0:8080")
}

func HomeHandler(c *gin.Context) {
	c.HTML(http.StatusOK, "index.html", nil)
}
```
Using r.GET("/", HomeHandler), when a client sends a GET request to the main page like "chatapp.com", it triggers the handler function, in this case, HomeHandler.
I also need to serve js and css files for my website. I modified the by adding `r.Static()`.

```go 
func main(){

    fmt.Println("Server is starting ...")
    r := gin.Default()

    r.Static("/css", "./static/css") 
	r.Static("/js", "./static/js")

    r.GET("/",HomeHandler)
    r.LoadHTMLFiles("static/index.html")
    r.Run("0.0.0.0:8080")
}
```

This is my project structure :
```
├── static
│   ├── css
│   │   ├── styles.css
│   ├── index.html
│   ├── js
│   │   ├── app.js
├── main.go
├── go.mod
```

I completed the site serving part of the project, let's continue with Websocket integration.


## Websocket Architecture

![Our Architecture](/backend-arch.png)

As evident from the diagram, we have four fundamental components:

- **wsHandler** :  This component manages the websocket handshake. To establish a websocket connection, an initial HTTP request is required, which is then upgraded to a websocket connection. This component not only oversees the connection upgrade but also retrieves the username from the user and directs the Registerer component to record the user.
- **Registerer** : The Registerer gathers information from registering users and sets up a listener for each registered user.
- **Listener**   : This component is created for each user. It listens for incoming messages from the user and forwards message information to the broadcaster.
- **Broadcaster**: This component disseminates messages to all connected clients.

That's it for now. Let's meet next part.