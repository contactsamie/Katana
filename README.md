# Katana
About Owin Implemetation

Katana is the Microsoft implemetation of owin specification

It exposes four definiions in order to achieve one of many goals of bringing into .NET the same kind of ease with which a web applications can be spawn up as there is in nodejs

1. System Host Absraction aka environment variables env
IDictionary<string, object>

2. Middleware/Framework Abstraction aka AppFunc
 Func<env,Task>

3. An Inline Middleware Factory aka Inline IAppBuilder Factory
Use(Func<env*,AppFunc next,Task>)

4. A Generic Middleware Factory aka Generic IAppBuilder Factory
Use<T>(R options)  
where T is new(AppFunc next) and has a method
Task Invoke(env)

env*=new OwinContext(env)

The required dictionary keys for an HTTP request are:


"owin.RequestBody"  env*.Request.Body

A Stream with the request body, if any. Stream.Null MAY be used as a placeholder if there is no request body. See Request Body.

"owin.RequestHeaders"  env*.Request.Headers

An IDictionary<string, string[]> of request headers. See Headers.

"owin.RequestMethod"  env*.Request.Method

A string containing the HTTP request method of the request (e.g., "GET", "POST").

"owin.RequestPath"  env*.Request.Path

A string containing the request path. The path MUST be relative to the "root" of the application delegate; see Paths.

"owin.RequestPathBase" env*.Request.PathBase

A string containing the portion of the request path corresponding to the "root" of the application delegate; see Paths.

"owin.RequestProtocol"  env*.Request.Protocol

A string containing the protocol name and version (e.g. "HTTP/1.0" or "HTTP/1.1").

"owin.RequestQueryString"  env*.Request.QueryString

A string containing the query string component of the HTTP request URI, without the leading “?” (e.g., "foo=bar&baz=quux"). The value may be an empty string.

"owin.RequestScheme"  env*.Request.Scheme

A string containing the URI scheme used for the request (e.g., "http", "https"); see URI Scheme.


#Host Responsibilities
1.Managing the underlying process.
2.Orchestrating the workflow that results in the selection of a server and the construction of an OWIN pipeline through which requests will be handled.

#Server Responsibilities
1.Open a network socket
2.Listen for requests
3.Send them through the pipeline of OWIN components specified by the user 


