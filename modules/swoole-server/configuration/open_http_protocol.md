## Configuration

### open_http_protocol

Enable the process of http protocol.

Once this configuration has enabled, the callback function `onReceive` will receive a whole http package.

The swoole_http_server will enable this configuration automatically.

#### Usage

```php
$serv->set(array('open_http_protocol' => true));
```
