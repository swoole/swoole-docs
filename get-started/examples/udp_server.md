## Create UDP Server

### Code example

`udp_server.php`

``` php
// Create the server object which listens at 127.0.0.1:9502. Set the server type to SWOOLE_SOCK_UDP
$server = new swoole_server("127.0.0.1", 9502, SWOOLE_PROCESS, SWOOLE_SOCK_UDP);

// Register callback function for the event `receive data`
$server->on('Packet', function($server, $data, $clientInfo){
    $server->sendto($clientInfo['address'], $clientInfo['port'], "Server : " . $data);
});

// Start the server
$server->start();
```

As UDP server, it is unlike TCP server and hasn't the concept of connection. When the UDP server has started, the client can send directly the data to the ip address and port which the server listens at. Then the UDP server will call the function registered for receiving packet.

- `$clientInfo` is the information of client. It is a array which contains the ip address and port of client.

- Calling the `$server->sendto($ip, $port, $data)` to send data to client


### Run program 

``` bash
php udp_server.php
```
You can use `netcat -u` to test.

``` bash
netcat -u 127.0.0.1 9502 
hello
Server : hello
```
