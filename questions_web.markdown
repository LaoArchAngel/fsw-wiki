*Questions related to web skills.  For example, web services, LBs, how the web works, DNS, REST, etc.*

---

# Phone Screen Questions

## Easy Questions

---

## Med Questions

#### Q: If you are building a form on a site, such as a form that takes a user’s address, do you think validation should happen on the client or the server side?

#### A: Both.

Client-side because it means a more responsive user experience and less chatter over the wire
* A good answer here indicates decent UI or usability skills
* If client-side is not mentioned, they may not have much web or JS experience

Server-side because code should never trust that a client has validated input (security).  Some validation also requires complex validation like asserting that a city matches a zip code, which is impractical to do client-side.
* A good answer here indicates solid coding fundamentals and at least rudimentary focus on security.
* If server-side is not mentioned, they may be more of a JS/HTML developer than a full-stack

#### Follow-Ups:
* Ask them “Why?” if they don’t give much explanation
* If they only give one, ask if they see a downside to only focusing on that type.  That should guide them towards thinking about both.

---

#### Q: What is the difference between and `HttpModule` and an `HttpHandler`?

#### A: 
* An `HttpModule` will execute for every request to your application, regardless of extension, and is generally used for cross-cutting concerns like security, statistics, logging, etc.  An `HttpModule` is a step in the execution of a web request.
* An `HttpHandler` is generally associated with a specific extension, and is used for things like RSS feeds, dynamic image generation or modification, and the like.  An `HttpHandler` is the end destination of a web request.

---

#### Q: What are the primary modes of Session storage in ASP.NET?

#### A:
* InProc mode, which stores session state in memory on the Web server. This is the default.
* StateServer mode, which stores session state in a separate process called the ASP.NET state service. This ensures that session state is preserved if the Web application is restarted and also makes session state available to multiple Web servers in a Web farm.
* SQLServer mode stores session state in a SQL Server database. This ensures that session state is preserved if the Web application is restarted and also makes session state available to multiple Web servers in a Web farm.
* Custom mode, which enables you to specify a custom storage provider.
* Off mode, which disables session state.

---

## Hard Questions

`Question`: What are some common network load-balancing algorithms?

`Answer`:

* Round Robin (sometimes called "Next in Loop").
* Weighted Round Robin -- as Round Robin, but some servers get a larger share of the overall traffic.
* Random.
* Source IP hash. Connections are distributed to backend servers based on the source IP address. If a webnode fails and is taken out of service the distribution changes. As long as all servers are running a given client IP address will always go to the same web server.
* URL hash. Much like source IP hash, except hashing is done on the URL of the request. Useful when load balancing in front of proxy caches, as requests for a given object will always go to just one backend cache. This avoids cache duplication, having the same object stored in several / all caches, and increases effective capacity of the backend caches.
* Least connections, weighted least connections. The load balancer monitors the number of open connections for each server, and sends to the least busy server.
* Least traffic, weighted least traffic. The load balancer monitors the bitrate from each server, and sends to the server that has the least outgoing traffic.
* Least latency. Perlbal makes a quick HTTP OPTIONS request to backend servers, and sends the request to the first server to answer.

---

# In-person questions

## Easy Questions

## Med Questions

## Hard Questions

---

# Whiteboard questions

## Easy Questions

## Med Questions

## Hard Questions