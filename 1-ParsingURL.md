# Parsing the URL

_Context: Browser needs to determine what needs to be fetched and where that resource is hosted._

_OSI Layer(s): 7_

![URL](./ref/ref2.png)

``protocol://host:port/path?query``

The browser now has the following information from the URL ([Uniform Resource Locator](https://tools.ietf.org/html/rfc1738)):

### Protocol

![proto](./ref/refProto.png)

Is this HTTP/S or some other protocol (ftp://, gopher://, smb://, etc)?

### Host

![path](./ref/refHost.png)

What is the host that holds the resource?

### Path

![resource](./ref/refPath.png)

What is the path the resource we are attempting to locate?

### Query Parameters

![query](./ref/refQuery.png)

Are there query parameters that should be passed to the responding web server?

### Convert non-ASCII Unicode characters in hostname

* The browser checks the hostname for characters that are not in `a-z`,
  `A-Z`, `0-9`, `-`, or `.`.

* Since the hostname is `google.com` there won't be any, but if there were the browser would apply [Punycode](https://en.wikipedia.org/wiki/Punycode) encoding to the hostname portion of the URL.

_Demonstration Step:_
* Make an HTTP request to ``Þingvellir.is`` (notice the "thorn" letter.). Copy/Paste the URL after loading the page.
* Find the GET request in Wireshark. Show the request line and the ``Host`` header the browser sent.

[Next: Checking the HSTS list](./2-CheckingHSTS.md)