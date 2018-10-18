# Swoole WebSocket server

The following PHP codes shows how to write a simple WebSocket server. The WebSocket server sends the client a message when the WebSocket connection is established.

The `swoole_websocket_server` class inherits from the class `swoole_server`.

## Example Code

``` php
<?php
$server = new swoole_websocket_server("127.0.0.1", 9501);

$server->on('open', function (swoole_websocket_server $server, $request) {
    echo "server: handshake success with fd{$request->fd}\n";
});

$server->on('message', function (swoole_websocket_server $server, $frame) {
    echo "receive from {$frame->fd}:{$frame->data},opcode:{$frame->opcode},fin:{$frame->finish}\n";
    $server->push($frame->fd, "This message is from swoole websocket server.");
});

$server->on('close', function ($ser, $fd) {
    echo "client {$fd} closed\n";
});

$server->start();
```

## Table of Contents

* [Events And Callback Functions](/modules/swoole-websocket-server/events-callbacks.md)

* [Methods List](/modules/swoole-websocket-server/methods.md)

* [Predefined Contants](/modules/swoole-websocket-server/constants.md)

* [Common Problems](/modules/swoole-websocket-server/common-problems.md)

> If the swoole_websocket_server has been set the callback function of event `request`, it can be used as Http server.

> If the swoole_websocket_server hasn't been set the callback function of event `request` and received http request, it would repond http 400 error.
