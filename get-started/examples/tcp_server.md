## Create TCP Server

### Code example

`server.php`

``` php
// Create the server object and listen 127.0.0.1:9501
$server = new swoole_server("127.0.0.1", 9501);

// Register the function for the event `connect`
$server->on('connect', function($server, $fd){
    echo "Client : Connect.\n";
});

// Register the function for the event `receive`
$server->on('receive', function($server, $fd, $from_id, $data){
    $server->send($fd, "Server: " . $data);
});

// Register the function for the event `close`
$server->on('close', function($server, $fd){
    echo "Client: {$fd} close.\n";
});

// Start the server
$server->start();
```
The code above creates a TCP server, and listens the 127.0.0.1:9501. It implements a simple echo tcp server. When the client connects to this server and sends a string 'hello', the server will respond with a string 'Server: hello'.

The class `swoole_server` creates an async server by registering the events listening functions. When an event happens, the internal of swoole will call the corresponding function which is registered for this event. 

For example, if a tcp connection comes and connects to the tcp server, the swoole will call the function which is registered for event `connect`. If a tcp client sends data to the tcp server, the swoole will recevice the data and call the corresponding function to handle this event. 

- The server can be connected by thousands of client at the same time and `$fd` is the unique identifier of client.

- When calling `$server->send($fd, $data)` to send data to client, `$fd` stands for the client.

- When calling `$server->close($fd)`, the connection between the client `$fd` and the server will be closed and the server will call the function registered for event `close`.

- When the client closes the connection proactively, the server will call the function registered for event `close`.

### Run program

``` bash
php server.php
```

Run the server file in command line. You can use the `netstat` to check which process is listening the 9501 port. 

`sudo netstat -nlp |awk '/9501/'`

Use the `telnet` or `netcat` tool to connect the server.
``` bash
telnet 127.0.0.1 9501
hello
Server: hello
```

### Q&A

#### Fail to connect the server

There are some ways to check this problem:

- Run `sudo netstat -nlp | grep 9501` to check if the 9501 has been listened

- If there is no problem after the above check, check the firewall of operating system.

- Pay attention to the ip address the server listens. The client should connect the same ip address
