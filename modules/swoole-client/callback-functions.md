# Swoole TCP/UDP client

## Events and Callback-functions List

There is no connect and close connection event for UDP. If you have set the callback function for event `connect`, it will be called immediately after the UDP client is created.

If you have set the callback function for event `close`, it will be called immediately after the UDP client is closed.

### Table of Contents

- onConnect
- onError
- onReceive
- onClose
- onBufferFull
- onBufferEmpty

#### onConnect

`connect` event happens when the client connect to the server successfully.

```php
function onConnect(swoole_client $client)
```

> For TCP client, it must set the callback function for event `connect`.

> For UDP client, it is optional to set the callback function for event `connect`.

#### onError

`error` event happens when the client fails to connect to the server.

```php
function onError(swoole_client $client)
```

> For UDP client, there is no event `error`.

#### onReceive

The `receive` event happens when the client receive the data from the server.

```php
function onReceive(swoole_client $client, string $data)
```
- `$data` data received from the server.

> If the client has set the configuration about `eof/length` check, the data received would be a whole packet.

#### onClose

The `close` event happens when the connection between the client and server is closed.

```php
function onClose(swoole_client $client)
```

> The `close` event is triggered when the connection is closed by either the server or the client.

#### onBufferFull

The `bufferfull` event happens when the buffer reaches the `buffer_high_watermark` which is set by `$client->buffer_high_watermark`. If the buffer is full, it can't send data to the server anymore.

```php
function onBufferFull(Swoole\Client $cli);
```
#### onBufferEmpty

The `bufferempty` event happens when the buffer reaches the `buffer_low_watermark` which is set by `$client->buffer_low_watermark`. If the buffer is empty, it can continue to send data to the server.

```php
function onBufferEmpty(Swoole\Client $cli);
```
