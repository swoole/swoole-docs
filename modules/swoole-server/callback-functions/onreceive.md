## Events and Callback functions

### onReceive

The event `receive` happens when the worker process receives the data.

The callback function registered for the event `receive` will be called in the worker process which has received the data.

#### Example

```php
function onReceive(swoole_server $server, int $fd, int $reactor_id, string $data)
```

- `$server` the swoole server object

- `$fd` If the swoole server is in TCP mode, it's the id number of client. If the swoole server is in UDP mode, it's the value of client ip which has been calculated by some algorithm.

- `$reactor_id` If the swoole server is in TCP mode, it's the id number of reactor thread. If the swoole server is in UDP mode, it's the value of client port which has been calculated by some algorithm.

- `$data` the data received from the client. If the configurations about automatic protocol hasn't been set, the max length of data that worker process could receive is 64KB.

For the TCP mode, the data translated between client and server flows and has no boundary. It needs to set the configurations(eof_check/length_check/http_protocol) about spliting the data into package or process the data into package manually.

