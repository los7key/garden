---
layout: post
title: HTTP Interaction  
description: HTTP Interaction
date: 2022-07-20
Last Updated: 
---
## Introduction
The topic of HTTP and what happens after pressing "Enter" on the keyboard came up recently during an interview.  There are a few steps (depending on how in depth we want to go) and it seemed like it was time for a refresher.  This assumes some basic level of networking and understanding of the internet.

## Steps of a simple HTTP transaction

1. **DNS lookup** - Client attempts to resolve the domain name for the request
    1. Client sends DNS Query to local ISP DNS server
    2. DNS server responds with the IP address for domain.com

2. **Connect** - Client establishes TCP connection with the IP address of domain.com
    1. A web server listens for connection requests on a socket bound to a port[^1] 
    2. Client sends a SYN packet to the web server
    3. Web server sends SYN-ACK packet back to client 
    4. Client answers with ACK packet[^2]

3. **Send** - Client sends the HTTP request to the web server

4. **Wait** - Client waits for a response from the web server
    1. Web server processes the request and sends the response back to the client
    2. Web server sends the first byte containing the HTTP headers and then content

5. **Load** - Client loads content sent by Web server

6. **Close** - Client sends a a FIN packet to close the TCP connection

## Body of a Request
The main ingredients of an HTTP request includes the following:


| Name      |   Example         | Requirement |
| ---       |   ---             | ---         |
| Method    | GET, POST, PUT    | Yes         |
| Host      | www.domain.com    | Yes         |
| Path      | /index.html       | Yes         |
| HTTP version | HTTP/1.1       | Yes         |
| Headers | Content-Type: application/json | No |
| Body | Hello world    | No  |

## The request
The request sent to the web browser from the client:

```
GET /index.html HTTP/1.1 <-- Method, Path, HTTP version
Host: www.domain.com     <-- URL of web server
User-Agent: curl/7.68.0  <-- Browser version
Accept: */*              <-- Tells web server that any type of response is okay
```

## The response
The response from the web server should look similar to below:

```
HTTP/1.1 200 OK
Date: Mon, 04 Jul 2022 15:37:37 GMT
Server: Apache
Last-Modified: Sun, 03 Jul 2022 06:13:43 GMT
Transfer-Encoding: chunked
Connection: Keep-Alive
Content-Type: text/html; charset=UTF-8

(Webpage Content)
```

## What is that HTTPS?
We can't talk HTTP without HTTPS.  Let's not forget, HTTP is inherently insecure and data can be intercepted in clear text!  This is where HTTPS comes in.  HTTPS is the secured HTTP protocol required to send and receive information securely over internet. In this day and age it is mandatory for all websites to have HTTPS protocol to have secured websites because most modern day web browsers will throw an error or refuse to connect to an insecure website. 

Aside from security and encryption, the communication structure of HTTPS protocol remains the same as HTTP protocol outlined above.


[^1]: Web servers typically listen on port 80 (HTTP) and/or 443 (HTTPS).  Any port can be used as long as the web server is listening on a port the client knows about.
[^2]: This is the completion of the three-way TCP handshake