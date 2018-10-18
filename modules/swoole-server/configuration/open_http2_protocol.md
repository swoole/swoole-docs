## Configuration

### open_http2_protocol

Enable the process of http2 protocol.

This configuration needs to compile swoole with `--enable-http2`

#### Usage

```php
$serv->set(array('open_http2_protocol' => true));
```
