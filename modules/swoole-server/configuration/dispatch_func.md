## Configuration

### dispatch_func

Set the `dispatch_func` to dispatch the connection to the worker process.

The swoole server provides [five types of `dispatch_mode`](/modules/swoole-server/configuration/dispatch_mode.md). If the `dispatch_mode` can't meet your need, you can write C++ function or PHP function to realize customized dispatch strategy.

#### Usage

```php
$serv->set(array(
    'dispatch_func' => 'my_dispatch_function',
));
```
> Once the `dispatch_func` has been set, the configuration `dispatch_mode` would not work.

> If the function set by `dispatch_func`, the swoole will result in a fatal error.

> If the data dispatched is more than 8K, `dispatch_func` can get 0-8180 bytes data.

#### PHP function

> It is forbidden to add any blocking operation in the `dispatch_func` otherwise the `Reactor` group would stop.

```php
$serv->set(array(
    'dispatch_func' => function ($serv, $fd, $type, $data) {
        var_dump($fd, $type, $data);
        return intval($data[0]);
    },
));
```
Parameters:

 - `$fd`, the id number of client

 - `$type`, the type of data, `0`: receive data from the client, `4`: the connection with the client closes, `5`: the connection with the client starts

 - `$data`, the data to dispatch

Return:

the return must be a integer between 0 and `worker_num`

#### C++ function

In other extension, use `swoole_add_function` to register function to swoole

```c++
int dispatch_function(swServer *serv, swConnection *conn, swEventData *data);

int dispatch_function(swServer *serv, swConnection *conn, swEventData *data)
{
    printf("cpp, type=%d, size=%d\n", data->info.type, data->info.len);
    return data->info.len % serv->worker_num;
}

int register_dispatch_function(swModule *module)
{
    swoole_add_function("my_dispatch_function", (void *) dispatch_function);
}
```
