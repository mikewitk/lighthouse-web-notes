# HyperText

HT = HyperText (HTTP, HTML)


## URL

URL = Uniform Resource Locator

A URL is composed of different parts, some mandatory and others optional

`http://www.example.com:80/path/to/myfile.html?key1=value1&key2=value2#SomewhereInTheDocument`

`http` : protocol. A set method for exchanging or transferring data around a computer network.
        examples: http, https, mailto, ftp

`www.example.com` : domain name. It indicates which Web server is being requested.

`:80` : port. It indicates the technical gate used to access the resources on the web server. It is usually ommited if the web server uses the standard ports (80 for HTTP and 443 for HTTPS)

`/path/tp/my/file.html` : path to the file.

`?key1=value1&key2=value2` : parameters. The web server can use those parameters to do extra stuff before returning the resource.

`#SomewhereInTheDocument` : anchor. Represents a sort of "bookmark" inside the resource.


## Headers

Every HTTP request and response consists of a *header* and a *body*.
*Header*: content of the request/response
*Body*: additional info (metadata, addressing info, cookies, etc)

## HTTP

Web Server: is just a computer program that listens for requests from browsers and then execute them.

It's worth noting that HTTP only defines what the browser and web server say to each other, not how they communicate.

