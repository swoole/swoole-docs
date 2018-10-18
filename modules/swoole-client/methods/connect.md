# Swoole TCP/UDP client

## Methods

### swoole_client->connect

#### Prototype

```php
bool swoole_client->connect(string $host, int $port, float $timeout = 0.1, int $flag = 0)
```

#### Illustration

Connect to the remote TCP/UDP port.

#### Parameter

* `$host`	  the ip address the client connects to
* `$port`     the port the client connects to
* `$timeout`  the timeout(second) of connect/send/recv, the dafault value is 0.1s
* `$flag`     if the type of client is UDP, the `$flag` means if to enable the configuration `udp_connect`. If the configuration `udp_connect` is enabled, the client will only receive the data from specified `ip:port`. If the type of client is TCP and the `$flag` is set to `1`, it must use `swoole_client_select` to check the connection status before `send/recv`.

> `$timeout` is noneffective for asynchronous client.

#### Return

##### Synchronous mode

This method won't return until the client connects to the server successfully or unsuccessfully.

```php
if ($cli->connect('127.0.0.1', 9501)) {
    $cli->send("data");
} else {
    echo "connect failed.";
}
```

##### Asynchronous mode


#### Example

``` php
<?php
if ($cli->connect('127.0.0.1', 9501)) {
      $cli->send("data");
} else {
      echo "connect failed.";
}
```
