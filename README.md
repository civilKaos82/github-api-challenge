# Github API Client

HTTP is handy for browsers and HTML, but the protocol itself is used with many different kinds of tools. For example, Github's entire API is exposed as HTTP, and instead of sending text back and forth Github sends JSON. At Devbootcamp we build all kinds of tools that use Github's API to help us administer challenges — that's all happening over the command line from HTTP.

We're going to build a tool that uses Github's API. Let's use Ruby's built in HTTP client — [Net::HTTP](http://www.ruby-doc.org/stdlib-2.1.3/libdoc/net/http/rdoc/Net/HTTP.html), no need to re-invent the wheel.

## Release 1, Hello Emoji

Produce a simple command-line app that contacts [Github's API](https://developer.github.com/v3/) (check under Miscellaneous) in Ruby and prints out a list of every Emoji it supports. It should look something like this:

```
$ ./emojis
888 Emojis:
 - 100
 - 1234
 - +1
 - -1
 - 8ball
 - a
 - ab
 - abc
 - abcd
 - accept
 - aerial_tramway
 [... snip ...]
```

You can use `curl` to hit a Github API endpoint first just to see what it sends back, but you should use Net::HTTP in Ruby to get the job done in your script.

## Release 2, Authenticate
Github aggressively rate-limits the number of requests we can make to their HTTP servers if we are not authenticated (only 60 reqs/hr), and those request are shared by everyone on the network. We'll run out of requests in no time as you test your code, so we need to start passing our credentials. Authenticated request have a cap of 5000 reqs/hr — that should be enough.

You already know about request and response headers from our work on the HTTP server challenge. One of the first additions to your github client should be the [Authorization header](https://developer.github.com/v3/#authentication).

You can [generate](https://github.com/settings/applications) an OAuth token for yourself to use in authentication, Github calls this a "Personal Access Token." You'll pass that token in the Authorization header to let Github know the request is coming from you (the user). The [docs](https://developer.github.com/v3/#authentication) have an example of that header (see the `curl -h` example).

Test your authentication by accessing the `/user` resource. If you are authenticated correctly, you should get back some information about yourself. If you're getting a `401` or `403` response from the server it means something is going wrong with authentication.

## Release 3, Github CLI Profile

You know how to access the Github API in Ruby, and you know how to send authenticated requests. Now produce a tool that prints out a simple Github profile summary given a person's Github user name:

```
$./ruby-profile mattbaker
Name: Matt Baker
Location: Chicago, IL
Public Repos: 15

 * Arrhythmia
 * divvyviz
 * is-lucas-home-yet
 * mattbaker.github.com
 * matasano-crypto-challenges
 * Reactive.js
 * ruby-heap-viz
 * ruby-tar-pit
 * swift-funsets
 * websocket-pipe
```
