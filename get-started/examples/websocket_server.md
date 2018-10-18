## Create Websocket Server

### Code example

`websocket_server.php`

``` php
//Create the websocket server object
$websocket_server = new swoole_websocket_server("0.0.0.0", 9502);

// Register function of the opening connection event
$websocket_server->on('open', function($websocket_server, $request){
    var_dump($request->fd, $request->get, $request->server);
    $websocket_server->push($request->fd, "Hello welcome\n");
});

// Register function of the receiving message event
$websocket_server->on('message', function($websocket_server, $frame){
    echo "Message : {$frame->data}\n";
    $websocket_server->push($frame->fd, "Server : {$frame->data}");
});

// Register function of the close event
$websocket_server->on('close', function($websocket_server, $fd){
    echo "client_{$fd} is closed\n";
});

// Start the server
$websocket_server->start();
```

Websocket server is based on the http server. The client will first send a handshake request to start the WebSockrt handshake process. If the process of handshake successed, the swoole would call the function registered for event `open` and get the `$request` object. The `$request` object contains the information of GET, Cookie and Http headers.

Once the connection has been set, the client and the server can make the interactive communication.

- The onMessage function will be called when the client send data to the server

- The server uses `$websocket_server->push($fd, $data)` to send data to the client

- The server is able to register the function for event `handshake` to handle the handshake

### Run program

``` bash
php websocket_server.php
```
In the browser, js code is below:
``` javascript
var wsServer = 'ws://127.0.0.1:9502';
var websocket = new WebSocket(wsServer);
websocket.onopen = function (evt) {
    console.log("Connected to WebSocket server.");
};

websocket.onclose = function (evt) {
    console.log("Disconnected");
};

websocket.onmessage = function (evt) {
    console.log('Retrieved data from server: ' + evt.data);
};

websocket.onerror = function (evt, e) {
    console.log('Error occured: ' + evt.data);
};

```
