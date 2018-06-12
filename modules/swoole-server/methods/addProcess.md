## Method

### swoole_server->addProcess

#### Prototype

```php
bool swoole_server->addProcess(swoole_process $process)
```

#### Illustration

Add a user defined child process to the server. The process can be used as monitoring or other tasks.

#### Parameter

* `$process` the swoole_process object defined by user
    - Check [the document of swoole_process](/modules/swoole-process/introduction.md)

##### Return

The return value indicates the result of add process to swoole server.

##### Example:

``` php
<?php
$server = new swoole_server('127.0.0.1', 9501);

$process = new swoole_process(function($process) use ($server) {
    while (true) {
        $msg = $process->read();
        foreach($server->connections as $conn) {
            $server->send($conn, $msg);
        }
    }
});

$server->addProcess($process);

$server->on('receive', function ($serv, $fd, $from_id, $data) use ($process) {
    // send the data received to all the child processes
    $process->write($data);
});

$server->start();
```
