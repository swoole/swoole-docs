## Method

### swoole_server::__construct 

#### Prototype

``` php
swoole_server::__construct(string $host, int $port = 0, int $mode = SWOOLE_PROCESS, int $sock_type = SWOOLE_SOCK_TCP);
```
#### Illustration

Construct a swoole server object

#### Parameter

* `$host`: the ip address of the server
* `$port`: the port of the server (it needs root privileges if the port is litte than 1024)
* `$mode`: the running mode of the server:
    * SWOOLE_PROCESS: multiple process mode, the business logic is running in child processes, the default running mode of server
    * SWOOLE_BASE: reactor based mode, the business logic is running in the reactor
* `$sock_type`: the socket type of the server:
    * SWOOLE_SOCK_TCP: TCP
    * SWOOLE_SOCK_TCP6: TCP IPv6
    * SWOOLE_SOCK_UDP: UDP
    * SWOOLE_SOCK_UDP6: UDP IPv6
    * SWOOLE_UNIX_DGRAM: Unix socket dgram
    * SWOOLE_UNIX_STREAM: Unix socket stream
* Enable SSL: `$sock_type | SWOOLE_SSL`. To enable ssl, it must set [the configuration about ssl](/modules/swoole-server/configuration.md).

#### Return

the swoole_server object

#### Example:

##### Listen on a random port:

The swoole supports the feature of listening on a random port. When the argument `$port` isn't seted or is `0`, the swoole will choose a random and available port to listen on. You can use `$server->port` to listen on. 

``` php
<?php
$http = new swoole_http_server("127.0.0.1");

$http->on('request', function ($request, $response) {
    $response->header("Content-Type", "text/html; charset=utf-8");
    $response->end("<h1>Hello Swoole. #".rand(1000, 9999)."</h1>");
});

$http->start();
```
##### Listen on a port defined in systemd

The swoole-1.9.7 adds the support for `systemd socket`. The port listened on can be setted by the configuration of systemd.

`swoole.socket`
``` bash
[Unit]
Description=Swoole Socket

[Socket]
ListenStream=9501
Accept=false
[Install]
WantedBy = sockets.target
```

`swoole.service`
``` bash
[Service]
Type=forking
PIDFile=/var/run/swoole.pid
ExecStart=/usr/bin/php /var/www/swoole/server.php
ExecStop=/bin/kill $MAINPID
ExecReload=/bin/kill -USR1 $MAINPID

[Install]
WantedBy = multi-user.target
```

`server.php`
``` php
$http = new swoole_http_server("systemd");

$http->set([
    'daemonize' => true,
    'pid_file' => '/var/run/swoole.pid',
]);

$http->on('request', function ($request, $response) {
    $response->header("Content-Type", "text/html; charset=utf-8");
    $response->end("<h1>Hello Swoole. #".rand(1000, 9999)."</h1>");
});

$http->start();
```

`Start the systemd service`

``` bash
sudo systemctl enable swoole.socket
sudo systemctl start swoole.socket
sudo systemctl start swoole.service
```
