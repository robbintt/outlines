# Modern HTTP/1.1 RFCs

`HTTP/1.1 RFC2616` replaced in 2014 by `RFCs 7230-7237`

Any `connection`, `port`, `protocol` can be used and is out of scope of the RFC.

The HTTP URI scheme `http` indicates TCP over IP with default tcp port 80.

This document highlights `rfc7230`, `rfc7231`, and `rfc7232` as of January 2019.


### Future

- Digesting the cacheing RFC will take some time (rfc7234).
- I am not sure what range requests are for, that's worth some quick research
    - [MDN on Range Requests](https://developer.mozilla.org/en-US/docs/Web/HTTP/Range_requests)


### Primary RFCs Summarized Below

These are the eight HTTP/1.1 RFCs. Other RFCs are discussed inside these RFCs.

- [Message Syntax and Routing](https://tools.ietf.org/html/rfc7230)
- [Semantics and Content](https://tools.ietf.org/html/rfc7231)
- [Conditional Requests](https://tools.ietf.org/html/rfc7232)
- [Range Requests](https://tools.ietf.org/html/rfc7233)
- [Caching](https://tools.ietf.org/html/rfc7234)
- [Authentication](https://tools.ietf.org/html/rfc7235)
- [Authentication Scheme Registrations](https://tools.ietf.org/html/rfc7236)
- [Method Registrations](https://tools.ietf.org/html/rfc7237)


### rfc7230 Highlights

- [Four distinct formats for request-target UgRI](https://tools.ietf.org/html/rfc7230#section-5.3)
- [Client w/ 2+ requests must maintain a time-ordered list and correlate first response to first request](https://tools.ietf.org/html/rfc7230#section-5.6)
- [Intermediaries may transform some message body. Sender can specify not to transform. Avoid for medical imaging etc.](https://tools.ietf.org/html/rfc7230#section-5.7.2)
    - [Payload Semantics e.g. PUT request vs POST request vs GET response](https://tools.ietf.org/html/rfc7231#section-3.3)
- [Persistence - HTTP/1.1 defaults to persistence](https://tools.ietf.org/html/rfc7230#section-6.3)
    - "close" connection option specifies a connection will not persist after current request/response.
    - related to HTTP/1.0 `keep-alive`
- [Pipelining](https://tools.ietf.org/html/rfc7230#section-6.3.2)
    - client can send mult. simulatenous requests, 
    - server can process requests with safe methods in parallel, must respond in order
        - Idempotent methods - don't pipeline after non-idempotent methods (see `rfc7231 highlights` in this document)
- [Tear-down & using the "Connection" header field "close" option](https://tools.ietf.org/html/rfc7230#section-6.6)
    - If client sends a "close" option, server response should have a "close" option
    - Server must close that connection after that response
    - Client must not use that connection again and must close the connection
    - If server sends "close" option in response
        - Client SHOULD NOT assume additional pipelined requests will be processed by server (no obligation to process by server)
    - `TCP reset problem` and half-closed connections (close write then close read) discussed inside


### rfc7231 Highlights

This contains `request methods`, `method header fields`, and `content representation`, among other things.

- [Representation Headers](https://tools.ietf.org/html/rfc7231#section-3.2)
    - data type of representation data is determined by header fields `Content-Type` and `Content-Encoding`
    - two-layer encoding model: `representation-data := Content-Encoding( Content-Type( bits ) )`
- [Content Negotation](https://tools.ietf.org/html/rfc7231#section-3.4)
    - `proactive` or `reactive` for negotiating `formats`, `languages`, or `encodings`
    - could influence which representation, among those available, would be best to deliver
- [Request Methods: GET, HEAD, POST, PUT, DELETE, CONNECT, OPTIONS, TRACE](https://tools.ietf.org/html/rfc7231#section-4)
    - All general purpose servers must support `GET` and `HEAD` (all others optional)
    - See `IANA HTTP Methods Registry` in this document's `References` for an up to date index of HTTP methods and their RFCs.
    - Concept of `safe methods`
        - Safe methods must be implemented in a safe way, beyond scope of spec
        - Of the request methods defined by this specification, the GET, HEAD, OPTIONS, and TRACE methods are defined to be safe.

        > Request methods are considered "safe" if their defined semantics are essentially read-only; i.e., the client does not request, and does not expect, any state change on the origin server as a result of applying a safe method to a target resource.  Likewise, reasonable use of a safe method is not expected to cause any harm, loss of property, or unusual burden on the origin server.  

        > This definition of safe methods does not prevent an implementation from including behavior that is potentially harmful, that is not entirely read-only, or that causes side effects while invoking a safe method.  What is important, however, is that the client did not request that additional behavior and cannot be held accountable for it.

- [idempotent Request methods: PUT, DELETE, safe request methods](https://tools.ietf.org/html/rfc7231#section-4.2.2)

    > Idempotent methods are distinguished because the request can be repeated automatically if a communication failure occurs before the client is able to read the server's response.

- [Method Definitions - for all methods](https://tools.ietf.org/html/rfc7231#section-4.3)

- [Request Header Fields](https://tools.ietf.org/html/rfc7231#section-5)

- [Response Status Codes](https://tools.ietf.org/html/rfc7231#section-6)
    - Range is 1xx-5xx, extensible
    - See `IANA Status Code Registry` URL in References in this document for an up-to-date list of `Status Codes` and their:
        - Description
        - RFC Reference URL
    - Details on each status code through the link
    - Cacheable by default: 200, 203, 204, 206, 300, 301, 404, 405, 410, 414, and 501

        >  Responses with status codes that are defined as cacheable by default (e.g., 200, 203, 204, 206, 300, 301, 404, 405, 410, 414, and 501 in this specification) can be reused by a cache with heuristic expiration unless otherwise indicated by the method definition or explicit cache controls [RFC7234]; all other status codes are not cacheable by default.

- [Response Header Fields](https://tools.ietf.org/html/rfc7231#section-7)
    - detailed index to be aware of if parsing responses

- [HTTP Semantics - Security Considerations](https://tools.ietf.org/html/rfc7231#section-9)
    - be aware of these, read them over


### rfc7232 Highlights

>    This specification defines two forms of metadata that are commonly used to observe resource state and test for preconditions: modification dates (Section 2.2) and opaque entity tags (Section 2.3).  Additional metadata that reflects resource state has been defined by various extensions of HTTP, such as Web Distributed Authoring and Versioning (WebDAV, [RFC4918]), that are beyond the scope of this specification.  A resource metadata value is referred to as a "validator" when it is used within a precondition.
  
- [Header Fields Defined by this RFC](https://tools.ietf.org/html/rfc7232#section-7.2)
    - `ETag`
    - `If-Match`
    - `If-Modified-Since`
    - `If-None-Match`
    - `If-Unmodified-Since`
    - `Last-Modified`
- [Last-Modified Header Field](https://tools.ietf.org/html/rfc7232#section-2.2)
    
    > The "Last-Modified" header field in a response provides a timestamp indicating the date and time at which the origin server believes the selected representation was last modified, as determined at the conclusion of handling the request.

- [ETag == entity-tag](https://tools.ietf.org/html/rfc7232#section-2.3) 
    
    > An entity-tag can be more reliable for validation than a modification date in situations where it is inconvenient to store modification dates, where the one-second resolution of HTTP date values is not sufficient, or where modification dates are not consistently maintained.


### rfc7233 Highlights



### rfc7234 Highlights



### rfc7235 Highlights

- `oauth2/bearer` Authorization is covered in `rfc7235` and its spec resides in [rfc6750](https://tools.ietf.org/html/rfc6749)
    - Note that `oauth2/bearer` aka The OAuth 2.0 Authorization Framework, supercedes [outh rfc6749](https://tools.ietf.org/html/rfc6749).
    - oauth2 `Authorization headers` are very common for `HTTP APIs`, particularly modern `JSON APIs`
- There is a IANA Authentication Scheme Registry in the References of this document.
- `rfc7235` supercedes [rfc2617](https://tools.ietf.org/html/rfc2617). 


### rfc7236 Highlights

This document is a sparse reference to grandfather HTTP Authentication Methods established before the IANA HTTP Authentication Scheme Registry was established.


### rfc7237 Highlights

This document is a sparse reference to grandfather HTTP Methods established in RFCs other than RFC7231 before the IANA HTTP Scheme Registry was established.

### References

- [IANA Authentication Scheme Registry](https://www.iana.org/assignments/http-authschemes/http-authschemes.xhtml)
    - Of note is `oauth2/bearer`
- [IANA HTTP Methods Registry](http://www.iana.org/assignments/http-methods/http-methods.xhtml)
    - table contains:
        - methods
        - if they are safe
        - if they are idempotent
        - current URL to RFC describing the method (many not in rfc7230 or rfc7231
- [IANA Status Code Registry](https://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml)
- [REST in rfc7231: references Fielding 2000 Ch. 5](http://roy.gbiv.com/pubs/dissertation/rest_arch_style.htm)
    - REST: "REpresentational State Transfer" architectural style for distributed hypermedia systems


### Obsolete

- https://tools.ietf.org/html/rfc1945
- https://tools.ietf.org/html/rfc2068
- https://tools.ietf.org/html/rfc2145
- https://tools.ietf.org/html/rfc2616


