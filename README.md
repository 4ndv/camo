# camo

Fork of [GitHub's camo](https://github.com/atmos/camo), but without HMAC signatures and hexencoding urls.

[![Deploy to Heroku](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/4ndv/camo)

Features
--------

* Max size for proxied images
* Follow redirects to a certain depth
* Restricts proxied images content-types to a whitelist
* Forward images regardless of HTTP status code

## URL Formats

Camo supports two URL formats:

    http://example.org/camo?url=<image-url>
    http://example.org/camo/<image-url>

## Configuration

Camo is configured through environment variables.

* `PORT`: The port number Camo should listen on. (default: 8081)
* `CAMO_HEADER_VIA`: The string for Camo to include in the `Via` and `User-Agent` headers it sends in requests to origin servers. (default: `Camo Asset Proxy <version>`)
* `CAMO_LENGTH_LIMIT`: The maximum `Content-Length` Camo will proxy. (default: 5242880)
* `CAMO_LOGGING_ENABLED`: The logging level used for reporting debug or error information. Options are `debug` and `disabled`. (default: `disabled`)
* `CAMO_MAX_REDIRECTS`: The maximum number of redirects Camo will follow while fetching an image. (default: 4)
* `CAMO_SOCKET_TIMEOUT`: The maximum number of seconds Camo will wait before giving up on fetching an image. (default: 10)
* `CAMO_TIMING_ALLOW_ORIGIN`: The string for Camo to include in the [`Timing-Allow-Origin` header](http://www.w3.org/TR/resource-timing/#cross-origin-resources) it sends in responses to clients. The header is omitted if this environment variable is not set. (default: not set)
* `CAMO_HOSTNAME`: The `Camo-Host` header value that Camo will send. (default: `unknown`)
* `CAMO_KEEP_ALIVE`: Whether or not to enable keep-alive session. (default: `false`)

## Testing Functionality

### Bundle Everything

    % rake bundle

### Start the server

    % coffee server.coffee

### In another shell

    % rake

### Debugging

To see the full URL restclient is hitting etc, try this.

    % RESTCLIENT_LOG=stdout rake

### Deployment

You should run this on heroku.

To enable useful line numbers in stacktraces you probably want to compile the server.coffee file to native javascript when deploying.

    % coffee -c server.coffee
    % /usr/bin/env PORT=9090 node server.js

### Docker

A `Dockerfile` is included, you can build and run it with:

```bash
docker build -t camo .
docker run -t camo
```
