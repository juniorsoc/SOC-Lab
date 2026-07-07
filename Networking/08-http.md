# HTTP — Statelessness, Sessions, and Structure

## Statelessness and Sessions

HTTP, with or without TLS encryption (denoted by the "S" in HTTPS), is fundamentally stateless: the server treats every incoming request as entirely independent and retains no memory of previous requests on its own. This creates an obvious problem for anything requiring continuity, such as staying logged in across multiple page loads.

The solution is the combination of sessions and cookies. When a user authenticates, the server generates a unique session identifier and stores it in a cookie on the client's browser. On every subsequent request, the browser automatically includes that cookie, allowing the server to recognize the user without requiring re-authentication on every single interaction. Session hijacking exploits this mechanism directly: if an attacker steals a valid session identifier from a victim's cookie, they can impersonate that user without ever needing to know their password, since the server has no way of distinguishing between the legitimate holder of the session and anyone else presenting the same identifier.

## URL Structure

A URL is composed of several distinct parts, each serving a specific function. The scheme indicates which protocol the browser should use to communicate, such as HTTP or HTTPS. Optional user credentials may precede the host if the destination requires authentication embedded directly in the URL. The host identifies the server being contacted, and an optional port specifies which service on that server to connect to, defaulting to standard values depending on the scheme in use. The path identifies a specific resource on the server, a query string carries additional parameters relevant to the request, and a fragment identifies a specific location within the returned resource, typically handled entirely on the client side.

## HTTP Requests and Responses

An HTTP request is composed of a request line specifying the method, target path, and protocol version, followed by a set of headers that provide additional context about the request. The User-Agent header identifies what software is making the request, and requests coming from automated tools rather than genuine browsers are often worth additional scrutiny. The Referer header indicates which page linked to the current request, and its absence or an unusual value can sometimes be informative during an investigation.

An HTTP response similarly opens with a status line indicating the protocol version and status code, followed by response headers. The Server header often reveals the specific software and version running on the server, which is valuable both to legitimate administrators and to anyone probing for known vulnerabilities associated with outdated software versions. The Content-Type header describes what kind of data the response contains, and a mismatch between the declared content type and the file's actual contents can be a sign of an attempt to disguise malicious content.

## HTTP Methods

HTTP defines several methods that indicate the type of action being requested. GET retrieves data from the server without modifying anything. POST submits new data, commonly used for actions like logging in or creating new records. PUT updates an existing resource. DELETE removes a resource entirely. The pattern of methods observed in a stream of requests can reveal a great deal about what's actually happening — for instance, an unusual concentration of POST requests directed at a login endpoint can indicate an automated attempt to guess credentials, while unexpected DELETE or PUT requests against sensitive resources may indicate unauthorized tampering.

## HTTP Status Codes

Status codes are grouped into ranges that broadly indicate the outcome of a request. Codes in the 2xx range indicate success. Codes in the 3xx range indicate that the requested resource has moved and the client should look elsewhere. Codes in the 4xx range indicate a problem with the request itself, originating on the client side. Codes in the 5xx range indicate that something went wrong on the server while attempting to process an otherwise valid request.

Within these ranges, certain codes recur often enough to be worth knowing individually. A 200 indicates the request succeeded as expected. A 401 indicates that authentication is required but wasn't provided. A 403 indicates that the request was understood and the client was identified, but access has nonetheless been denied. A 404 indicates that the requested resource simply doesn't exist. A 500 indicates an unhandled failure on the server side while processing the request.

Patterns in these codes across a log file often carry investigative significance. A concentrated burst of 404 responses originating from a single source frequently indicates automated scanning for hidden files or directories that don't normally exist. A concentrated burst of 401 or 403 responses can indicate a sustained attempt to access resources without proper authorization.

## HTTP Headers

Request headers carry information from the client to the server. Beyond the User-Agent and Referer already discussed, the Host header specifies which particular site is being requested, relevant since a single server can host multiple distinct websites. The Content-Length header indicates the size of any data being submitted with the request, and the Accept-Encoding header specifies which compression methods the client is able to handle. The Cookie header carries any values the server previously asked the client to store, most commonly the session identifier discussed earlier.

Response headers carry information back from the server to the client. The Set-Cookie header instructs the browser to store a new cookie value. The Cache-Control header dictates how long, if at all, the browser should retain a cached copy of the response. The Content-Type header describes the nature of the returned content, and Content-Encoding specifies what compression, if any, was applied before transmission.

Reviewing headers during an investigation can surface a range of anomalies: a User-Agent identifying a scripting library rather than a genuine browser, a missing Host header where one would normally be expected, an unexpected or duplicated Cookie value suggestive of a stolen session, or a Content-Type that doesn't match the actual nature of the file being transferred.

## Practical Example — Inspecting a Raw HTTP Exchange

```bash
$ curl -v http://example.com/login
> GET /login HTTP/1.1
> Host: example.com
> User-Agent: curl/8.4.0
> Accept: */*
>
< HTTP/1.1 200 OK
< Server: nginx/1.18.0
< Content-Type: text/html
< Set-Cookie: session_id=a1f9c3...; HttpOnly
```

```bash
$ grep " 404 " access.log | awk '{print $1}' | sort | uniq -c | sort -rn | head -3
    342 203.0.113.44
      8 198.51.100.7
      2 192.0.2.15
```

The second command counts 404 responses per IP and sorts by frequency — 342 not-found requests from a single IP in a short window is a strong signal of directory/endpoint brute-forcing, and is exactly the kind of query a SOC analyst runs when triaging a busy access log.
