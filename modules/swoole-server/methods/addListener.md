## Method

### swoole_server->addListener

#### Prototype

```php
mixed swoole_server->addListener(string $host, int $port, $type = SWOOLE_SOCK_TCP);
```

#### Illustration

Add more listening IP or port for the server. The connection information can be acccessed by `$server->connection_info()` when the server has started. By the connection information, you can distinguish the source port of the connection.

#### Parameter

* `$host`: the ip address of the server
* `$port`: the port of the server
    - it needs root privileges if the port is litte than 1024
    - the parameter `$port` will be ignored when the parameter `$sock_type` is set to `SWOOLE_UNIX_DGRAM` or `SWOOLE_UNIX_STREAM`
    - if the parameter `$port` is set to `0`, the swoole server would use a random and available port

* `$sock_type`: the socket type of the server:
    * SWOOLE_SOCK_TCP: TCP
    * SWOOLE_SOCK_TCP6: TCP IPv6
    * SWOOLE_SOCK_UDP: UDP
    * SWOOLE_SOCK_UDP6: UDP IPv6
    * SWOOLE_UNIX_DGRAM: Unix socket dgram
    * SWOOLE_UNIX_STREAM: Unix socket stream
* Enable SSL: `$sock_type | SWOOLE_SSL`. To enable ssl, it must set [the configuration about ssl](/modules/swoole-server/configuration.md).

#### Return

The swoole_server_port object

#### Example

``` php
<?php
$server->addlistener("127.0.0.1", 9502, SWOOLE_SOCK_TCP);
$server->addlistener("192.168.1.100", 9503, SWOOLE_SOCK_TCP);
$server->addlistener("0.0.0.0", 9504, SWOOLE_SOCK_UDP);
//UnixSocket Stream
$server->addlistener("/var/run/myserv.sock", 0, SWOOLE_UNIX_STREAM);
//TCP + SSL
$server->addlistener("127.0.0.1", 9502, SWOOLE_SOCK_TCP | SWOOLE_SSL);
//Listen on a random port
$port = $server->addListener("0.0.0.0", 0, SWOOLE_SOCK_TCP);
echo $port->port;
```
