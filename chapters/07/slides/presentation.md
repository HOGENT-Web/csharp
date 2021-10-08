class: dark middle

# Enterprise Web Development C&#35;
> Chapter 7 - Ain't no REST for the wicked
---

### Chapter 7 - Ain't no REST for the wicked
# Table of contents

- [What is an API?](#api)
- [What is REST?](#rest)
- [HTTP methods and status ranges](#http)
- [Document your API](#documentation)
- [Building a REST API](#building-rest-api)
- [Input validation](#input-validation)
- [gRPC](#grpc)
- [Summary](#summary)

---
name: api
class: dark middle

# Ain't no REST for the wicked
> What is an API?

---
### Ain't no REST for the wicked
# What is an API?

* **A**pplication **P**rogramming **I**nterface
* approach to make software work with other software
* <=> User Interface: let's users work with software
* nowadays mostly in the context of the Web (HTTP)

---
name: rest
class: dark middle

# Ain't no REST for the wicked
> What is REST?

---
### Ain't no REST for the wicked
# What is REST?

- **R**epresentational **S**tate **T**ransfer, [°Roy Fielding in 2000](http://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm)
- **architectural style** for designing networked applications
- nothing more but **using current features of the web**
  - 40y old matured and widely accepted HTTP protocol
  - standard and unified methods (POST, GET, PUT and DELETE)
  - stateless nature of HTTP
  - easy to use **U**niform **R**esource **I**dentifier

---
### Ain't no REST for the wicked
# What is REST?

- leverages these features with 5 constraints:
  - uniform interface
  - client-server
  - stateless
  - cachable
  - layered system

> <a href="https://restfulapi.net/rest-architectural-constraints/" target="_blank">Read more about these constraints</a>

---
### What is REST?
# Uniform interface

> Everything is **Resource**

- fundamental concept of REST
- has
  - data
  - relationships to other resources
  - methods that operates against it to allow for accessing and manipulating the associated information

Examples:
- [www.hogent.be/image/logo.gif]() (Image resource)
- [www.hogent.be/students/1001]() (Dynamically pulled resource)
- [www.hogent.be/videos/v001]() (Video resource)
- [www.hogent.be/home.html]() (Static resource)

---
### What is REST?
# Uniform interface

> Every resource is identified by a **Unique Identifier**

- **U**nifirm **R**esource **L**ocator identifies the online location of a resource
- directory structure-like URIs

Examples:
- Get customer details with name "Shiv": [www.hogent.be/Customers/Shiv]()
- Get customer details with name "Raju": [www.hogent.be/Customers/Raju]()
- Get orders for customer "Shiv": [www.hogent.be/Customers/Shiv/Orders]()
- Get orders for customer "Raju": [www.hogent.be/Customers/Raju/Orders]()

---
### What is REST?
# Uniform interface

> Communication is done by **Representation**

- use some **media type**
  - often JSON (`application/json`)
  - or XML (`application/xml`)
- set the appropriate **HTTP headers**
  - `Accept`: what do you expect as input?
  - `Content-Type`: what are you returning?

---
### What is REST?
# Client-Server

* client and server should be able to evolve independently
* client should be able to do all it needs with the available resource URI's

---
### What is REST?
# Stateless

- every request is independent
- server does not need to remember previous requests and state
- no sessions, no history...

<br />
<img src="./images/REST-stateless.png" width="70%" class="center" />

---
### What is REST?
# Cacheable

* all responses should be made cachable (if possible)
* good caching ensures the server scales better (less requests to process)
* and the client responds faster

---
### What is REST?
# Layered System

* REST allows to spread data and API over several servers
* example:
  * Server A: API
  * Server B: data storage
  * Server C: authentication
* big advantage: servers are able to scale independently

---
name: http
class: dark middle

# Ain't no REST for the wicked
> HTTP methods and status ranges

---
### What is REST?
# HTTP methods

> Describe resource **functionality** with **HTTP methods**

.center[
| Method | Description                             |
| ------ | --------------------------------------- |
| GET    | retrieve a representation of a resource |
| POST   | create new resources and sub-resources  |
| PUT    | update existing resources               |
| PATCH  | partially update existing resources     |
| DELETE | delete existing resources               |
]

This ensures **uniform interfaces** accross multiple REST APIs

---
### What is REST?
# HTTP status ranges in a nutshell

- `1xx`: hold on
- `2xx`: here you go
- `3xx`: go away
- `4xx`: you fucked up
- `5xx`: I fucked up

> <a href="https://en.wikipedia.org/wiki/List_of_HTTP_status_codes" target="_blank">Read about all HTTP status codes yourself</a>

---
name: documentation
class: dark middle

# Ain't no REST for the wicked
> Document your API

---
### Ain't no REST for the wicked
# Document your API

- OpenAPI = specification
- Swagger = tools (for displaying OpenAPI specs, etc.)

<br />
<img src="./images/openapi-swagger.png" width="50%" class="center" />

---
### Document your API
# OpenAPI

- **O**pen**A**PI **S**pecification (OAS)
- formerly known as Swagger
- YAML or JSON
- standard, programming language independent description of a REST API
- only specifies functionality
  - not which implementation
  - not what dataset
  - ...
- **OAS 3.0**: both people and machines can view, understand and interpret the functionality of a REST API
- from documentation the client code can be generated

---
### Document your API
# swagger.json

```{json}
{
  "swagger":"2.0",
  "info":{
    "description":"This is a sample server Petstore server.  You can find out more about Swagger at [http://swagger.io](http://swagger.io) or on [irc.freenode.net, #swagger](http://swagger.io/irc/).  For this sample, you can use the api key `special-key` to test the authorization filters.",
    "version":"1.0.5",
    "title":"Swagger Petstore",
    "termsOfService":"http://swagger.io/terms/",
    "contact":{
      "email":"apiteam@swagger.io"
    }
  },
  "host":"petstore.swagger.io",
  "basePath":"/v2",
}
```

> <a href="https://petstore.swagger.io/v2/swagger.json" target="_blank">Take a look at a live example (you might need a JSON prettifier)</a>

---
### Document your API
# Swagger UI

- to visualize and interact with the API's resources
- auto-generated from OAS

<img src="./images/swagger-ui.png" width="90%" class="center" />

---
### What is REST?
# Consumer

Who can consume a REST API?

- MVC application
- SPA application (Blazor, Angular, React, Vue...)
- The Swagger UI
- Postman app
- ...

---
name: building-rest-api
class: dark middle

# Ain't no REST for the wicked
> Building a REST API

---

### Ain't no REST for the wicked
# Building a REST API

Read through the following tutorial

- [Create a web API with ASP.NET Core](https://docs.microsoft.com/en-us/learn/modules/build-web-api-aspnet-core/)

---
name: input-validation
class: dark middle

# Ain't no REST for the wicked
> Input validation

---
### Ain't no REST for the wicked
# Input validation

Read through these tutorials

- <a href="https://docs.fluentvalidation.net/en/latest/index.html" target="_blank">FluentValidation documentation</a>
- <a href="https://github.com/Blazored/FluentValidation" target="_blank">FluentValidation in Blazor</a>

---
name: grpc
class: dark middle

# Ain't no REST for the wicked
> gRPC

---
### gRPC
# What is gRPC?

- **R**emote **P**rocedure **C**all
- Open-source
- Developed at Google
- **Call a method on a server as if it's a local method** on the client
- Uses **protocol buffers**
- Defines
    - **services**: expose the methods
    - **messages**: what is sent around

> <a href="https://grpc.io/docs" target="_blank">Read the official docs</a>

TODO: probably add video about gRPC in .NET

---
### gRPC
# What is gRPC?

<img src="./images/gRPC-example.svg" class="center" width="70%" />

> Clients and servers can talk to each other in a variety of languages/environments

---
### gRPC
# Protocol buffers

- Mechanism to **serialize data**
- **Independent** of language, platform...
- Like XML or JSON but smaller, faster and simpler
- Works with so called messages
- Messages transformed into a **binary** format before being sent


```{proto}
message Person {
  required string name = 1;
  required int32 id = 2;
  optional string email = 3;
}
```

---
### gRPC
# Typical protocol buffers

- Domain objects
- Requests
- Replies
- ... (whatever you need)


---
### gRPC
# Services

- **Expose methods** on a server
- Clients can call these methods
- Defines methods which
    - take a **message as argument**
    - can **return a message**

```{protobuf}
service Greeter {
  rpc SayHello (HelloRequest) returns (HelloReply) {}
}

message HelloRequest {
  string name = 1;
}

message HelloReply {
  string message = 1;
}
```

---
### Ain't no REST for the wicked
# gRPC

Read through the following tutorial:

- [Code-first gRPC services and clients with .NET](https://docs.microsoft.com/en-us/aspnet/core/grpc/code-first?view=aspnetcore-5.0)

---
name: exercise
class: dark middle

# Ain't no REST for the wicked
> Exercise

---
### Ain't no REST for the wicked
# Exercise

TODO: add SportStore exercise

---
name: solution
class: dark middle

# Ain't no REST for the wicked
> Solution

---
### Ain't no REST for the wicked
# Solution

TODO: add SportStore solution

---
name: summary
class: dark middle

# Ain't no REST for the wicked
> Summary

---
### Ain't no REST for the wicked
# Summary

- REST is **not a standard**
- set of **5 constraints** to call an API **RESTful**
  - Uniform interface
  - Client-server separated
  - Stateless
  - Cachable
  - Layered system
