## Configuration

### max_request

the number of max request the worker process could receive.

The dafault value of `max_request` is 0 which means there is no limit of the max request. If the `max_request` is set to some number, the worker process will exit and release all the memory amd resouce occupied by this process after receiving the `max_request` request. And then, the manager will respawn a new worker process.

This parameter is to resolve the problem of nonlocalizable and slow memory leak.

> `max_request` only works for synchronous, blocking and stateless reponse program
> The totally asynchronous server should not set `max_request`
> `max_request` only works for `SWOOLE_PROCESS` mode.

```php
<?php
$serv = new swoole_server("127.0.0.1", 9501);
$serv->set(array(
            'worker_num' => 2,
            'max_request' => 3,
            'dispatch_mode'=>3,
));

$serv->on('receive', function ($serv, $fd, $from_id, $data) {
        $serv->send($fd, "Server: ".$data);
});

$serv->start();
```
Check the pid of worker process before request and after many times request.
