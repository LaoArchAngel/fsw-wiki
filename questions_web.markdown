*Questions related to web skills.  For example, web services, LBs, how the web works, DNS, REST, etc.*

---

# Phone Screen Questions

## Easy Questions

#### Q: What is the difference between server-side and client-side code?

#### A: Server-side code executes on a web server, while client-side code executes in a user's client (typically a browser).  For example, in an ASP.NET application, C# is server side and creates HTML and JS code that is sent back to the browser to be executed as client-side code.

---

#### Q: What is the difference between a cookie and an asp.net session?

#### A: Sessions are server-side and contain user information, while Cookies are client-side files that contain user information. Sessions have a unique identifier that maps them to specific users. This identifier can be passed in the URL or saved into a session cookie.  In the latter case, clearing your cookie will result in clearing your session because your unique sessionID will be lost.

---

#### Q: In terms of load balancing, what does *sticky session* mean?

#### A: When multiple servers are processing web requests, a load balancer will route requests to servers based on one of many possible strategies.  A Sticky Session means that the same web server will handle all requests from a user's session (that user's requests will not be sent to different web servers).

---

## Med Questions

`Question`: What does it mean when we say that HTTP is stateless?

`Answer`: All HTTP requests are separate and must contain enough information on their own to fulfill the request, in isolation.  HTTP requests cannot be associated with each other absent some shared info the server knows about (which is often some correlation id passed in the cookie header).

---

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

`Question`: How does a CDN work?

`Answer`: A Content Delivery Network is a method of distributing web-based content (like an image or CSS file) on Edge servers all over the country or world so that requests for those resources experience fewer network hops and are literally physically closer to requesting users' machines.  This minimizes the time it takes for resources to be deliver to a client, speeding site operation.  It also distributes load from web servers in 1-2 locations to redundant servers all around the world that are optimized to handle traffic elastically.

---

#### Q: Why is the TTL of DNS records important for site speed?

#### A: 
Higher TTL values prevent repeat visitors from needing to perform frequent DNS lookups.  This saves time during requests and results in a quicker time to first byte.

---

#### Q: What are the 4 common HTTP methods used with REST services?

#### A:
GET, POST, PUT, DELETE

---

#### Q: What is the difference between a redirects using 301 and 302 response codes?

#### A:
A 301 response code indicates that the content has been moved permanently.  In addition to this being cached heavily by browsers, it also has SEO significance.  A 302 response code indicates that the content is now found somewhere else, but maybe only temporarily.

#### Q: When I type www.fsw.com in the address bar of a web browser, what happens next? Please be as descriptive as you possibly can to demonstrate the breadth of your knowledge. We can dig deeper into topics as you enumerate them.

#### A: This is a very open-ended question intended to understand the breadth of knowledge of the interviewee. The topics that they should be able to touch are IP packets, routing, DNS, load balancing, SSL/TLS, web servers, static html, web applications, distributed systems, databases, sessions, multi-threading, threadpools, etc.

---

#### Q: What is XSS (Cross-Site Scripting)?

#### A:  A type of web application security vulnerability enabling attackers to inject client-side script into Web pages viewed by other users. A cross-site scripting vulnerability may be used by attackers to bypass access controls such as the same-origin policy. 

#### Follow-Up: How can XSS be prevented?

#### A: <TODO>

---

#### Q: What is XSRF/CSRF (Cross-Site Request Forgery)?

#### A:  Also known as a `one-click attack` or `session riding`, is a type of malicious exploit of a website whereby unauthorized commands are transmitted from a user that the website trusts. Unlike cross-site scripting (XSS), which exploits the trust a user has for a particular site, CSRF exploits the trust that a site has in a user's browser.

#### Follow-Up: Who can XSRF be prevented?

#### A: <TODO>

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

#### Q: Name a few IP addresses that are not internet routable.

#### A:
Any address in the following ranges is correct.
* 10.0.0.0 - 10.255.255.255
* 192.168.0.0 - 192.168.255.255
* 172.16.0.0 - 172.31.255.255


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