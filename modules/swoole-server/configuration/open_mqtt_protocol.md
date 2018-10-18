## Configuration

### open_mqtt_protocol

Enable the process of mqtt protocol.

Once this configuration has enabled, the swoole will analyze the mqtt package head and the callback function `onReceive` will receive a whole mqtt package.

#### Usage

```php
$serv->set(array('open_mqtt_protocol' => true));
```
