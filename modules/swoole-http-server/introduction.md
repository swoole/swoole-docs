# Swoole HTTP server

With 5 lines of code, you can write an Async non-blocking IO, multiple process HTTP server.

The `swoole_http_server` class inherits from the class `swoole_server`. It is a complete implementation of http server.

## Example code

``` php
<?php 
$http = new swoole_http_server("127.0.0.1", 9501);

$http->on('request', function ($request, $response) {
    $response->end("<h1>Hello World. #".rand(1000, 9999)."</h1>");
});

$http->start();
```

> swoole_http_server does not support the complete HTTP protocol, Nginx is recommended to be used as a proxy for Swoole HTTP server.

## Table of Contents

* [Methods And Properties List](/modules/swoole-http-server/methods_properties.md)

* [Configurations List](/modules/swoole-http-server/configuration.md)

* [Common Problems](/modules/swoole-http-server/common-problems.md)

## Performance

Compare with PHP-FPM, the default Golang HTTP server, the default Node.js HTTP server, Swoole HTTP server performs much better. It has the similar performance compare with the Nginx static files server. 

The experiment is done with benchmark tool Apache bench, on a normal PC server with Inter Core-I5 4 core CPU, 8GB memory. Swoole HTTP server hits 110K request per second.

``` bash
ab -c 200 -n 200000 -k http://127.0.0.1:9501
```
## HTTP2 protocol support

Swoole HTTP server supports HTTP2 protocol thanks to *nghttp2* library. Openssl is required for HTTP2 protocol and the openssl has to support TLS1.2, ALPN and NPN. 

PHP extension compile configuration:

``` bash
./configure --enable-openssl --enable-http2
```

## Swoole HTTP server configuration:

``` bash
// Enable SSL
$server = new swoole_http_server("127.0.0.1", 9501, SWOOLE_PROCESS, SWOOLE_SOCK_TCP | SWOOLE_SSL);
// setup the location of ssl cert files and key files
$server->set([
    'ssl_cert_file' => $ssl_dir . '/ssl.crt',
    'ssl_key_file' => $ssl_dir . '/ssl.key',
    'open_http2_protocol' => true, // Enable HTTP2 protocol
]);
```

## Nginx configuration:

``` text
server {
    root /data/wwwroot/;
    server_name localhost;

    location / {
        try_files $uri @swoole;
    }
    location @swoole {
        proxy_pass http://127.0.0.1:9501;
        proxy_http_version 1.1;
        proxy_set_header Connection "keep-alive";
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header Host            $host;
    }
}

```
