# Swoole EventLoop

Developers can use swoole EventLoop API to use the system EventLoop.

## Methods

### bool swoole_event_add(int $sock, mixed $read_callback, mixed $write_callback = null, int $flags = null);

Add new callback functions of a socket into the EventLoop.

Example:

``` php
<?php
$fp = stream_socket_client("tcp://www.qq.com:80", $errno, $errstr, 30);
fwrite($fp,"GET / HTTP/1.1\r\nHost: www.qq.com\r\n\r\n");

swoole_event_add($fp, function($fp) {
    $resp = fread($fp, 8192);
    // Remove the socket from eventloop
    swoole_event_del($fp);
    fclose($fp);
});
echo "Finish\n";
```

### bool swoole_event_set($fd, mixed $read_callback, mixed $write_callback, int $flags);

Update the event callback functions of a socket.

### bool swoole_event_del(int $sock);

Remove all event callback functions of a socket.

### void swoole_event_exit()

Exit the eventloop, only available at client side.

### void swoole_event_wait(void);

### swoole_event_write($fp, $data);

Write data to the socket.

Example:

``` php
<?php
$fp = stream_socket_client('tcp://127.0.0.1:9501');
$data = str_repeat('A', 1024 * 1024*2);

swoole_event_add($fp, function($fp) {
     echo fread($fp);
});

swoole_event_write($fp, $data);
```

### swoole_event_defer(mixed $callback_function);

Add callback function to the next event loop.

Example:

``` php
<?php
swoole_event_defer(function(){
    echo "After EventLoop\n";
});
```
