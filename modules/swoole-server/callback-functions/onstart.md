## Events and Callback functions

### onStart

When the swoole server starts, the event `start` happens and the swoole will call the callback function registered for `start` in the master process.

Before the `start` event, the swoole server has proceeded the below operations:

- Create the manager process
- Create the worker process
- Listen on the set TCP/UDP Port
- Listen on the timer

After the `start` event, the reactor will receive event and the client can connect the server

In the callback function registered for `start`, it only allows to log record and modify the name of process.

The event `start` and `workerstart` happen concurrently in different processes and have no precedence.

It is recommended to record the value of `$serv->master_pid` and `$serv->manager_pid` into file. If so, you can wirte script to send signal to control the process.

#### Example

```php
function onStart(swoole_server $server){

}
```
