# Browsers and Client - Server Communication
## Content
- [Standardization](#standardization)
- [Browser engines](#browser-engines)
- [Internet Basics](#internet-basics)
- [DNS](#dns)
- [Transfer levels and protocols](#transfer-levels-and-protocols)
- [HTTP](#http)
- [Authorization](#authorization)
- [REST](#rest)
- [Websites and deployment process](#websites-and-deployment-process)

## Standardization
<details>
<summary>Learn more</summary>

- [TC39](https://tc39.es/)
- [TC39 - proposals](https://github.com/tc39/proposals)
- [WHATWG](https://whatwg.org/)
- [WHATWG - Standards](https://spec.whatwg.org/)
- [W3C](https://www.w3.org/TR/html52/)
- [W3C - CSS](https://www.w3.org/Style/CSS/)

</details>

## Browser engines

## Internet Basics
<details>
<summary>What is the basic process of publishing a website?</summary>

1. Publish the website (choose the domain name and hosting, link the domain to the web server, deploy the website to the hosting)
2. Enter the website name to the browser
3. Transfer the name to IP via [DNS](#dns)
4. Browser tries to connect to a server using TCP/IP protocol (by default connects to 80/443 port as by default web-server waits browser to connect to this port). Looking for a program via port number (different for client and server): 80 for HTTP or 443 for HTTPS (web server nginx, apache), on complete port closes
  - the port can be changed by the server administrator `https://example.com:3000`
5. After the connection is settled browser forms an HTTP-request and sends it to the server (browserscope.org check the available amount of requests for different browsers)
  - doesn't know about server language
  - 1 file = 1 request (less weight and files = better)
  - web server could have several virtual hosts, get our by site name (domain) (host header in the request)
6. Sending the response (headers and body: html, css, js, media, files)
7. Browser parses the code (according to the specification native to browser)

</details>

<details>
<summary>What is a domain name and how to get it?</summary>

- check if it's free
- domain registering service
- sometimes need a passport to purchase
- if there was ip in the dns settings, links to domain

</details>

<details>
<summary>What is hosting and how to get it?</summary>

- paid or free
- gives an access to the server where the web server runs
- gives a temporary address (site-name.hosting.com)
- link the domain to the web server
- deploy the website to hosting

</details>

<details>
<summary>Learn more</summary>

- [ ] [How Websites Work](https://academind.com/learn/web-dev/how-the-web-works/)
- [How Browsers Work: Behind the scenes of modern web browsers](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)

</details>

## DNS
<details>
<summary>What are the main points about DNS?</summary>

- slow (up to 48 hours to update)
- large
- secure (complex implementation)
- distributed (uses cache)

</details>

## Transfer levels and protocols
<details>
<summary>Where to look for information about a protocol?</summary>

- in the RFC documentation (Request for Comments) 

</details>

<details>
<summary>What is the link/connection layer?</summary>

- cables

</details>

<details>
<summary>What is the internet layer?</summary>

- IP (Internet Protocol) earlier IPv4, new IPv6
- describes the network structure and packets delivery system
- secure delivery is not guaranteed

</details>

<details>
<summary>What is the transport layer?</summary>

- UTP - doesn't wait for the package to be delivered (sound, games, streams, video)
- TCP - waits for the packages (files, used by browsers)
  - lost or discarded packets are resent
  - includes traffic congestion control

</details>

<details>
<summary>What is the application layer?</summary>

- HTTP(S) - HyperText Transfer Protocol (Secure) RFC2616 for the HTTP 1.1
- FTP - File Transfer Protocol
- SMTP - Simple Mail Transfer Protocol
- SSH - Secure Shell - for accessing remote servers (linux)

</details>

<details>
<summary>Learn more</summary>

- [Internet protocol suite](https://en.wikipedia.org/wiki/Internet_protocol_suite)

</details>

## HTTP

<details>
<summary>What is Http?</summary>

- Data transfer protocol - the way computer uses to exchange the information (there are many different protocols, in the web we use http)
- HTTP - hypertext transfer protocol - client exchanges data with the server
- HTTP request is always text

</details>

<details>
<summary>What is the difference between HTTP and HTTPS</summary>

- HTTPS (HyperText Transfer Protocol Secure) is an extension of the HTTP protocol
- the connection established via the HTTPS supports the encoded traffic (the data is encoded, so there is no sense in interception)

</details>

<details>
<summary>What is an HTTP-request?</summary>

```JavaScript
// request string - required
// / - root and the page
GET /contacts.html HTTP/1.1
// headers - optional for ver 1.0 (earlier the proposal was 
// that one IP is one website)
// host is required for ver 1.1+ (when virtual hosts start to be supported)
// to let server find the website we need
// if you don't pass the host header 
// - the website will be default to the server
Host: example.com
User-Agent: Mozilla/5.0
Accept: text/html
// type of the content inside the body
Content-Type: application/json
// size in bytes - tells server that there is body of the length
// so that server doesn't break the connection on default \n\n
Content-Length: 100
// custom headers usually are named with X-
X-Token: secret token
// body - optional (contains the data to send)
{
  "title": "Harry Potter",
  "rating": 5
}
```

</details>

<details>
<summary>What is an HTTP-response?</summary>

- server response = text
```JavaScript
// status line 2 - class, 00 - operation status
HTTP/1.1 200 OK
// headers - if client doesn't know about one of the headers
// such header will be ignored
Cache-Control: max-age=604800
Content-Type: text/html
Date: Tue, 24 Oct 2017 11:08:24 GMT
Etag: "359670651+ident"
Expires: Tue, 30 Oct 2017 11:08:24 GMT
Last-Modified: Fri, 09 Aug 2016 23:23:35 GMT
Server: ECS (dcs/53DB)
Vary: Accept-Encoding
// custom headers start with X-
X-Cache: HIT
Content-Length: 1270
// response body
<!doctype html>
<html>
  <head></head>
  <body></body>
</html>
```

</details>

<details>
<summary>What are the main method types of an http request?</summary>

- read
  - HEAD - get only headers (ex: to the check if the info has been updated or we can worked with cache)
  - OPTIONS - to check which requests we can send to the resource (ex: img supports `GET` and `HEAD`, user-name also supports `POST` and `PUT`)
  - GET - get the information from the server
- write
  - POST - create a new record (body is required)
  - PUT - to fully rewrite the existing record
  - PATCH - to partially update the existing record
  - DELETE - to delete the record

</details>

<details>
<summary>What are the main 5 status classes of the HTTP-response?</summary>

- 1 informational
- 2 success (phrase reason: 200 OK, 201 Created)
- 3 redirection
- 4 client error
- 5 server error

</details>

## Authorization
<details>
<summary>What is the purpose of the authorization?</summary>

- restricts the access for different users

</details>

<details>
<summary>What are the ways to identify the user?</summary>

- Identification - tell the site who you are
- Authentication - (authentic - true, genuine) the confirmation that you are who you state you are
- Authorization - check if you are allowed to get access to some parts of the website or webapp

</details>

<details>
<summary>What is the authorization order?</summary>

1. Identification - user enters login and password
2. Authentication - server checks if the login and password are correct and gives a token (access to the web app, often holds the rules and never stores open)
3. Authorization - you give the token to the server and the server decides whether to give you an access or not
  - 200 - success, allowed
  - 401 - unauthorized
  - 403 - not enough rights

</details>

<details>
<summary>What is the basic authentication (provided by HTTP protocol)?</summary>

- used to restrict access to some pages for unauthorized users
- browser shows a modal window to enter the login and password
- if wrong = server returns 401 Unauthorized
- browser gives you the opportunity to enter the login and password several times
```JavaScript
// request
// when user enters the data, the browser sends
// this request to the server
GET /secret HTTP/1.1
Host: example.com
// Basic - for basic authentication
// YWRtaW46MTIzNDU2 - encoded login and password (admin:123456)
// base64 - standard encodes binary data with 64 ASCII symbols
Authorization: Basic YWRtaW46MTIzNDU2

// response
// 401 and special header are required
// for browser to show the modal
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Basic realm="Protected server"
```

</details>

## REST
<details>
<summary>What is REST?</summary>

- Representational State Transfer - a set of rules for client-server communication (working with data - CRUD system)

</details>

<details>
<summary>What is CRUD?</summary>

- Create, Read, Update, Delete - a set of methods to work with data

</details>

<details>
<summary>How to 'translate' CRUD into HTTP terms?</summary>

- Create - `POST`
- Read - `GET`
- Update - `PUT` or `PATCH`
- Delete - `DELETE`

</details>

<details>
<summary>What is the REST implementation?</summary>

- every resource on the server has it's own address and CRUD methods it supports
```JavaScript
// to create a comment
POST /comments

// to get a comment /comments/:id
GET /comments/1

// to update the comment
PUT /comments/1
PATCH /comments/1

// to delete a comment
DELETE /comments/1
```

</details>

<details>
<summary>How to get a set of available addresses for sending a request?</summary>

- ask a backend developer
- read the API docs
- write it (light backend) - usually Node.js is used - the only purpose of this thing is to deal with client requests and send them further to the server (where there is the logic which works with database)

</details>

## Websites and deployment process
<details>
<summary>What are the types of websites?</summary>

- Static (just HTML, CSS, JS)
- SPA (HTML, CSS, JS with only one HTML page being served, client-side JS is used to re-render the page dynamically)
- Dynamic (SSR) Web Apps (HTML pages are created dynamically on the server via template engines like EJS)

</details>

<details>
<summary>What is the deployment process in general?</summary>

1. write the code
2. test the code
3. optimise the code
4. build for production
5. deploy depending on the type of website
  - static host - doesn't execute the server-side code: AWS S3, Firebase Hosting, etc
  - dynamic host - can execute the server-side code: AWS Elastic, Heroku, etc

</details>

<details>
<summary>Learn more</summary>

- [ ] [Dynamic vs Static vs SPA](https://academind.com/learn/web-dev/dynamic-vs-static-vs-spa/)
- [ ] [Firebase hosting docs](https://firebase.google.com/docs/hosting)
- [ ] [Heroku docs](https://devcenter.heroku.com/categories/reference)

</details>