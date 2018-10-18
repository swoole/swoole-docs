# Swoole TCP/UDP client

## Properties List

### Table of Contents

- swoole_client->errCode

- swoole_client->sock

- swoole_client->reuse

### swoole_client->errCode

When the call of method `connect/send/recv/close` failed, the value of `swoole_client->errCode` is set automatically.

The value of `swoole_client->errCode` equals to the value of `errno` of Linux. You can use `socket_strerror` to check the concrete information of errCode.

```php
echo socket_strerror($client->errCode);
```

### swoole_client->sock

It is an integer which stands for the file descriptor of socket.

You can use this value to convert a stream socket used for `fread/fwrite/fclose` functions.

```php
$sock = fopen("php://fd/".$swoole_client->sock);
```

### swoole_client->reuse

It is an Boolean value which stands for reuse status of socket.

```php
if ($client->reuse)
{
    // reused socket
    $client->send($data);
}
else
{
    // new socket
    $client->doHandShake();
    $client->send($data);
}
```
