## Swoole Server

### Listening On Multiple Ports

The swoole supports listening on multiple ports and analyzing multiple protocols.

You can set different protocols and callback functions on different ports. SSL/TLS can also enabled on certain port.

- If the listening on new port does not have protocol set, it will be in the no protocol mode.

- If the listening on new port does not have the callback functions set, it will use the callback functions of `$server`.

- The return of `$server->listen` is object of `swoole_server_port`

- The callback functions set for different ports still run in same worker process.

#### Listen on new port

```php
$port1 = $server->listen("127.0.0.1", 9501, SWOOLE_SOCK_TCP);
$port2 = $server->listen("127.0.0.1", 9502, SWOOLE_SOCK_UDP);
$port3 = $server->listen("127.0.0.1", 9503, SWOOLE_SOCK_TCP | SWOOLE_SSL);
```

#### Set protocol
```php
$port1->set([
    'open_length_check' => true,
    'package_length_type' => 'N',
    'package_length_offset' => 0,
    'package_max_length' => 800000,
]);

$port3->set([
    'open_eof_split' => true,
    'package_eof' => "\r\n",
    'ssl_cert_file' => 'ssl.cert',
    'ssl_key_file' => 'ssl.key',
]);
```

#### Set callback functions of events
```php
$port1->on('connect', function ($serv, $fd){
    echo "Client:Connect.\n";
});

$port1->on('receive', function ($serv, $fd, $from_id, $data) {
    $serv->send($fd, 'Swoole: '.$data);
    $serv->close($fd);
});

$port1->on('close', function ($serv, $fd) {
    echo "Client: Close.\n";
});

$port2->on('packet', function ($serv, $data, $addr) {
    var_dump($data, $addr);
})
```

#### Optional configurations for swoole_server_port object

The swoole_server_port object can only set part of [the configurations list of swoole_server](/modules/swoole-server/configuration.md)

- If the swoole_server_port object hasn't set any configuration, it will use the configurations of the main swoole server object.

- If the main server object is instance of `swoole_http_server` or `swoole_websocket_server` and the swoole_server_port object hasn't been set the configuration about protocol, the swoole_server_port is set to analyze `http` or `websocket` protocol automatically and the custom callback function of event `receive` can not be set.

- If the main server object is instance of `swoole_http_server` or `swoole_websocket_server` and the swoole_server_port object has been set some custom configurations, the swoole_server_port object would change to analyze TCP protocol. If you still want to set the swoole_server_port object to analyze the `Http/WebSocket` protocol, it needs to add `open_http_protocol => true` or `open_websocket_protocol => true`

Available Configurations for swoole_server_port object:

- socket configurations, for example, backlog, TCP_KEEPALIVE, open_tcp_nodelay, tcp_defer_accept, etc

- protocol configurations, for example, open_length_check, open_eof_check, package_length_type, etc

- ssl configurations, for example, ssl_cert_file、ssl_key_file, etc

Unavailable Configurations for swoole_server_port object:

- worker_num, task_worker_num, reactor_num

- dispatch_mode, task_ipc_num

- heartbeart_check

- log_file

- user, group, chroot

- open_cpu_affinity

- max_request, task_max_request

#### Optional callback functions for swoole_server_port object

The swoole_server_port object can only set part of [the callback functions of swoole_server](/modules/swoole-server/callback-functions.md)

For TCP server:

- onConnect

- onClose

- onReceive

For UDP server:

- onPacket

- onReceive

The below callback functions can only be set by swoole_server object.

- onStart

- onShutdown

- onWorkerStart

- onWorkerStop

- onManagerStart

- onManagerStop

- onTask

- onFinish

- onPipeMessage

- onWorkerError

#### Q&A

The `swoole_http_server` class and `swoole_websocket_server` class inherit the `swoole_server` class. The swoole_server object can't call `listen` method to create swoole_server_port object of Http or Websocket server.

In this situation, you can create the swoole_http_server object and then call `listen` method to create tcp server.

```php
$http_server=new swoole_http_server('0.0.0.0',9998);
$http_server->set(array('xxx'=>'yyy'));
$http_server->on('request','request');
$tcp_server=$http_server->addListener('0.0.0.0',9999,SWOOLE_SOCK_TCP);
```
