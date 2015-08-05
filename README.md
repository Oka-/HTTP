# HTTP

HTTP is a super lightweight interface for making asynchronous requests, with chained methods.

Intended for simple usage in modern browsers.

## Example

```JavaScript
HTTP.POST('/some/endpoint/somewhere')
  .set('Content-Type', 'application/xml')
  .mime('text/plain')
  .cred()
  .data({one: 1})
  .then(function (response, status, request) {
    console.log(response, status.request);
  });
```

## Usage

The chain begins with the `HTTP` function, or one of it's methods. This returns an `io` object with all the chainable methods.

- `HTTP(method, url)`
- `HTTP.DELETE(url)`
- `HTTP.GET(url)`
- `HTTP.HEAD(url)`
- `HTTP.OPTIONS(url)`
- `HTTP.POST(url)`
- `HTTP.PUT(url)`

The named methods are equivalent to passing the method name to the main function.

Passing only a single parameter that isn't a method string, will result in a default `GET` request, and the first parameter used as the `url`.

The following are all equivalent.

```JavaScript
HTTP('/my/endpoint.json')
HTTP('GET', '/my/endpoint.json')
HTTP.GET('/my/endpoint.json')
```

You get the idea.

Passing the wrong method string, that isn't a `url`, will result in total chaos. Try to avoid that.

The chainable methods provided on the `io` object are as follows:

`.cred()`

- Sets the `withCredentials` property on the `XMLHttpRequest` object to `true`.

`.do(fn([response[, status[, request]]))`

- Acts immediately upon the `XMLHttpRequest` object.
- Can be used to further customize the request.
- Can be used after the fact if a reference to the `io` object is kept.
- `this` context in `fn` set to the `XMLHttpRequest` object.

`.set(header, value)`

-  Sets or combines a header.

`.data(data)`

- Provides data to be sent.

`.mime(type)`

- Overrides response `mimeType`.

`.then(fn([response[, status[, request]]))`
- Adds a callback function to the list of callbacks to be invoked when the response loads.
- Callbacks are invoked in the order they are added.
- `this` context in `fn` set to the `XMLHttpRequest` object.


The request is sent when the chain ends.

Additionally, `HTTP.delay([time])` returns the internal chain delay. Can be passed a `time` (ms) parameter to change the timing.

## Support

Requires

- `XMLHttpRequest`
- `EventTarget.addEventListener`

and other ES5 standards. Check your compatibility tables.

Look elsewhere for `ActiveXObject` legacy support.

---

Have fun.

Colin Hall-Coates < [yo@oka.io](mailto:yo@oka.io) >

[@Okahyphen](https://twitter.com/Okahyphen)
