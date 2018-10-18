## Configuration

### open_websocket_protocol

Enable the process of websocket protocol.

The swoole  will enable this configuration `open_http_protocol` automatically if the configuration `open_websocket_protocol` has been enabled.

The swoole_websocket_server will enable this configuration automatically.

#### Usage

```php
$serv->set(array('open_websocket_protocol' => true));
```
