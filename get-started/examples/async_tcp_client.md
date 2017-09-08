## Create Async TCP Client

### Code example

`async_tcp_client.php`

``` php
// Create the asynchronous tcp client object
$client = new swoole_client(SWOOLE_SOCK_TCP, SWOOLE_SOCK_ASYNC);

// Register the function for the event of connecting server
$client->on("connect", function($client){
	$client->send("Hello World");
});

// Register the function for the event of receiving data from server
$client->on("receive", function($client, $data){
	echo "Received :" . $data . "\n";
})

// Register the function for the event of error
$client->on("error", function($client){
	echo "Connect failed";
})

// Register the function for the event of closing connection
$client->on("close", function($client){
	echo "Connection close\n";
});

// Start to connect to the server
$client->connect("127.0.0.1", 9501, 0.5);
```

This tcp client is asynchronous and non-blocking and is used for high concurrency program. The `redis-async` and `mysql-async` provided by swoole is based on this tcp client.

It needs to register functions for the events. There are four events which must be setted. 

- the event of connecting which is triggered when the client connects the server successfully
- the event of error which is triggered when the client fails to connect the server
- the event of receiving data which is triggered when the client receives data from the server
- the event of close which is triggered when the connection between the client and the server is closed

`$client->connect` returns immediately. When some event is triggered, the swoole would call the corresponding function registered for the event.


### Run program

``` bash
php async_tcp_client.php
```
